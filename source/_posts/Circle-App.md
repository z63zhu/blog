---
title: Circle App
date: 2019-02-19 12:24:19
tags:
---
An andriod App for CS446's project (2017/4 - 2017/8)
Github: https://github.com/446DayDayUp/CircleApp

## An Overview of software architecture and language used
	Client side mobile app is built in React-Native with JavaScript which is component-based framework and it makes building hybrid mobile app easier. Because limitation of JavaScript and React-Native framework, some native modules are implemented with Java.
	Server is built in Node.js with Javascript which is an event-driven, non-blocking back-end framework to process HTTP request, establish socket and communicate with Mongo Database and Google Cloud Storage.


## Functions
### Login
	1.Select profile picture
		The users are able to pick profile picture from a given set of icons.
	2.Enter username
		The users can set  their user name. 
		A username must be provided and it cannot be empty.
### Manage User Profile
	1.After login, user can change their usernames and profile picture.
### Create Chat Rooms
	1.To create
		User can push the “+” button to create a chat room.
	2.Chat room name
		User must set a chat room name.
		Chat room name cannot be empty.
	3.Chat room visible range
		User can set the visible range of the chat room.
		User can choose the range from 50m, 100m, 500m, 1km, 5km and 10km.
		The default range is 1km.
	4.Chat room tags
		User can select one or more tags from a given set of tags.
### View Nearby Chat Rooms
	1.A list of nearby chat rooms is displayed to the user.
	2.Chat room name, number of users in the chat room, distance to the chat room from your current location and room tags are displayed.
	3.User can join chat rooms in the list.
	4.User can quit a joined chat room.
### Chat In Joined Chat Rooms
	1.User can enter a joined chat room.
	2.User can send and receive messages in current chat room.
	3.User can temporarily leave a joined chat room and user can still receive messages from the chat room.
### Search Chat Rooms
	1.User can search chat rooms in both joined chat room page and nearby chat room page.
	2.User can filter displayed chat rooms based on name, range, and/or tags.


## UML

![UML](/source/image/UML.png)


