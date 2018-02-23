# LearningWebSockets
CS324
--------------------------------------------------
1. Setup
 
1a. Download hw5.tar.gz and un-tar/gzip it to a directory.
 
1b. Run "make" to build two executables: client and server.
 
2. client.c
 
2a. What two system calls are required to create and prepare a client socket for use?

	socket() and connect()
 
2b. Start a netcat ("nc" command) server listening for incoming UDP datagrams on a port of your choosing (but should be above 1023).  Show the command line you used.

	nc -ul 1234 &

2c. Use the netstat command to show only the services *listening* on UDP ports.  Also, have it display the PIDs/command names for the services for which you are the owner.  Finally, use the "-n" option to have it show addresses instead of names.  Show the command line you used and its output (Hint: your nc service should show up in the list. Hint 2: you should not be piping your output to grep or any other program--this can/should be done using only command-line options for netstat.  See the man page for these options).
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -ulp
	(Not all processes could be identified, non-owned process info
	 will not be shown, you would have to be root to see it all.)
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	udp        0      0 *:54647                 *:*                                 -               
	udp        0      0 alex-Mint:domain        *:*                                 -               
	udp        0      0 *:bootpc                *:*                                 -               
	udp        0      0 10.0.2.15:ntp           *:*                                 -               
	udp        0      0 localhost:ntp           *:*                                 -               
	udp        0      0 *:ntp                   *:*                                 -               
	udp        0      0 *:1234                  *:*                                 16120/nc        
	udp        0      0 *:43734                 *:*                                 -               
	udp        0      0 *:mdns                  *:*                                 -               
	udp6       0      0 fe80::b0e3:6f59:a7e:ntp [::]:*                              -               
	udp6       0      0 ip6-localhost:ntp       [::]:*                              -               
	udp6       0      0 [::]:ntp                [::]:*                              -               
	udp6       0      0 [::]:42511              [::]:*                              -               
	udp6       0      0 [::]:mdns               [::]:*                              -

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -ulpn
	(Not all processes could be identified, non-owned process info
	 will not be shown, you would have to be root to see it all.)
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	udp        0      0 0.0.0.0:54647           0.0.0.0:*                           -               
	udp        0      0 127.0.1.1:53            0.0.0.0:*                           -               
	udp        0      0 0.0.0.0:68              0.0.0.0:*                           -               
	udp        0      0 10.0.2.15:123           0.0.0.0:*                           -               
	udp        0      0 127.0.0.1:123           0.0.0.0:*                           -               
	udp        0      0 0.0.0.0:123             0.0.0.0:*                           -               
	udp        0      0 0.0.0.0:1234            0.0.0.0:*                           16120/nc        
	udp        0      0 0.0.0.0:43734           0.0.0.0:*                           -               
	udp        0      0 0.0.0.0:5353            0.0.0.0:*                           -               
	udp6       0      0 fe80::b0e3:6f59:a7e:123 :::*                                -               
	udp6       0      0 ::1:123                 :::*                                -               
	udp6       0      0 :::123                  :::*                                -               
	udp6       0      0 :::42511                :::*                                -               
	udp6       0      0 :::5353                 :::*                                -

2d. Modify client.c such that: 1) it sleeps for 2 seconds immediately before writing each argument to the the socket that has been established; and 2) it does not attempt to read from the socket--or print what it read--after writing to to the socket.  For #2, comment out the appropriate code rather than removing it (you'll want to use it later).  Re-make to compile the changes.  Determine the SHA1 sum of the newly compiled binary file (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.

	
 
2e. While the netcat server is still running, execute the client program in a different window, such that it sends the following strings, separately, to the netcat server via a UDP socket: foo, bar, baz, and catvideo.  Show: 1) the command-line you used to run the client program; and 2) the console output from the netcat server (not the client).
 
2f.  While the client program is running (you might need to restart the server and client, if your run from 2e already finished), run netstat in a separate window to show only non-listening UDP "connections" (even though UDP is connectionless, sometimes "connection" is still used to describe client-server UDP communications).  Again, use the "-n" option to show addresses instead of names.  Show the command line you used and its output (Hint: your nc "connection" should show up in the list).
 
2g. When the client program has finished running, interrupt the netcat server also, so that it is no longer running.  Now repeat the netstat command from 2f.  Show the command line you used and its output.
 
 
3. client.c - TCP
 
