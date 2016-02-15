SendBird JavaScript SDK Function: Messaging
=================================
Function references to implement private messaging features.

### 1-on-1 Messaging 
It is suitable for private messaging between users.  
It also offers additional features such as read receipts and typing indicators.

* Note: An user can remove itself from a channel. But the channel appears on the list of channels again when the other person sends new message to the user.
 

### Group Messaging 
It is suitable for private group communications.  
Only users who have been added/invited to the channel can see  messages and the list of members in the channel.  
When an user leaves or is removed from the channel, the channel disappears from the list.  

### Download and Install 
All of the functions are included in `SendBird JavaScript SDK`. No additional files or installations are required.


### 1. Start 1-on-1 Messaging
Start 1-on-1 messaging.

```javascript
  ...
  sendbird.startMessaging(
    guestIds,
    {
      "successFunc" : function(data) {
        console.log(data);
        sendbird.connect({
          "successFunc" : function(data) {
            console.log(data);
            // do something
          },
          "errorFunc": function(status, error) {
            console.log(status, error);
            // do something
          }
        });
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

 * **guestIds**: `Guest ID` of the users to be invited for 1-on-1 and group messaging. It can handle both a string format and an array (if you want to start with multiple users)
   - `e.g.) "76f01c7a-52bc-4c2b-b3c6-09f2649aa11e" or or ["76f01c7a-52bc-4c2b-b3c6-09f2649aa11e"] or ["76f01c7a-52bc-4c2b-b3c6-09f2649aa11e", "36277788-ca5f-4685-b3a5-8f6cf739d078"]`   

#### Response

```json
  {
    "channel": {
      "channel_url": string,     // channel url string
      "member_count": int,       // count of members who are joined channel
      "name": string             // channel topic
    },
    "last_message": string,      // last message in channel
    "members": [
      0: {
        "guest_id": string,      // user unique id
        "image": string,         // user profile image url
        "name": string           // user nickname
      },
      1: {
        ...
      },
      ...
    ],
    "read_status": {
      0: int,                    // timestamp
      1: int,                    // timestamp
      ...
    },
    "unread_message_count": int  // unread message count
  }
```

 * **other fields**: Internal use only or deprecated 
 

### 2. Invite Users
Invite a certain user to a messaging channel.

``` javascript
  ...
  sendbird.inviteMessaging(
    guestIds,
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

 * **guestIds**: `Guest ID` of the users tobe invited for 1-on-1 messaging.  
 If it's more than just one user, send it as array format. If it's not, you can send it as either array format or string format.  
   - `e.g.) "76f01c7a-52bc-4c2b-b3c6-09f2649aa11e" or or ["76f01c7a-52bc-4c2b-b3c6-09f2649aa11e"] or ["76f01c7a-52bc-4c2b-b3c6-09f2649aa11e", "36277788-ca5f-4685-b3a5-8f6cf739d078"]`  

#### Response

```json
  {
    "channel": {
      "channel_url": string,     // channel url string
      "member_count": int,       // count of members who are joined channel
      "name": string             // channel topic
    },
    "last_message": string,      // last message in channel
    "members": [
      0: {
        "guest_id": string,      // user unique id
        "image": string,         // user profile image url
        "name": string           // user nickname
      },
      1: {
        ...
      },
      ...
    ],
    "read_status": {
      0: int,                    // timestamp
      1: int,                    // timestamp
      ...
    },
    "unread_message_count": int  // unread message count
  }
```

 * **other fields**: Internal use only or deprecated 


### 3. End a Messaging
Leave a 1-on-1 messaging channel or a group message channel.
The user is removed from the channel's member list and the channel no longer shows up on the user's channel list.

```javascript
  ...
  sendbird.endMessaging(
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

 * **url**: `URL` of the 1-on-1 messaging channel to end.
   - `e.g.) sendbird_messaging_520693_be67a4b22c7739c5f0bc44aa8746fca1e6a10596`  

#### Response
 
```json
  {
    "channel": {
      "channel_url": string,     // channel url string
      "member_count": int,       // count of members who are joined channel
      "name": string             // channel topic
    },
    "last_message": string,      // last message in channel
    "members": [
      0: {
        "guest_id": string,      // user unique id
        "image": string,         // user profile image url
        "name": string           // user nickname
      },
      1: {
        ...
      },
      ...
    ],
    "read_status": {
      0: int,                    // timestamp
      1: int,                    // timestamp
      ...
    },
    "unread_message_count": int  // unread message count
  }
