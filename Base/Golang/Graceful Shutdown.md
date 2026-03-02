2026-03-02 23:13
Tags: #golang 

Graceful Shutdown в Go позволяет завершить работу сервиса без потери данных, дождавшись окончания всех горутин, запросов и соединений. Статья описывает антипаттерны и пошаговую реализацию с использованием каналов, WaitGroup, context и сигналов ОС.

---

### Антипаттерны

Избегайте искусственного блокирования горутины без ожидания
(например, `<-ch` с nil-каналом) и `os.Exit()`,
который убивает процесс как SIGKILL, не закрывая соединения. Эти подходы приводят к потере данных и незавершенным операциям.

---

### Ожидание горутин

- **Канал**: Создайте `chan struct{}`, каждая горутина сигнализирует `defer close(ch)`, основная читает столько раз, сколько горутин.
    
- **sync.WaitGroup**: `wg.Add(1)` перед `go`, `defer wg.Done()` внутри; основная ждет `wg.Wait()`.
    
- **golang.org/x/sync/errgroup**: `g, ctx := errgroup.WithContext(ctx); g.Go(func() error {...}); g.Wait()` — передает ошибки и отмену.

---

### Обработка сигналов

Перехватывайте `os.Interrupt` (Ctrl+C) и `syscall.SIGTERM` (Docker/K8s): `c := make(chan os.Signal, 1); signal.Notify(c, ...)`.
Используйте `select` с `<-c` для прерывания циклов вместо `time.Sleep`.

---

### Context для отмены

`ctx, cancel := context.WithCancel(context.Background())`;
передавайте ctx в горутины, проверяйте `<-ctx.Done()`.
Для сигналов: `ctx, stop := signal.NotifyContext(ctx, os.Interrupt, syscall.SIGTERM)`.
Вызов `cancel()` или `stop()` транслируется всем.

---

### HTTP-сервер

Запустите `http.Server` в errgroup: одна горутина — `ListenAndServe()`, вторая ждет `<-ctx.Done()` и вызывает `Shutdown(ctx)`.
Установите `BaseContext: func() context.Context { return mainCtx }` для отмены запросов.
Новые соединения блокируются, активные завершаются.

---

### Каналы воркеров

Закрывайте канал после всех писателей: `g.Wait(); close(ch)`.
Читайте с `for v := range ch` или `select { case v, ok := <-ch: if !ok { return } }`. Один писатель — `defer close(ch)` в defer.

---

### Пример полного main()

```go
mainCtx, stop := signal.NotifyContext(context.Background(), os.Interrupt, syscall.SIGTERM)
defer stop()

srv := &http.Server{Addr: ":8000", BaseContext: func(_ net.Listener) context.Context { return mainCtx }}

g, gCtx := errgroup.WithContext(mainCtx)
g.Go(func() error { return srv.ListenAndServe() })
g.Go(func() error { <-gCtx.Done(); return srv.Shutdown(context.Background()) })
g.Wait()
```
Этот код обеспечивает graceful shutdown сервера.

---
### Links
[[Base/Golang/Golang|Golang]]