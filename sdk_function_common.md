SendBird JavaScript SDK Function: Common
=================================
References to the functions used to implement real-time open chat using `SendBird`.    

### Download and Install 
All of the functions are included in `SendBird JavaScript SDK`. No additional installs are necessary.


### 1. Join Channel / Connect to Channel
Make a connection to a channel.

After Wed SDK 2.1 version, all of connect/join functions are asynchronous now.

For Open Chat, please check out this link.

[Join Open Chat Channel](https://sendbird.gitbooks.io/sendbird-web-sdk/content/en/sdk_function_openchat.html) 

For 1 on 1 or Group Messaging, please check out this link.

[Start 1-on-1 Messaging or Join Messaging Channel](https://sendbird.gitbooks.io/sendbird-web-sdk/content/en/sdk_function_message.html)


### 2. Disconnect Messaging Connection

Disconnect the messaging connection from the channel explicitly.

If you join/connect another channel, this is called automatically. You can call this when you don't want to get any real-time updates from the channel. ex) when you get back to channel list UI.

```javascript
  ...
  sendbird.disconnect();
  ...
```  


### 3. Send Message
Send a text message to Open Chat or 1-on-1/Group Messaging channels.

####3.1. When you want to send a message only

```javascript
  ...
  sendbird.message(msg);
  ...
```

 * **msg**: Message to be sent.
 
####3.2. When you want to send a message with other data

```javascript
  ...
  sendbird.messageWithData(msg, data);
  ...
```

 * **msg**: Message to be sent.
 * **data**: String field contains any structured data you want to send. You should properly stringify them. ex) json/xml

####3.3. When you want to send a message with tempId

TempId is used to check if your message has been delivered successfully.
Next section describes how you can use it.

```javascript
  ...
  sendbird.message(msg, tempId);
  ...
```

 * **msg**: Message to be sent.
 * **tempId**: Unique temporary id for this message.
 
or  

```javascript
  ...
  sendbird.messageWithData(msg, data, tempId);
  ...
```

 * **msg**: Message to be sent.
 * **data**: String field contains any structured data you want to send. You should properly stringify them. ex) json/xml
 * **tempId**: Unique temporary id for this message.

### 3.4. How to check if your message has been delivered successfully with tempId

All messages each client sends are returned back to itself in `onMessageReceived` along with messages coming from others.

If the client attaches a `tempId` to its messages, then they are returned with `tempId`.

By storing tempIds in local and comparing them to tempIds coming in `onMessageReceived`, you can check which messages are delivered or not. 

You should generate locally unique ids.


### 4. Send File

Send a file to Open Chat or 1-on-1/Group Messaging channels.

####4.1. When you already have your own file servers and file links

You can use `sendFileURL` to send a file link with relevant fields.

```javascript
  ...
  var fileInfo = {
    "url": file_url,
    "name": file_name,
    "type": file_type,
    "size": file_size,
    "custom": ''
  };
  sendbird.sendFileURL(fileInfo);
  ...
```
  * **fileInfo.url**: An url of the file you want to use
    - `e.g.) https://example.com/test_img.png`
  * **fileInfo.name**: File name
  * **fileInfo.size**: File size (in bytes)
  * **fileInfo.type**: File type string
  * **fileInfo.custom**: A field that you can pass any custom string data to be saved

####4.2. When you want to upload a file to SendBird server

You can use `sendFile` to send a file to the `SendBird` server and call `sendFileURL` automatically. File size is limited up to 25MB.

```javascript
  ...
  sendbird.sendFile(
    file, 
    {
      "successFunc" : function(data) {
        console.log(data);
        // do something
      },
      "errorFunc": function(status, error) {
        console.log(status, error);
        // do something
      } 
    }
  );
  ...
```
  * **file**: File DOM object to be transferred
    - `e.g.) $('#file_input_field')[0].files[0]`

#### Response
Response is a url of the uploaded file
```json
  {
    "error": boolean
    "url": string
  }
```
or 
```json
  {
    "error": boolean
    "message": string
  }
```
  * **error**: error status.
  * **url**: uploaded file url in `SendBird` server  
    - `e.g.) https://s3.amazonaws.com/sendbird/test_img.png`
  * **message**: reason of error . 
    - `e.g.) Maximum file size <= 25MB`  