```

 * **other fields**: Internal use only or deprecated 
 

### 4. Get Messaging Channel List
Get a list of 1-on-1/group messaging channels.


```javascript
  ...
  var page = 1;
  var limit = 20;
  sendbird.getMessagingChannelList({
    "page": page,
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

 * **page**: Page number. `default : 1`  
 * **limit**: Number of channels to be displayed per page. `default : 9999`  

#### Response
 
```json
  {
    "channels": [
      0: {
        "channel": {
          "channel_url": string,     // channel url string
          "member_count": int,       // count of members who are joined channel
          "name": string             // channel topic
        },
        "last_message": string,      // last message in channel
        "members": [
          0: {
            "guest_id": string,      // user unique id
            "image": string,         // user profile image url
            "name": string           // user nickname
          },
          1: {
            ...
          },
          ...
          ],
          "read_status": {
            0: int,                    // timestamp
            1: int,                    // timestamp
            ...
          },
          "unread_message_count": int  // unread message count
      },
      1: {
        ...
      } ,
      ...
    ],
    "next": int // next page number. if this value is 0, next page are not exist.
    "page": int // current page number
  }
```

 * **other fields**: Internal use only or deprecated 


### 5. Join Messaging Channel
Join a 1-on-1 messaging channel or a group messaging channel an user left in the past.

```javascript
  ...
  sendbird.joinMessagingChannel(
    url,
    {
      "successFunc" : function(data) {
        console.log(data);
        sendbird.connect({
          "successFunc" : function(data) {
            console.log(data);
            // do something
          },
          "errorFunc": function(status, error) {
            console.log(status, error);
            // do something
          }
        });
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

 * **url**: `URL` of the channel to be joined.
   - `e.g.) sendbird_messaging_520693_be67a4b22c7739c5f0bc44aa8746fca1e6a10596`  

#### Response

```json
  {
    "channel": {
      "channel_url": string,     // channel url string
      "member_count": int,       // count of members who are joined channel
      "name": string             // channel topic
    },
    "last_message": string,      // last message in channel
    "members": [
      0: {
        "guest_id": string,      // user unique id
        "image": string,         // user profile image url
        "name": string           // user nickname
      },
      1: {
        ...
      },
      ...
    ],
    "read_status": {
      0: int,                    // timestamp
      1: int,                    // timestamp
      ...
    },
    "unread_message_count": int  // unread message count
  }
```

 * **other fields**: Internal use only or deprecated 


### 6. Messaging read status change to read
When there are unread messages, this function makes message state to be readed.    
```javascript
  ...
  sendbird.markAsRead(url);
  ...
```

 * **url**: `URL` of the channel.
   - `e.g.) sendbird.test_channel_1`  


### 7. Typing Start
Call this function when an user starts typing.  
It notifies a typing-start event to users in the channel. 

```javascript
  ...
  sendbird.typeStart();
  ...
```

### 8. Typing End
Call this function when an user ends typing.  
It notifies a typing-end event to users in the channel. 

```javascript
  ...
  sendbird.typeEnd();
  ...
```

### 9. Check Group Messaging Channel
Check if the type of the messaging channel is group messaging channel.
Return a boolean.

```javascript
  ...
  sendbird.getMessagingChannelList({
    "successFunc": function(data) {
      ...
      var isGroup = sendbird.isGroupMessaging(channel["channel_type"])
      console.log(isGroup);
      ...
    },
    ...
  });
  ...
```

### 10. Get User List
Get a full list of registered users in your app who an user can invite


```javascript
  ...
  sendbird.getUserList({
    "token": token,
    "page": page,
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
  * **token**: If you don't pass a token, we generate new snapshot of users and return new token in a response. As long as you pass the token, you will explore the same snapshot. If you want to get an updated snapshot, then call this method again without the token. Then you will get new token.     `default: ''`  
  * **page**: Page number. `default: 1`   
  * **limit**: Number of users to be displayed per page. `default: 30`  

#### Response
```json
  {
    "token": string,
    "next": number,
    "users": json
  }
```
  * **token**: Token that you should pass to explore the same snapshot.  
  * **next**: Next page number. If this value is 0, current page is the last page.
  * **users**: List of users.   





