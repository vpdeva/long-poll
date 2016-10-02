# long-poll
Push Data with Long Polling using Node.js, Socket.io and MySQL

You need to push data from your server without the client asking for it, in order to display real time data without a page refresh. One limitation to do this with polling is, your clients have to bash the server with short pauses, asking for a value continuously, however there is an approach around it, by waiting until there really is an update on the database before the server pushes the data to the clients. This approach is called long polling, and it is the way big names like facebook pushes notifications, as well as Gmail displaying new emails without page refreshes etc. In this post, I will keep the text short for you to dig into code straight away.

# Server side

The following code is for server.js, our vanilla Node.JS server which allows us to poll the database every second (see POLLING_INTERVAL variable) and only push the response if it is different than previous response. Later on we will see client.html to display the client side of socket.io code we need to push the notification from server.

In this particular example, the business logic is simplified to only display the count of notifications we have from our mysql table, called activity_log, which displays activities taken part on our site by the user, uniquely identified with profile_id column. Obviously, one prerequisite for this to work is to have this table created in your MySql database, with the same columns (notified, profile_id) and values (both columns are int).

# Client side 

On the client side (see client.html file below), instead of pulling the new data via AJAX, we make use of socket.io to listen to notifications emitted by the server and display the response data in a div. This is enabled by web sockets (socket.io library in this case) and it's a great way to display real-time data on our single page applications.

As stated earlier, if you notice the line where there's a querystring variable called profile_id being sent, this is retrieved via socket.handshake.query.profile_id on server side, via our socket.

# TLDR: Install nodejs and mysql (and make a db/table as the mysql statement above requires) copy and paste above server (server.js, with mysql and socket.io package dependencies) and client (client.html) codes to experiment with a working prototype of long polling push notifications.
