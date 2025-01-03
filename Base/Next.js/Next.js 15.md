2025-01-03 10:43
Tags: #nextjs 

---

### React Compiler
это долгожданное улучшение. Он автоматически оптимизирует код и мемоизирует компоненты, самостоятельно определяя, где это необходимо, чтобы избежать лишних перерисовок. Это устранит одну из главных проблем разработчиков. Подключить компилятор можно через ‘next.config.js’
```js
const nextConfig = {  
  experimental: {    
    reactCompiler: true,  
  },
}; 

module.exports = nextConfig;
```

---

### Исправление поведения кэширования
По умолчанию используется флаг ‘no-store’, который отключает кэширование и гарантирует получение актуальной информации.
```js
// было:
fetch("https:// …" , { cache: 'force-cache' });
// стало:
fetch("https:// …" , { cache: 'no-store' });
```
Возможные значения:
- ‘no-store’ — получать ресурс с удаленного сервера при каждом запросе и не обновлять кеш.
- ‘force-cache’ — получить ресурс из кеша (если он существует) или удаленного сервера и обновить кэш.

---

### Partial Prerendering (PPR)
Эта экспериментальная функция впервые появилась в версии 14 и продолжает дорабатываться. Partial Prerendering делит страницу на сегменты, часть из которых будет сгенерирована статично, а другая — динамично. Это позволяет рендерить страницу частично статически и частично динамически, что улучшает производительность и пользовательский опыт.
```js
import { Suspense } from "react";
import { StaticComponent, DynamicComponent } from "@/app/ui";

export const experimental_ppr = true;

export default function Page() {  
  return (    
    <>	     
      <StaticComponent />
      <Suspense fallback={...}>
        <DynamicComponent />	    
      </Suspense>     
    </>
  );
}
```
Если включен частичный предварительный рендеринг (PPR), страница Page генерирует статическую оболочку на основе установленной границы<Suspense />. fallback из React Suspense предварительно визуализируется.
Резервные варианты отображения в оболочке (т. е. fallback, на месте которого обычно рисуют Skeleton или Loader) затем заменяются динамическими компонентами (<DynamicComponent />), например, такими как чтение файлов cookie для определения корзины или показ баннера на основе данных о пользователе.

Чтобы пользоваться этой функцией, нужно предварительно подключить её:
```js
const nextConfig = {  
  experimental: {   
    ppr: 'incremental',  
  },
};

module.exports = nextConfig;
```

---

### API next/after
API after() разделяет задачи на сервере на "основные" и "вторичные". Это позволяет клиенту получать ответ быстрее, так как вторичные задачи (например, логирование или аналитика) выполняются позже. Сейчас клиенту приходится ждать, пока "вторичные" задачи завершатся, прежде чем он получит ответ на запрос. Однако after()изменит этот порядок. Например, если мы хотим посмотреть видео на сайте, то по логике after() сначала загрузится интересующий нас контент, и только потом начнется выполнение аналитики и других второстепенных задач на сайте.

Пример использования after():
```js
import { unstable_after as after } from 'next/server';
import { log } from '@/app/utils';
 
export default function Layout({ children }) {
  // Secondary task
  after(() => {
    log();
  });
 
  // Primary task
  return <>{children}</>;
}
```
Чтобы функция заработала, её нужно подключить в next.config:
```js
const nextConfig = {
  experimental: {
    reactCompiler: true,
  },
};

module.exports = nextConfig;
```

[Документация по API unstable_after](https://nextjs.org/docs/app/api-reference/functions/unstable_after)

---

### Оптимизация бандлинга внешних пакетов (стабильная версия)
Теперь у разработчиков есть больше возможностей контролировать, какие пакеты попадают в бандл, что позволяет значительно уменьшить его размер.

Опция bundlePagesRouterDependencies включает автоматическое объединение зависимостей на стороне сервера для приложений, использующих Pages Router:
```js
/** @type {import('next').NextConfig} */
const nextConfig = {  
  bundlePagesRouterDependencies: true,
};

module.exports = nextConfig;
```

---
### Links
[[Next.js]]
