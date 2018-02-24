# LearningWebSockets
CS324
--------------------------------------------------

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

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ sha1sum -b client
	992fd6bd959935f26ffa47bea0b112ba50405197 *client
 
2e. While the netcat server is still running, execute the client program in a different window, such that it sends the following strings, separately, to the netcat server via a UDP socket: foo, bar, baz, and catvideo.  Show: 1) the command-line you used to run the client program; and 2) the console output from the netcat server (not the client).

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ ./client localhost 1234 foo bar baz catvideo

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ foobarbazcatvideo
 
2f.  While the client program is running (you might need to restart the server and client, if your run from 2e already finished), run netstat in a separate window to show only non-listening UDP "connections" (even though UDP is connectionless, sometimes "connection" is still used to describe client-server UDP communications).  Again, use the "-n" option to show addresses instead of names.  Show the command line you used and its output (Hint: your nc "connection" should show up in the list).

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -upn
	(Not all processes could be identified, non-owned process info
	will not be shown, you would have to be root to see it all.)
	Active Internet connections (w/o servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	udp        0      0 127.0.0.1:55848         127.0.0.1:1234          ESTABLISHED 26657/client    
	udp        0      0 127.0.0.1:1234          127.0.0.1:55848         ESTABLISHED 26648/nc

2g. When the client program has finished running, interrupt the netcat server also, so that it is no longer running.  Now repeat the netstat command from 2f.  Show the command line you used and its output.

	----I'm not sure if you want me to pause or terminate the process, since both SIGSTP and SIGINT interrupt the flow of the program and make it stop running. I'll put the output from the job stopped first and then when it is terminated.

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -upn
	(Not all processes could be identified, non-owned process info
	will not be shown, you would have to be root to see it all.)
	Active Internet connections (w/o servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	udp        0      0 127.0.0.1:1234          127.0.0.1:55848         ESTABLISHED 26648/nc

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -upn
	(Not all processes could be identified, non-owned process info
	will not be shown, you would have to be root to see it all.)
	Active Internet connections (w/o servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name

3. client.c - TCP
 
3a. Modify client.c, such that TCP is used instead of UDP.  Determine the SHA1 sum of the newly compiled binary file (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ sha1sum -b client
	374d0b70843610cd78bc48cf6c5605d60c9500c8 *client

3b. Start a netcat ("nc" command) server listening for incoming TCP datagrams on a port of your choosing (but should be above 1023).  Show the command line you used.
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ nc -l 1234

3c. Use the netstat command to show only the services *listening* on TCP ports.  Also, have it display the PIDs/command names for the services for which you are the owner.  Finally, use the "-n" option to have it show addresses instead of names.  Show the command line you used and its output (Hint: your nc service should show up in the list. Hint 2: you should not be piping your output to grep or any other program--this can/should be done using only command-line options for netstat.  See the man page for these options).
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -tlpn
	(Not all processes could be identified, non-owned process info
	will not be shown, you would have to be root to see it all.)
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 0.0.0.0:1234            0.0.0.0:*               LISTEN      29127/nc        
	tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN      -               
	tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      -               
	tcp6       0      0 :::80                   :::*                    LISTEN      -               
	tcp6       0      0 ::1:631                 :::*                    LISTEN      -

3d. While the netcat server is still running, execute the client program in a different window, such that it sends the following strings, separately, to the netcat server via a TCP socket: foo, bar, baz, and catvideo.  Show: 1) the command-line you used to run the client program; and 2) the console output from the netcat server (not the client).
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ ./client localhost 1234 foo bar baz catvideo &
	
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ foobarbazcatvideo

3e.  While the client program is running (you might need to restart the server and client, if your run from 3d already finished), run netstat in a separate window to show only non-listening TCP connections.  Again, use the "-n" option to show addresses instead of names.  Show the command line you used and its output (Hint: your nc connection should show up in the list).
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -tpn
	(Not all processes could be identified, non-owned process info
	will not be shown, you would have to be root to see it all.)
	Active Internet connections (w/o servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 10.0.2.15:48290         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55776         54.225.64.197:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55778         54.225.64.197:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45374         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:36138         72.21.91.29:80          CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:46764         23.23.199.103:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48262         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:51244         54.221.212.171:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55360         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:51236         54.221.212.171:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 127.0.0.1:38680         127.0.0.1:1234          ESTABLISHED 31063/client    
	tcp        0      0 10.0.2.15:55408         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:38168         178.62.110.224:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55452         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55500         50.17.199.74:443        CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55406         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45368         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48286         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:39072         23.23.74.204:443        CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45372         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:38170         178.62.110.224:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48292         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55488         50.17.199.74:443        CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55358         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 127.0.0.1:1234          127.0.0.1:38680         ESTABLISHED 31024/nc        
	tcp        1      0 10.0.2.15:48282         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:48280         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55454         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp       32      0 10.0.2.15:55404         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45370         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp       32      0 10.0.2.15:55432         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55436         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55356         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:46766         23.23.199.103:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55456         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48288         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48914         184.73.188.164:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55434         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:36998         54.186.123.227:443      ESTABLISHED 28418/firefox   
	tcp        1      0 10.0.2.15:55376         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-

3f. When the client program has finished running, interrupt the netcat server also, so that it is no longer running.  Now repeat the netstat command from 3e.  Show the command line you used and its output.
 
	----I'm not sure if you want me to pause or terminate the process, since both SIGSTP and SIGINT interrupt the flow of the program and make it stop running. I'll put the output from the job stopped first and then when it is terminated.

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -tpn
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 10.0.2.15:48290         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55776         54.225.64.197:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55778         54.225.64.197:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45374         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:36138         72.21.91.29:80          CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:46764         23.23.199.103:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48262         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:51244         54.221.212.171:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55360         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:51236         54.221.212.171:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55408         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:38168         178.62.110.224:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55452         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55500         50.17.199.74:443        CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55406         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45368         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48286         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:39072         23.23.74.204:443        CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45372         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:38170         178.62.110.224:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48292         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55488         50.17.199.74:443        CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55358         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:48282         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:48280         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55454         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp       32      0 10.0.2.15:55404         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45370         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp       32      0 10.0.2.15:55432         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55436         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55356         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:46766         23.23.199.103:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55456         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48288         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48914         184.73.188.164:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55434         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:36998         54.186.123.227:443      ESTABLISHED 28418/firefox   
	tcp        1      0 10.0.2.15:55376         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ netstat -tpn
	(Not all processes could be identified, non-owned process info
	will not be shown, you would have to be root to see it all.)
	Active Internet connections (w/o servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
	tcp        0      0 10.0.2.15:48290         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55776         54.225.64.197:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55778         54.225.64.197:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45374         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:36138         72.21.91.29:80          CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:46764         23.23.199.103:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48262         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:51244         54.221.212.171:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55360         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:51236         54.221.212.171:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55408         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:38168         178.62.110.224:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55452         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55500         50.17.199.74:443        CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55406         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45368         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48286         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:39072         23.23.74.204:443        CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45372         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:38170         178.62.110.224:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48292         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55488         50.17.199.74:443        CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:55358         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:48282         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:48280         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55454         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp       32      0 10.0.2.15:55404         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:45370         96.126.102.55:443       CLOSE_WAIT  20786/code --unity-
	tcp       32      0 10.0.2.15:55432         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55436         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55356         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        1      0 10.0.2.15:46766         23.23.199.103:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55456         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48288         151.101.40.133:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:48914         184.73.188.164:443      CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:55434         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-
	tcp        0      0 10.0.2.15:36998         54.186.123.227:443      ESTABLISHED 28418/firefox   
	tcp        1      0 10.0.2.15:55376         50.17.211.206:443       CLOSE_WAIT  20786/code --unity-

4. server.c - TCP
 
4a. Modify server.c such that the server socket communicates over TCP instead of UDP: 1) prior to the second "for" loop (i.e., "for (;;)"), use the listen() function on the TCP server socket (you can use a backlog value of 100); 2) immediately after the call to listen(), use the accept() function to wait for a client to connect and create/return a new client socket (note that you can re-use some of the arguments from recvfrom() below); 3) change the recvfrom() call to recv() (note that you just need to remove some of the arguments); and 4) break out of the loop if recv() returns 0 bytes.  Re-make.  Determine the SHA1 sum of the newly compiled binary file for the server (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ sha1sum -b server
	2d67dbf6e30264ba2a27bf0aa9ef55d338f7bd12 *server

4b. Run the server program to listen on a port of your choosing (but should be above 1023).  While the server program is running, execute the client program in a different window, such that it sends the following strings, separately, to the server program via a TCP socket: foo, bar, baz, and catvideo.  Show: 1) the command-line you used to run the server program; and 2) the command-line you used to run the client program, and the output from the client (not the server).
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ ./server 1234

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ ./client localhost 1234 foo bar baz catvideo

