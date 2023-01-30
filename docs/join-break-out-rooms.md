---
title: "Join a Break Out Room"
date: 
description:
type: "docs"
weight: 2
---
The *EnxRoom.joinBreakOutRoom()* method allows users to join a Break-Out room on being invited by the creator. A user can join a Break-Out Room from the Parent Room only and can join only one Break-Out Room at a time, thus allowing the user to join another Break-Out Room only after rejoining the Parent Room first.

**Method**: *EnxRoom.joinBreakOutRoom(Joinee, streamInfo, Callback);*

**Parameters**:

- *Joinee* – JSON Object with details required to join the Break-Out Room.
    - *role* – String. Required. Enumerated Values: participant, moderator.
    - *room_id* – String. Required. Room-ID of the Break-Out Room being joined.
- *streamInfo* – JSON Object with Stream information while joining the Break-Out Room.
    - *audio* – Boolean. Set to true to join with Audio.
    - *video* – Boolean. Set to true to join with Video. This is currently not supported.
    - *screen* – Boolean. Set to true for screen sharing capability.
    - *canvas* – Boolen. Set to true for canvas streaming capability.
- *Callback* – To know result of the join Room call.

**Event Listeners**

- *breakout-room-error* – Notification to the Joiner on failure to join the Break-Out Room.
- *breakout-room-connected* – Acknowledgment to the Joiner when Break-Out Room joined successfully.
- *user-joined-breakout-room* – Notification to everyone in the Break-Out Room when a new user joins the Room.
```
Joinee = {
	"role" : "participant", 
	"room_id" : "RoomID"
};

StreamInfo = {
	"audio": true, 
	"video" : false,
	"canvas" : false,
	"screen" : false
};

room.joinBreakOutRoom(Joinee, StreamInfo, function(resp) {
	// Status 
});

// User gets connected to Break-Out Room 
room.addEventListener("breakout-room-connected", function (roomMeta) {
	// roomMetadata contains meta information of the Room 
});

// User fails to connect  to Break-Out Room 
room.addEventListener("breakout-room-error", function (result) {
	// result contains reasons of failed connection, e.g.
	/*
	{	"result": 1729,
		"msg": "Failed to generate Token"
	}
	*/
});

// Others are notified about the new joinee in Break-Out Room 
room.addEventListener("user-joined-breakout-room", function (result) {
	// result contains new joinee user's information 
	/*
	{	"clientId": "String",
		"room": "String";
	}
	*/
});
```