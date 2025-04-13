2022-10-15 12:29
Tags: #ReactNative
__
# React Native

---

### Установка React Native Expo:
`npm i -g expo-cli` - устанавливаем  expo глобально
`expo init my-app` - инициальзируем проект в папке
`yarn start` - запуск приложения (в папке проекта)

---

### React-Navigation
yarn add @react-navigation/native
npx expo install react-native-screens react-native-safe-area-context
yarn add @react-navigation/native-stack

---

### Drawer navigation
yarn add @react-navigation/drawer - боковая понель выезжающая
yarn add @react-navigation/bottom-tabs - нижние табы приложения
npx expo install react-native-gesture-handler react-native-reanimated

```ts
//babel.config.js
plugins: ['react-native-reanimated/plugin'],
```
`expo start -c`

---

Вложености и их написание
```ts
navigation.navigate('Name')
navigation.navigate('Name1')
navigation.navigate('Name2')

navigation.navigate('Home', { screen: 'Profile' })
navigation.navigate('Home', { screen: 'Home' })
navigation.navigate('Home', { screen: 'Jobs' })

navigation.navigate('Home', { screen: 'Profile', {screen: 'Name' }})
navigation.navigate('Home', { screen: 'Home', {screen: 'Name' }})
navigation.navigate('Home', { screen: 'Jobs', {screen: 'Name' }})

```

---

### Тэги:
`View` - это аналог div
`Text` - внутри писать текст
`TextInput` - аналог input
`ActivityIndicator` - индикато загрузки (preloader)
`TouchableOpacity` - это кнопка которую можно стилизовать
`FlatList` - тот же map, позволяет вывести массив данных
`ScrollView` - добавляет возможность скролить приложение
`Pressable` - внутри тега объект становиться кликабельным

__
### Links
[[Base/React/React]]