---
title: Circle App
date: 2019-02-19 12:24:19
tags:
---
An andriod App for CS446's project (2017/4 - 2017/8)
Github: https://github.com/446DayDayUp/CircleApp

![Logo](Logo.png)
## An Overview of software architecture and language used
Client side mobile app is built in React-Native with JavaScript which is component-based framework and it makes building hybrid mobile app easier. Because limitation of **JavaScript** and **React-Native** framework, some native modules are implemented with Java.
	Server is built in Node.js with Javascript which is an event-driven, non-blocking back-end framework to process HTTP request, establish socket and communicate with **Mongo Database** and **Google Cloud Storage**.



## <font color="#0D2989"> ** Functions ** </font>
1. Login
2. Manage User Profile
3. Create Chat Rooms
4. View Nearby Chat Rooms
5. Chat In Joined Chat Rooms
6. send voice massages, play small games, share current location
7. Search Chat Rooms by Tags


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



