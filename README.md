This is a fork of https://github.com/sradevski/tobii-eyex-websocket-server


## Synopsis

**Tobii Web Socket Server** is a Web Socket Server that wraps the Tobii EyeX SDK and transmits the data through web sockets. We used it in our EyeCaptain Electron application to stream the X/Y positions to the app.

## Usage

- run `TobiiSocketServer.exe`, which will start the server on the default port (8887)
- you can optionally pass a custom port number like `TobiiSocketServer.exe 8886`

## Usage in electron

- in your Electron main application, start the Server as a background process:

```
var child = spawn("path/to/TobiiSocketServer.exe", {
    //stdio: "ignore"
  });
```

- After starting, tell the renderer process to connect to the websocket and do something with the position information

```
var ws = new WebSocket('ws://' + ipAddress + ':' + port);
ws.on('open', function () {
  // Tracker connected
});

ws.on('close', function () {
  // Tracker disconnected
});

ws.on('message', function (msg, flags) {
  // Parse json position message:
  var tmpPosition = JSON.parse(msg);
  console.log(tmpPosition)
});
```

## License

This project is under the [MIT Licence](LICENSE)
