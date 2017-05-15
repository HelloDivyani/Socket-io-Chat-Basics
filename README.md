Android Chat Application Using Sockets
Socket is an internal endpoint in the single node for sending and receiving data in computer network.

3 Components :
1.Socket Server -  handling Socket client connections and sending messages between clients.
2.Web App  - Join the chat conversation from the browser.
3.Android App
(web-web) (web-android) (android-android)

J2EE =  Java platform independent Java-centric environment from Sun for developing,
building and deploying Web-based enterprise applications online.

J2EE -  Java Platform Enterprise Edition

It is collection of Java APIs owned by Oracle that software developer use to build server side application

Apache Tomcat is used to deploy Java Servlets and JSPs

Socket.io  native implementation in android studio
Creating First Socket chat application


Express is flexible node.js application
Require JS is the module script loader improves the quality and speed of the code


Sockets provide bidirectional communication channel between a client and a server.
This means that the server can push messages to clients.
Whenever you write a chat message, the idea is that the server will get it and push it to all other connected clients.


package.json  manifest file describes our project




var app = require('express')();
var http = require('http').Server(app);

app.get('/', function(req, res){
  res.send('<h1>Hello world</h1>');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});




This translates into the following:

* Express initializes app to be a function handler that you can supply to an HTTP server
* We define a route handler / that gets called when we hit our website home.
* We make the http server listen on port 3000.

Integrating Socket IO:
Socket.IO is composed of two parts:

A server that integrates with (or mounts on) the Node.JS HTTP Server: socket.io
A client library that loads on the browser side: socket.io-client



var io = require('socket.io')(http);
By this we initialize the new instance of socket.io by passing the http server object
Then I listen on the connection event for incoming sockets, and I log it to the console.


<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
</script>


That all it takes for the socket.io-client to load and exposes io global and connect
Notice that I’m not specifying any URL when I call io(), since it defaults to trying to connect to the host that serves the page.

If you now reload the server and the website you should see the console print “a user connected”.

Run the js file through the node and host the html file as a response to a request in the js.

Emitting Events :
The main idea behind Socket.IO is that you can send and receive any events you want, with any data you want.
Any objects that can be encoded as JSON will do, and binary data is supported too.

BroadCasting :
The next goal is for us to emit the event from the server to the rest of the users.
Inorder to send Event to everyone use io.emit()
io.emit('some event', { for: 'everyone' });

If you want to send a message to everyone except for a certain socket, we have the broadcast flag:
io.on('connection', function(socket){
  socket.broadcast.emit('hi');
});


Client Side Capture the chat Message and Include it in the Page
