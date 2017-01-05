### CS250 Introduction to C Programming<br> Capitol Technology University
--
### Homework 1<br>

#### TCP Client in C

The outcome of this homework will be a functional echo client that connects to the echo-server (provided in this repository). This will require you to properly implement a simple TCP socket, process runtime arguments to the client, and send user input to the server after the network connection is established.

The user will supply the IP address and port to connect to at client runtime.

Be sure to:<br><br>
1. Handle whether the connection is made or not<br>
2. Output status to the user (e.g. connected)<br>
3. Handle replies from the server<br>
4. Teardown the connection properly when existing the client.