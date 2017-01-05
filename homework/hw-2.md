### CS250 Introduction to C Programming<br> Capitol Technology University
--
### Homework 2<br>

#### TCP Server in C

The outcome of this homework will be a functional telnet server that accepts connections from the standard telnet client available in popular operating systems. This will require you to properly implement a simple TCP socket, process commands from a connected client, execute those commands on the local operating systems, and return results to the client.

Be sure to:<br><br>
1. Bind to any IP Address on port 23/tcp<br>
2. Handle whether the connection is made or not<br>
3. Process input from the client (you are not required to validate commands) and execute in the operating system<br>
4. Return the results to the client<br>
5. Teardown the connection properly when the client disconnects