2022-07-17 19:53
Tags: #GitHub
__
# GitHub-pages

Порядок установки:
1) `yarn add gh-pages` или `yarn add gh-pages --dev`

2) добавить в package.json:
```tsx
"homepage": "https://Traihel.github.io/ToDoList-TS",

// после строки например "name": ...
//homepage: "https://ВашЛогин.github.io/НазваниеРеппозитория" 
```

3) добавить в package.json в объект "scripts":
```tsx
"predeploy": "npm run build",
"deploy": "gh-pages -d build"
```

4) после каждого коммит/пуша нужно сделать `yarn deploy` чтобы изменения в проекте появились на вашем сайте

package.json:
![[deploy.jpg]]
__
### Links
[[Install React]]