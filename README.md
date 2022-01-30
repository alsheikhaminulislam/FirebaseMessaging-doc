> Add Firebase Library (this version)
```
   implementation 'com.google.firebase:firebase-messaging:17.3.4'
```

> Get user Token or Topic
```
   String token =  FirebaseInstanceId.getInstance().getToken();
   subscribe
   FirebaseMessaging.getInstance().subscribeToTopic("Topicname");
   Un Subscribe
   FirebaseMessaging.getInstance().unsubscribeFromTopic("Topicname");
```

> Now Add this
```
   dependencies {
      implementation files("libs/firebasemessaging-1.0.0.aar")
   }
```
```
   implementation files("libs/firebasemessaging-1.0.0.aar")
```
> Server Notification Builder
```
   FCMBuilder.Builder builder = new FCMBuilder.Builder(this,"FIREBASE SERVER KEY");
        builder.setTitle("");
        builder.setBody("");
        builder.setTarget(""); // user Token or Topic
        builder.setPriority(FCMNotificationManagerCompat.PRIORITY_USER); // OR FCMNotificationManagerCompat.PRIORITY_TOPIC
        builder.setDataOne("");
        builder.setDataTwo("");
        builder.setDataThree("");
        builder.setDataFour("");
        builder.setDataFive("");
        builder.setIconURL("");
```

> Create FCMNotificationManagerCompat with or without ValueEventListener
```
   FCMNotificationManagerCompat fcmNotificationManagerCompat = new FCMNotificationManagerCompat.from(this);
      fcmNotificationManagerCompat.notify(builder);
      fcmNotificationManagerCompat.notify(builder, new ValueEventListener() {
         @Override
         public void onSuccess() {
         }
         @Override
         public void onResult(String result) {
         }
         @Override
         public void onError(String e) {

         }
      });
```

> Create a new java class in my case the name is: myFirebaseMessaging.java
> If you wish to do any message handling beyond receiving notifications on apps in the background, create a new Service ( File &gt; New &gt; Service &gt; Service ) that extends FirebaseMessagingService . This service is necessary to receive notifications in foregrounded apps, to receive data payload, to send upstream messages, and so on.<br>In this service create an onMessageReceived method to handle incoming messages.

```
   public class myFirebaseMessaging extends FirebaseMessagingService {
    @Override
    public void onMessageReceived(RemoteMessage remoteMessage) {
        super.onMessageReceived(remoteMessage);
            String Title = remoteMessage.getNotification().getTitle();
            String Body = remoteMessage.getNotification().getBody();
            String DataOne = remoteMessage.getData().get( FCMNotificationManagerCompat.DataOne);
            String DataTwo = remoteMessage.getData().get( FCMNotificationManagerCompat.DataTwo);
            String DataThree = remoteMessage.getData().get( FCMNotificationManagerCompat.DataThree);
            String DataFour = remoteMessage.getData().get( FCMNotificationManagerCompat.DataFour);
            String DataFive = remoteMessage.getData().get( FCMNotificationManagerCompat.DataFive);
            String ICONURL = remoteMessage.getData().get( FCMNotificationManagerCompat.ICONURL);
       }
   }
```