[Please note: because you commented out the read/print portion of the client code, there will be no output to the console (nor reading from the socket) for problem 4b.  This outcome wasn't necessarily intentional, but it needs to stay this way because if you uncomment the code from 2d now, it will affect later homework problems.]
 
4c. Why is there a difference between handling of "connections" at the server with TCP and with UDP?
 
	UDP basically sends datagrams and you just kind of hope that they all arrive properly, whereas TCP connects the two endpoints with a bytestream and remains connected continuously via this stream until the transmission is complete.
 
5. Client modification
 
5a. Modify client.c such that *instead* of looping through each command-line argument and writing it to the socket, it does the following, *after* the socket connection is established:
1) reads (using fread()) input from stdin into a buffer (char []) until EOF is reached (max total bytes 4096).
2) After *all* data has been read from stdin (i.e., EOF has been reached), loop to send the data in the buffer until it has all been sent.  Note that write() will return the number of bytes actually sent, which might be less than the number you requested to be sent (see the man page for more!), so you need to loop to ensure that all has been sent.  This is important not only for this lab but for future labs.
Determine the SHA1 sum of the newly compiled binary file (see man sha1sum).  Show the command line you used to discover the SHA1 sum and its output.
 
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ sha1sum -b client
	5594fc2dd365ff4e54d66220eebd840bbbc4eae6 *client

