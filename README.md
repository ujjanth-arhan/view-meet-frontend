# view-meet-frontend

View Meet is a communication applicaiton. This this is the front end part of the code.
Current Features:
1. Simple reactive front end that adjusts to mobile and computer screens
2. Send messages by pressing the enter key or by clicking send
3. Autoscroll to latest message when a new message is sent or received
4. Connect to socket using URL with ws prefix for http and wss prefix for http with tls
5. Supports both sending and receiving of messages through the socket

### Run and Test Application

Install docker https://docs.docker.com/get-docker/<br>
(tested on Docker Desktop 4.27.2 (137060))

Clone the repository<br>
**OR**<br>
Pull the docker image
```docker
docker pull ujjanth/view-meet-frontend:latest
```

Execute the following in `view-meet-frontend/`
```docker
docker build -t view-meet-frontend .
```

```docker
docker run --name view-meet-frontend-container --rm -p 127.0.0.1:3000:3000 view-meet-frontend
```

Open multiple 127.0.0.1:3000 in different windows or in private or incognito mode and chat away 

### Development Setup

```shell
npm install
```

```shell
npm run dev
```

Visit any website that lets you test web sockets and replace the url in the code with the socket url<br>
**OR**<br>
Download and run view-meet-backend

Happy chatting away!