3a. Modify client.c, such that TCP is used instead of UDP.  Determine the SHA1 sum of the newly compiled binary file (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.
 
3b. Start a netcat ("nc" command) server listening for incoming TCP datagrams on a port of your choosing (but should be above 1023).  Show the command line you used.
 
3c. Use the netstat command to show only the services *listening* on TCP ports.  Also, have it display the PIDs/command names for the services for which you are the owner.  Finally, use the "-n" option to have it show addresses instead of names.  Show the command line you used and its output (Hint: your nc service should show up in the list. Hint 2: you should not be piping your output to grep or any other program--this can/should be done using only command-line options for netstat.  See the man page for these options).
 
3d. While the netcat server is still running, execute the client program in a different window, such that it sends the following strings, separately, to the netcat server via a TCP socket: foo, bar, baz, and catvideo.  Show: 1) the command-line you used to run the client program; and 2) the console output from the netcat server (not the client).
 
3e.  While the client program is running (you might need to restart the server and client, if your run from 3d already finished), run netstat in a separate window to show only non-listening TCP connections.  Again, use the "-n" option to show addresses instead of names.  Show the command line you used and its output (Hint: your nc connection should show up in the list).
 
3f. When the client program has finished running, interrupt the netcat server also, so that it is no longer running.  Now repeat the netstat command from 3e.  Show the command line you used and its output.
 
 
4. server.c - TCP
 
4a. Modify server.c such that the server socket communicates over TCP instead of UDP: 1) prior to the second "for" loop (i.e., "for (;;)"), use the listen() function on the TCP server socket (you can use a backlog value of 100); 2) immediately after the call to listen(), use the accept() function to wait for a client to connect and create/return a new client socket (note that you can re-use some of the arguments from recvfrom() below); 3) change the recvfrom() call to recv() (note that you just need to remove some of the arguments); and 4) break out of the loop if recv() returns 0 bytes.  Re-make.  Determine the SHA1 sum of the newly compiled binary file for the server (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.
 
4b. Run the server program to listen on a port of your choosing (but should be above 1023).  While the server program is running, execute the client program in a different window, such that it sends the following strings, separately, to the server program via a TCP socket: foo, bar, baz, and catvideo.  Show: 1) the command-line you used to run the server program; and 2) the command-line you used to run the client program, and the output from the client (not the server).
 
[Please note: because you commented out the read/print portion of the client code, there will be no output to the console (nor reading from the socket) for problem 4b.  This outcome wasn't necessarily intentional, but it needs to stay this way because if you uncomment the code from 2d now, it will affect later homework problems.]
 
4c. Why is there a difference between handling of "connections" at the server with TCP and with UDP?
 
 
5. Client modification
 
5a. Modify client.c such that *instead* of looping through each command-line argument and writing it to the socket, it does the following, *after* the socket connection is established:
1) reads (using fread()) input from stdin into a buffer (char []) until EOF is reached (max total bytes 4096).
2) After *all* data has been read from stdin (i.e., EOF has been reached), loop to send the data in the buffer until it has all been sent.  Note that write() will return the number of bytes actually sent, which might be less than the number you requested to be sent (see the man page for more!), so you need to loop to ensure that all has been sent.  This is important not only for this lab but for future labs.
Determine the SHA1 sum of the newly compiled binary file (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.
 
5b. Start a netcat ("nc" command) server listening for incoming TCP connections on a port of your choosing, and such that its output is piped to the sha1sum command.   Then test your client program by redirecting the contents of alpha.txt (from the tar file) to the program's standard input (using input redirection on the shell).  Show: 1) the pipeline you used to run nc, and its output (after the client finished executing); and 2) the command line you used to run the client program.  The output of the nc pipeline should equal the following: 0ef39a3f241cdd6552ad131e01afa9171b3dab8d
 
5c. Modify client.c, such that after all the data read from stdin has been sent to the socket, the server reads from the socket and prints it out to stdout (you should be able to use the code you commented out in 2d).  Then execute your your client program such that 1) you are sending data to the standard HTTP port at www.sandia.gov;  and that 2) you are redirecting the contents of file-http.txt (from the tar file) to the program's standard input (using input redirection on the shell).  Show the command line you used to run the client program and its output.  Note that it should result in an HTTP/1.1 200 OK response.
 
Submission
Please include 1) the final modified source code for client.c and server.c, and 2) the output/writeup from requested from each of the numbered items above, in a single file
