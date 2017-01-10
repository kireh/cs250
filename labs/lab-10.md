### CS250 Introduction to C Programming<br> Capitol Technology University
--
### Lab 10<br>

**Instructions**: Respond to the prompt below in writing and submit to the course portal in Canvas. Written responses are expected to be full, complete statements that exemplify a quality commensurate with collegiate level articulation. See the course syllabus for specific grading criteria.

**Prompt**: By default, our servers handle one connection at a time. Subsequent clients can connect and send messages but will not receive a repsonse. There are three types of concurrent servers - what are the names? Review the code below and describe which type of concurrent server is present.

	int main()
	{
	 int sockfd;//to create socket
	 int newsockfd;//to accept connection
	
	 struct sockaddr_in serverAddress;//server receive on this address
	 struct sockaddr_in clientAddress;//server sends to client on this address
	
	 int n;
	 char msg[MAXSZ];
	 int clientAddressLength;
	 int pid;
	
	 sockfd=socket(AF_INET,SOCK_STREAM,0);
	 memset(&serverAddress,0,sizeof(serverAddress));
	 serverAddress.sin_family=AF_INET;
	 serverAddress.sin_addr.s_addr=htonl(INADDR_ANY);
	 serverAddress.sin_port=htons(PORT);
	
	 bind(sockfd,(struct sockaddr *)&serverAddress, sizeof(serverAddress));
	
	 listen(sockfd,5);
	
	 while(1)
	 {
	  printf("\n*****server waiting for new client connection:*****\n");
	  clientAddressLength=sizeof(clientAddress);
	  newsockfd=accept(sockfd,(struct sockaddr*)&clientAddress,&clientAddressLength);
	  printf("connected to client: %s\n",inet_ntoa(clientAddress.sin_addr));
	
	  pid=fork();
	  if(pid==0)//child process rec and send
	  {
	   while(1)
	   {
	    n=recv(newsockfd,msg,MAXSZ,0);
	    if(n==0)
	    {
	     close(newsockfd);
	     break;
	    }
	    msg[n]=0;
	    send(newsockfd,msg,n,0);
	
	    printf("Receive and set:%s\n",msg);
	   }
	  exit(0);
	  }
	  else
	  {
	   close(newsockfd);
	  }
	 }
	
	 return 0;
	}