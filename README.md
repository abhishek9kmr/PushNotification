# PushNotification
This is simple project for learning push notification in android
=====================================================================

Steps to create push notification project
==========================================

In this project we will see android notification in foreground state, background state and kill state.

1) create react-native project.
2)Create a project in firebase.(click next-next and select default account).
3)Get started by adding Firebase to your app - select android option from ios,android,web, unity,flutter
4)Fill package name - You can get it at multiple places - MainActivity.kt or MainApplication.kt or build.gradle applicationId.
5) Generate SHA1 key and fill using command-cd android && ./gradlew signingReport.
6)Download google-services.json file and place it inside app folder of android project.
7)Add firebase sdk - change dependencies and add plugins as per documentation.
8)We will have to setup the firebase within the react native application. follow rnfirebase.io
9)Cloud-messaging will be used in the application. Install the necessary libraeries.
10)We need to get device token using const token =await messaging().getToken();
11) We will go to test fcm site for testing and we will need server key. To get server key go to Project -> project setting -> cloud messaging -> cloud api messaging legacy. We have to enable it. click on 3 dots.
12)Provide notification permission in AndroidManifest.xml

Code
======

 //Function to get device token.
  const tokenFun = async()=>{
    const token = await messaging().getToken();
    console.log(token)

In App.js
===========

// This will show notification in foreground state.
  useEffect(() => {
    const unsubscribe = messaging().onMessage(async remoteMessage => {
      Alert.alert('A new FCM message arrived in foreground state!', JSON.stringify(remoteMessage));
    });
    return unsubscribe;
  }, []);

In Index.js
============

// We will be able to read data from notification when app is in background state
messaging().setBackgroundMessageHandler(async remoteMessage => {
    console.log('Message handled in the background!', remoteMessage);
  });

//We will be able to read data from notification when app is in killed state
messaging().getInitialNotification(async remoteMessage => {
    console.log('Message handled in the background!', remoteMessage);
  });


