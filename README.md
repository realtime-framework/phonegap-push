# Adobe PhoneGap Build iOS/Android Push Notifications with Realtime
This project shows how to build an Android app able to receive APNS and GCM push notifications built using the [Adobe PhoneGap Build](https://build.phonegap.com/) and the Realtime [CordovaPush](https://build.phonegap.com/plugins/3684) plugin.

## Push notifications setup guide

- Create a Google project, more info [here](http://messaging-public.realtime.co/documentation/starting-guide/mobilePushGCM.html).

- Add deviceready event listener to the HEAD section of your HTML page
 
		<script type="text/javascript">
		     document.addEventListener("deviceready",
		              function () {
		                if(window.plugins && window.plugins.OrtcPushPlugin){
		                        var OrtcPushPlugin = window.plugins.OrtcPushPlugin;
		                        OrtcPushPlugin.checkForNotifications();
		                 }
		               }, false);
		</script>

- Enter your Realtime Application Key and Google Project Number at the `OrtcPushPlugin.connect` call: 
				
- Set the `push-notification` event listener: 

		document.addEventListener("push-notification", function(notification) {              
              var payload = document.getElementById('payload');
              payload.innerHTML = JSON.stringify( notification.payload );
              payload.value = JSON.stringify( notification.payload );
           }, false);

- Add the `CordovaPush` plugin to your `config.xml` file:

		<gap:plugin name="co.realtime.plugins.cordovapush" version="0.1.5" />
		
		
## Testing the app
Start the app, enter a channel name and subscribe to it.

Now open the Realtime Web Console at [http://console.realtime.co](http://console.realtime.co), enter your Realtime Application Key, connect and send a message to the channel you have subscribed in the app.

If the app is in background or closed you should see a new message added to your notification manager. Tapping it will open the app and show the push payload in the UI.

If the app is in foreground you should see the push payload immediately in the UI.
 
## Documentation
The CordovaPush Plugin Documentation can be found [here](https://github.com/realtime-framework/CordovaPush).

The complete Realtime® Messaging reference documentation is available [here](http://framework.realtime.co/messaging/#documentation)

## Security note

For simplicity these samples assume you're using a Realtime® Framework developers' application key with the authentication service disabled (every connection will have permission to publish and subscribe to any channel). For security guidelines please refer to the [Security Guide](http://messaging-public.realtime.co/documentation/starting-guide/security.html). 
 
**Don't forget to replace `YOUR_APPLICATION_KEY` with your own application key. If you don't already own a free Realtime Messaging application key, [get one now](https://accounts.realtime.co/signup/).**
   