# push-notification
Template project with work notifications
 
##  Для начала нужно установить react-native-firebase/app и react-native-firebase/messaging

### Installation

Requires `@react-native-firebase/app` to be installed.

```bash
yarn add @react-native-firebase/messaging
```

### Documentation `@react-native-firebase/app`

- [Quick Start](https://rnfirebase.io/app/usage)
- [Reference](https://rnfirebase.io/reference/app)

### Documentation  `@react-native-firebase/messaging`

- [Quick Start](https://rnfirebase.io/messaging/usage)
- [Reference](https://rnfirebase.io/reference/messaging)

## Переходим к React Native Push Notifications

### Installation

```bash
npm install --save react-native-push-notification
```
**ПРИМЕЧАНИЕ. Если вам также нужны уведомления и на iOS, необходимо установить [PushNotificationIOS](https://github.com/react-native-community/react-native-push-notification-ios), поскольку этот пакет зависит от него. В противном случае, моежете переходить к пункту 4**

## Подключение уведомлений на IOS через PushNotificationIOS

  ### Installation

  ```bash
  yarn add @react-native-community/push-notification-ios
  ```
  ## Добавьте Background Mode - Remote Notifications

  Перейдите в каталог MyReactProject/ios и откройте MyProject.xcworkspace. Выберите папку «MyProject» и вкладку `Signing & Capabilities`, далее найдите чуть ниже '+' и дважды нажмите на него: 

<p align="center">
    <img width="800px" src="https://i.ibb.co/mJ8KHgR/Screenshot-2020-08-20-at-20-46-53.png"><br/>
</p>
