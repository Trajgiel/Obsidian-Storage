2025-01-03 10:43
Tags: #nextjs 

## Содержание:
- [React Compiler](#React%20Compiler)
- [Исправление поведения кэширования](#Исправление%20поведения%20кэширования)
- [Partial Prerendering (PPR)](#Partial%20Prerendering%20(PPR))
- [API next/after](#API%20next/after)
- [Оптимизация бандлинга внешних пакетов](#Оптимизация%20бандлинга%20внешних%20пакетов)

---

### ReactCompiler

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

### Оптимизация бандлинга внешних пакетов

Теперь у разработчиков есть больше возможностей контролировать, какие пакеты попадают в бандл, что позволяет значительно уменьшить его размер.

Опция *\*bundlePagesRouterDependencies** включает автоматическое объединение зависимостей на стороне сервера для приложений, использующих Pages Router:
```js
/** @type {import('next').NextConfig} */
const nextConfig = {  
  bundlePagesRouterDependencies: true,
};

module.exports = nextConfig;
```

Вы можете использовать опцию **serverExternalPackages**, чтобы отказаться от определенных пакетов, если это необходимо. Чтобы исключить пакеты из бандла используйте:
```js
const nextConfig = {
  // Automatically bundle external packages in the Pages Router:
  bundlePagesRouterDependencies: true,
  // Opt specific packages out of bundling for both App и Pages Router:
  serverExternalPackages: ['package-name'],
};

module.exports = nextConfig;
```

С помощью опции  [transpilePackages](https://nextjs.org/docs/pages/api-reference/next-config-js/transpilePackages) Next.js может автоматически транспилировать и бандлить зависимости из локальных пакетов (например, монорепозиториев) или внешних зависимостей (node_modules). Это заменяет пакет next-transpile-modules.

С помощью опции **transpilePackages** Next.js может автоматически транспилировать и бандлить зависимости из локальных пакетов (например, из монорепозиториев) или внешних зависимостей (node_modules). Эта опция заменяет пакет next-transpile-modules:

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  transpilePackages: ['package-name'],
};

module.exports = nextConfig;
```

Опция **optimizePackageImports** позволит загружать только те модули, которые вы действительно используете:

```js
/** @type {import('next').NextConfig} */
const nextConfig = {  
  experimental: {    
    optimizePackageImports: ['icon-library'],  
  },
};

module.exports = nextConfig;
```

Опция **serverExternalPackages** позволяет исключить из объединения определенные пакеты:

```js
/** @type {import('next').NextConfig} */
const nextConfig = {  
  serverExternalPackages: ['package-name'],
};

module.exports = nextConfig;
```

Подробнее о технологии можно почитать [здесь](https://nextjs.org/docs/app/building-your-application/optimizing/package-bundling).

---
### Links
[[Next.js]]
