Setup SendBird with JavaScript SDK 
=========================

### Download and Install
After downloading the `SendBird JavaScript SDK` JavaScript file, add it to your Project Classpath (`generally the libs directory`).  
You can download the latest `SDK` here:  

<a class="sendbird-btn sendbird-btn--green" href="download_sdk.html">Download SendBird JavaScript SDK</a>

### 1. Setup APP ID and Login to SendBird
Initialize SendBird by using the assigned APP ID.

```javascript
  ...
  sendbird.init({
    "app_id": string,
    "guest_id": string,
    "user_name": string,
    "image_url": string,
    "access_token": string,
    "successFunc": function(data) {
      console.log(data);
      // do something...
    },
    "errorFunc": function(status, error) {
      console.log(status, error);
      // do something
    }
  });
  ...
```

 * **app_id**: Your `SendBird` `APP_ID` found on the dashboard  
   - `e.g.) X951XA51-AXAE-1XE4-8XC1-10DDXXDX1X5F`  
 * **guest_id**: Unique key of user  
   - `e.g.) user001`  
 * **user_name**: User Nickname
 * **image_url**: Profile image `URL` of the user   
 * **access_token**: If you set access token `true` using [Server API](https://sendbird.gitbooks.io/sendbird-server-api/content/en/user.html) and make a user from it, you should set this value. If it's not, just set empty string.   

### 2. Define Event Function
Define event functions that handle the message transfers.

```javascript
sendbird.events.onMessageReceived = function(obj) {
  console.log(obj);
  // do something
};

sendbird.events.onSystemMessageReceived = function(obj) {
  console.log(obj);
  // do something...
};

sendbird.events.onFileMessageReceived = function(obj) {
  console.log(obj);
  // do something...
};

sendbird.events.onBroadcastMessageReceived = function(obj) {
  console.log(obj);
  // do something...
};

sendbird.events.onMessagingChannelUpdateReceived = function(obj) {
  console.log(obj);
  // do something...
};


sendbird.events.onTypeStartReceived = function(obj) {
  console.log(obj);
  // do something...
}

sendbird.events.onTypeEndReceived = function(obj) {
  console.log(obj);
  // do something...
}

sendbird.events.onReadReceived = function(obj) {
  console.log(obj);
  // do something...
};

sendbird.events.onMessageDelivery = function(obj) {
  console.log(obj);
  // do something...
};
```

 * **onMessageReceived**: The function is called when a generic message has been received.
 * **onSystemMessageReceived**: The function is called when a system message has been received.
 * **onFileMessageReceived**: The function is called when a file message has been received.
 * **onBroadcastMessageReceived**: The function is called when a broadcast message has been received.
 * **onMessagingChannelUpdateReceived**: The function is called when a 1-on-1 Messaging channel/Group Messaging channel has been updated.
 * **onTypeStartReceived**: The function is called when a typing start message has been received.
 * **onTypeEndReceived**: The function is called when a typing end message has been received.
 * **onReadReceived**: The function is called when signal that other user read message in messaging channel has been received.
 * **onMessageDelivery**: The function is called when a message has been sent.


#### Event object
Event object passed by event functions has the following format.

```json
  {
    "data": string,        // reserved data. will come soon.
    "message": string,     // message string
    "ts": int,             // timestamp
    "user": {
      "guest_id": string,  // user unique id
      "image": string,     // user profile image url
      "name": string       // user nickname
    }
  }
```

 * **other fields**: Internal use only or deprecated 
