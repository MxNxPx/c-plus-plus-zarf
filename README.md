# Zarf package for C++ (c-plus-plus) app

A simple HTTP server implemented in C++ using the C++ REST SDK. It listens for incoming HTTP GET requests and responds with a JSON message. See Docker's [C++ Language Guide](https://docs.docker.com/language/cpp/).

## API

The server only supports the HTTP GET method. When a GET request is received, the server responds with a JSON object:

```json
{
    "message": "OK"
}
```