### 5. Get Message
Get messages from the current channel.

```javascript
  ...
  sendbird.getMessageLoadMore({
    "limit": limit,
    "successFunc" : function(data) {
      console.log(data);
      // do something
    },
    "errorFunc": function(status, error) {
      console.log(status, error);
      // do something
    }
  });
  ...
```

 * **limit**: Number of messages to be displayed per page. `default: 20`  


### 6. Get Channel Member List
Get a list of members on the channel.

```javascript
  ...
  sendbird.getMemberList(
    url,
    {
      "successFunc" : function(data) {
        console.log(data);
        // do something
      },
      "errorFunc": function(status, error) {
        console.log(status, error);
        // do something
      } 
    }
  );
  ...
```

 * **url**: `URL` of the channel to get a list from
   - `e.g.) sendbird.test_channel_1`  


#### Response

```json
  {
    "members": [
      0: {
        "guest_id": string,   // user unique id
        "is_online": boolean, // user online state
        "picture": string,    // user profile image url
        "nickname": string    // user nickname
      },
      1: {
        ...
      },
      ...
    ],
    "next": int // next page number. if this value is 0, next page are not exist.
    "page": int // current page number
  }
```

 * **other fields**: Internal use only or deprecated 
 

### 7. Delete a message
Delete a message permanently.
A client which has a local cache should reload chat data in its side. 

```javascript
  ...
  sendbird.deleteMessage(
    msgId,
    {
      "successFunc" : function(data) {
        console.log(data);
        // do something
      },
      "errorFunc": function(status, error) {
        console.log(status, error);
        // do something
      } 
    }
  );
  ...
```

 * **msgId**: Unique key of each message. It's equivalent to `msg_id` field in message object.


#### Response

```json
  {
    "app_id": string,
    "msg_id": int
  }
```

### 8. Extract Command and Payload
Extract a command and a payload from a raw message.
Basically it is used with `5. Get Message`.

```javascript
  ...
  sendbird.getMessageLoadMore({
    "successFunc" : function(data) {
      console.log(data);
      moreMessage = data["messages"];
      $.each(moreMessage.reverse(), function(index, msg) {
        console.log(item);
      });
      // do something
    },
    "errorFunc": function(status, error) {
      console.log(status, error);
      // do something
    }
  });
  ...
```


#### Response
```json
  {
    "cmd": string, 
    "payload": json
  }
```


### 9. Check Message
Check if the type of the message is text message.
Return a boolean.

```javascript
  ...
  sendbird.isMessage(item.cmd)
  ...
```

  * **item**: One of the items in the list returned from `5. Get Message`.  


### 10. Check File
Check if the type of the message is file.
Return a boolean.

```javascript
  ...
  sendbird.isFileMessage(item.cmd)
  ...
```

  * **item**: One of the items in the list returned from `5. Get Message`.  


### 11. Check Image
Check if this file has any images.
Return a boolean.

```javascript
  ...
  sendbird.hasImage(item.payload)
  ...
```

  * **item**: One of the items in the list returned from `5. Get Message`.  

### 12. Set Debug
Print the debug messages. You can check them in the console tab of browser developer tools. The default value is false.

```javascript
  ...
  sendbird.setDebugMessage(boolean);
  ...
```  


### 13. Get Channel Info  
Get current channel info.    

```javascript  
  {
    ...
    sendbird.getChannelInfo(function(data) {
      console.log(data);
    });
    ...
  }
```

#### Response

```javascript  
  {
    channel_url: string,
    cover_img_url: string,
    member_count: int,
    name: string
  }
```

### 14. Get User Info  
Get current user info.    

```javascript  
  {
    ...
    sendbird.getUserInfo(function(data) {
      console.log(data);
    });
    ...
  }
```

#### Response

```javascript  
  {
    guest_id: string,
    image_url: string,
    nickname: string
  }
```

### 15. Check version    
Check current SDK version.   

```javascript  
  {
    ...
    sendbird.version
    ...
  }
```

#### Response  
 
```javascript  
  [version] x.x.x;
```
