SendBird JavaScript SDK Function: Open Chat
=================================

Function references to implement Open Chat.
Open Chat is suitable for public chat rooms to host thousands of users in a single channel.  
ex) twitch-like chat rooms, interest-based communities, game lobbies, clan/guild chats, etc.

 * Note: Users can also browse the list of available open channels that they are not yet part of.  

### Download and Install 
All of the functions are included in `SendBird JavaScript SDK`. No additional files or installations are required.


### 1. Join Channel
Join a channel.

```javascript
  ...
  sendbird.joinChannel(
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

 * **url**: `URL` of the channel to join.
   - `e.g.) sendbird.test_channel_1`  


#### Response

```json
  {
    "channel_url": string,   // channel url string
    "cover_img_url": string, // channel cover image url
    "member_count": int,     // count of members who are joined channel
    "name": string           // channel topic
  }
```

 * **other fields**: Internal use only or deprecated 
 

### 2. Leave Channel
Leave a channel.  
The user is removed from the member list of the channel.
 ( This does not move an user to a different channel automatically.)

```javascript
  ...
  sendbird.leaveChannel(
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

 * **url**: `URL` of the channel to leave.
   - `e.g.) sendbird.test_channel_1`  
 

#### Response

```json
  {
    "channel_url": string,  // channel url string
    "member_count": int,    // count of members who are joined channel
    "name": string          // channel topic
  }
```

 * **other fields**: Internal use only or deprecated 
 

### 3. Send Message
Send a text message.

```javascript
  ...
  sendbird.message(msg);
  ...
```

 * **msg**: Message to be sent.


### 4. Get Channel List
Get a list of Open Chat channels.

```javascript
  ...
  var page = 1;
  var limit = 20;
  sendbird.getChannelList({
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

 * **page**: Page number. `default: 1`
 * **limit**: Number of channels to be displayed per page. `default: 20`  
 

#### Response

```json
  {
    "channels": [
      0: {
        "channel_url": string,  // channel url string
        "member_count": int,    // count of members who are joined channel
        "name": string          // channel topic
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


### 5. Search Channel
Search for channels by a text query on channel names

```javascript
  ...
  var page = 1;
  var limit = 20;
  sendbird.getChannelSearch({
    "page": page,
    "limit": limit,
    "query": query,
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

* **query**: Search keyword.
* **page**: Page number. `default: 1`
* **limit**: Number of channels to be displayed per page. `default: 20`  
 

#### Response

```json
  {
    "channels": [
      0: {
        "channel_url": string,  // channel url string
        "member_count": int,    // count of members who are joined channel
        "name": string          // channel topic
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


