### CS250 Introduction to C Programming<br> Capitol Technology University
--
### Homework 4<br>

#### UDP Server in C

The outcome of this homework will be a functional time server that responds to client time queries. This will require you to properly implement a simple UDP socket, process queries from a connected client, execute those commands on the local operating systems, and return results to the client.

Be sure to:<br><br>
1. Bind to any IP Address on port 1337/udp<br>
2. Process queries from the client (you are not required to validate commands) and execute in the operating system. You'll likely need to parse the output so that you only return time to the client<br>
4. Return the results to the client<br>