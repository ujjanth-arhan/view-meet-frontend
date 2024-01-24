# view-meet-frontend

View Meet is a communication applicaiton. This this is the front end part of the code.
Current Features:
1. Simple reactive front end that adjusts to mobile and computer screens
2. Send messages by pressing the enter key or by clicking send
3. Autoscroll to latest message when a new message is sent or received
4. Connect to socket using URL with ws prefix for http and wss prefix for http with tls
5. Supports both sending and receiving of messages through the socket

## Project Setup

```sh
npm install
```

Visit any website that lets you test web sockets and replace the url in the code with the socket url.

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