5b. Start a netcat ("nc" command) server listening for incoming TCP connections on a port of your choosing, and such that its output is piped to the sha1sum command.   Then test your client program by redirecting the contents of alpha.txt (from the tar file) to the program's standard input (using input redirection on the shell).  Show: 1) the pipeline you used to run nc, and its output (after the client finished executing); and 2) the command line you used to run the client program.  The output of the nc pipeline should equal the following: 0ef39a3f241cdd6552ad131e01afa9171b3dab8d

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ nc -l 1234 | sha1sum
	0ef39a3f241cdd6552ad131e01afa9171b3dab8d  -

	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ cat alpha.txt | ./client localhost 1234

5c. Modify client.c, such that after all the data read from stdin has been sent to the socket, the server reads from the socket and prints it out to stdout (you should be able to use the code you commented out in 2d).  Then execute your client program such that 1) you are sending data to the standard HTTP port at www.sandia.gov;  and that 2) you are redirecting the contents of file-http.txt (from the tar file) to the program's standard input (using input redirection on the shell).  Show the command line you used to run the client program and its output.  Note that it should result in an HTTP/1.1 200 OK response.
	
	alex@alex-Mint ~/Documents/LearningWebSockets/hw5 $ cat file-http.txt | ./client www.sandia.gov 80
	Received 215 bytes: HTTP/1.1 200 OK
	Date: Sat, 24 Feb 2018 06:02:04 GMT
	Server: Apache
	X-Frame-Options: SAMEORIGIN
	Last-Modified: Mon, 22 Jan 2018 23:54:21 GMT
	Vary: Accept-Encoding
	Content-Type: text/html; charset=iso-8859-1

Submission
Please include 1) the final modified source code for client.c and server.c, and 2) the output/writeup from requested from each of the numbered items above, in a single file
