# push-notification
Template project with work notifications
 
##  Для начала нужно установить react-native-firebase/app и react-native-firebase/messaging

#### Installation

Requires `@react-native-firebase/app` to be installed.

```bash
yarn add @react-native-firebase/messaging
```

#### Documentation `@react-native-firebase/app`

- [Quick Start](https://rnfirebase.io/app/usage)
- [Reference](https://rnfirebase.io/reference/app)

#### Documentation  `@react-native-firebase/messaging`

- [Quick Start](https://rnfirebase.io/messaging/usage)
- [Reference](https://rnfirebase.io/reference/messaging)

## Переходим к React Native Push Notifications

#### Installation

```bash
npm install --save react-native-push-notification
```
**ПРИМЕЧАНИЕ. Если вам также нужны уведомления и на iOS, необходимо установить [PushNotificationIOS](https://github.com/react-native-community/react-native-push-notification-ios), поскольку этот пакет зависит от него. В противном случае, моежете переходить к пункту 4**

## Подключение уведомлений на IOS через PushNotificationIOS

  #### Installation

  ```bash
  yarn add @react-native-community/push-notification-ios
  ```
  #### Добавьте Background Mode - Remote Notifications

  Перейдите в каталог MyReactProject/ios и откройте MyProject.xcworkspace. Выберите папку «MyProject» и вкладку `Signing & Capabilities`, далее найдите чуть ниже '+' и дважды нажмите на него: 

<p align="center">
    <img width="800px" src="https://i.ibb.co/mJ8KHgR/Screenshot-2020-08-20-at-20-46-53.png"><br/>
</p>

В итоге должно получится также, как на следующем скрине: 

<p align="center">
    <img width="400px" src="https://i.ibb.co/1R4d2md/Screenshot-2020-08-20-at-20-54-23.png"><br/>
</p>

Наконец, чтобы включить поддержку уведомлений нв IOS, необходимо изменить AppDelegate.

#### `AppDelegate.h`

В начале файла добавьте следующую строчку:

```objective-c
#import <UserNotifications/UNUserNotificationCenter.h>
```

Затем припишите в протоколы UNUserNotificationCenterDelegate:

```objective-c
@interface AppDelegate : UIResponder <UIApplicationDelegate, RCTBridgeDelegate, UNUserNotificationCenterDelegate>
```

#### `AppDelegate.m`

В начале файла: 

```objective-c
#import <UserNotifications/UserNotifications.h>
#import <RNCPushNotificationIOS.h>
```

Перед последним @end : 

```objective-c
// Required to register for notifications
- (void)application:(UIApplication *)application didRegisterUserNotificationSettings:(UIUserNotificationSettings *)notificationSettings
{
 [RNCPushNotificationIOS didRegisterUserNotificationSettings:notificationSettings];
}
// Required for the register event.
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
{
 [RNCPushNotificationIOS didRegisterForRemoteNotificationsWithDeviceToken:deviceToken];
}
// Required for the notification event. You must call the completion handler after handling the remote notification.
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
{
  [RNCPushNotificationIOS didReceiveRemoteNotification:userInfo fetchCompletionHandler:completionHandler];
}
// Required for the registrationError event.
- (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error
{
 [RNCPushNotificationIOS didFailToRegisterForRemoteNotificationsWithError:error];
}
// IOS 10+ Required for localNotification event
- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void (^)(void))completionHandler
{
  [RNCPushNotificationIOS didReceiveNotificationResponse:response];
  completionHandler();
}
// IOS 4-10 Required for the localNotification event.
- (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification
{
 [RNCPushNotificationIOS didReceiveLocalNotification:notification];
}

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  ...
  // Define UNUserNotificationCenter
  UNUserNotificationCenter *center = [UNUserNotificationCenter currentNotificationCenter];
  center.delegate = self;

  return YES;
}

//Called when a notification is delivered to a foreground app.
-(void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
{
  completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}
```
