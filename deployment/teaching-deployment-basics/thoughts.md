# Teaching deployment basics

When it comes to deploying front end web apps or backend services,
which is in general releasing software / distributing software,
there are lots of things that a person needs to learn. Also,
we have come a long way in how to deploy services, different
methods and platforms and tools and what not. It's not easy to
teach someone about this though. The below is my take at what to
talk about.

Deployment 101. Server. Server serves. It refers to a process. File server, TCP server. Sometimes people refer to the whole computer as one server, it's possibly because that's the main process running in the computer according to them, surely other things are running and possibly other servers itself. Possible. 

Server runs at a port. Port? Machine has an IP. IP?

Networking 101. IP address. Port number. Process to process communication. IP to identify computer, port to identify exact process, as a computer can run more than one process. IP - private IP, public IP. Due to the deficiency of IP addresses in IPv4. Now we have IPv6, but usage is less. How to know IP, just know it, or use DNS, Domain name service, which have names and then records to know what's the IP address of the domain name. Domain names are easy for humans to remember. Computers can convert domain names to IP addresses as they need IP to communicate in network. Port is assumed based on the protocol being used. Protocols have some default ports for the servers talking using that protocol. For HTTP server default port is 80. But that's just a standard. You can still run a HTTP server at port 8080 or 9090 or any valid port number. Just that, your client needs to know this. Usually the human or system who ran the server should help the client know this information somehow. DNS records can also help with this. There's a SRV record. And DNS records need to be created by someone or some system. That's the discovery part of it. And there are different kinds of DNS records. CNAME, A, AAAA, TXT, etc. 

Client server architecture. Client commands, server serves functionality to client. Helps to create a centralized system that the client can access from anywhere if the server is intact. There can different forms of clients, different devices. Mobile, desktop, tab. Command line interface, graphical user interface, voice interface etc.

For deployment, you need a computer, with CPU, RAM, disk, network etc, running all time with power. Static IP. Hard.

Cloud. They take care of maintaining stuff for you.

