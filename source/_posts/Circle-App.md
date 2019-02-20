---
title: Circle App
date: 2019-02-19 12:24:19
tags:
---
An andriod App for CS446's project (2017/4 - 2017/8)
Applink: https://446daydayup.github.io/
Github: https://github.com/446DayDayUp/CircleApp

![Logo](Logo.png)
Our project is to build an app that allows users to meet and chat with people near them. The app allows user to create chat rooms with tags. Other users are able to search and enter those chat rooms based on name or tags. Within a chat room, users can interact with other uses by sending text messages, voice messages, pictures, current location, or start a game with other people in the chat room.

The app allows users to chat with strangers and make friends.
The app allows users to find interesting chat rooms by tags.
All chat rooms are created based on location. Only nearby users are able to enter the room.
All users are totally anonymous to each other.

## <font color="#0D2989"> ** Functional Properties ** </font>
Users are able to log in with a username and profile picture.
Users can create chat room with a name, optional tags, and range specifying the visible range of this chat room.
Users can view nearby chat rooms, join visible chat rooms, and quit joined chat rooms.
Users can search chat rooms based on name and tags.
Users are allowed to send different types of messages including text, location, image, voice and possibly video message.
Users can play mini games in the chat room and share their score with others.
User can blacklist other users and their message will no longer be displayed.

## <font color="#0D2989"> ** Non Functional Properties ** </font>
Circle handles unexpected input. Our app will detect invalid input and alert users.
Circle is able to run on Android phones with version higher than 5.0.
Circle is able to display reasonable amount of messages sent by users in a chat room within 500 ms under stable Internet connectivity.
Circle does not contain user information so it will never reveal user privacy.

## <font color="#0D2989"> ** UML ** </font>

![UML](UML.png)

## <font color="#0D2989"> ** Architecture ** </font>
### Client Server Architecture
Vision, Goal and Objective: We need a server to process client request such as joining chat room, search nearby chat rooms and send messages to other clients. 
**Implementation:** Client program is an android app built with React-Native and server program is built in Node and Express and it is deployed on Heroku. HTTP request and web socket are used to communicate between client and server.  The client makes HTTP Get request to query nearby chat rooms. The client makes HTTP Post request to create a chat room. The client and server establish a socket connection to send messages among clients.
### Event Driven Architecture
Vision, Goal and Objective: Clients need to receive messages from other clients. A event driven architecture is employed to achieve this.
**Implementation:** Both server and client uses a websocket and have multiple event listeners listening on this socket. When chat messages are received on client side. The message have different types such as notification, text message, audio message and video message. The client will enqueue this message object in a message queue and display it in the chat room page.



## <font color="#0D2989"> **Design Patterns** </font>
#### State Design Pattern
**Use:** state design pattern is used in all major components because React framework uses state to check if it is necessary to re-render a component.
#### Balking
**Use:** We use balking design pattern in the chat room bottom bar and the search chat room condition in the main page.
**Implementation**: In the chat room page, there is a bottom bar component. Extra buttons such as send image button, game button will be displayed only if the user pressed an expand button. A state is used to check if the user have pressed the expand button and to render different views.
In the main page, the scrolling search condition is shown only when user has started a search. 
#### Publish-subscribe Pattern
**Use:** We use publish-subscribe design pattern to receive messages from a joined chat room. Client's socket sends a request to join and subscribes to the chat room by chat room id. Later, when the chat room receives some messages, client will be notified.
**Implementation:** When user click the join button of a chat room, the client will send a enter-chat-room message to server through its socket. The server than subscribe this socket to the chat room by chat room id. When other users send messages in the chat room. The server will publish the message to all users who subscribed on the chat room id.
#### Factory Pattern
**Use:** We use factory design pattern to create different messages components in a chat room. 
**Implementation:** A superclass Message and its derived classes such as textMessage, audioMessage and imageMessage are implemented. Their creation and render logic is not exposed to client and a common interface is used to create different type of message and they have different render methods.
#### One Way Direction Data Flow
**Use:** We have a main page component that makes HTTP requests to server to fetch a list of all nearby chat rooms. Then the chat room information is passed down the component hierarchy from main page to chat room list and chat room panel.
**Implementation:** Messages are passed as properties from parent component to child components down the component hierarchy.
#### Singleton Pattern
**Use:** In chat room, we want to make sure there is only one audio player exists and no multiple audio will be played simultaneously.
**Implementation:** While rendering messages in a chat room, AudioPlayer is implemented as a singleton object to play audio messages. When the audio player exists, it returns the existing audio player object. 



