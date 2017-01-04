### CS250 Introduction to C Programming<br> Capitol Technology University
--
### Lab 8<br>

**Instructions**: Respond to the prompt below in writing and submit to the course portal in Canvas. Written responses are expected to be full, complete statements that exemplify a quality commensurate with collegiate level articulation. See the course syllabus for specific grading criteria.

**Prompt**: Review the code below. What will happen if a response is not received to the initial message this client sends? What could we add to the client so that such a condition is not possible?

	int main(int argc, char **argv) {
	    int sockfd, portno, n;
	    int serverlen;
	    struct sockaddr_in serveraddr;
	    struct hostent *server;
	    char *hostname;
	    char buf[BUFSIZE];
	
	    /* check command line arguments */
	    if (argc != 3) {
	       fprintf(stderr,"usage: %s <hostname> <port>\n", argv[0]);
	       exit(0);
	    }
	    hostname = argv[1];
	    portno = atoi(argv[2]);
	
	    /* socket: create the socket */
	    sockfd = socket(AF_INET, SOCK_DGRAM, 0);
	    if (sockfd < 0) 
	        error("ERROR opening socket");
	
	    /* gethostbyname: get the server's DNS entry */
	    server = gethostbyname(hostname);
	    if (server == NULL) {
	        fprintf(stderr,"ERROR, no such host as %s\n", hostname);
	        exit(0);
	    }
	
	    /* build the server's Internet address */
	    bzero((char *) &serveraddr, sizeof(serveraddr));
	    serveraddr.sin_family = AF_INET;
	    bcopy((char *)server->h_addr, 
		  (char *)&serveraddr.sin_addr.s_addr, server->h_length);
	    serveraddr.sin_port = htons(portno);
	
	    /* get a message from the user */
	    bzero(buf, BUFSIZE);
	    printf("Please enter msg: ");
	    fgets(buf, BUFSIZE, stdin);
	
	    /* send the message to the server */
	    serverlen = sizeof(serveraddr);
	    n = sendto(sockfd, buf, strlen(buf), 0, &serveraddr, serverlen);
	    if (n < 0) 
	      error("ERROR in sendto");
	    
	    /* print the server's reply */
	    n = recvfrom(sockfd, buf, strlen(buf), 0, &serveraddr, &serverlen);
	    if (n < 0) 
	      error("ERROR in recvfrom");
	    printf("Echo from server: %s", buf);
	    return 0;
	}