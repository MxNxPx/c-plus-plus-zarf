# Zarf package for C++ (c-plus-plus) app

A simple HTTP server implemented in C++ using the C++ REST SDK. It listens for incoming HTTP GET requests and responds with a JSON message. See Docker's [C++ Language Guide](https://docs.docker.com/language/cpp/).

## API

The server only supports the HTTP GET method. When a GET request is received, the server responds with a JSON object:

```json
{
    "message": "OK"
}
```

## Useful commands

```bash
# Build AMD package 
uds run create-packages --set ZARF_CREATE_OPTIONS="--set VERSION=0.1.0"

# Build ARM package 
uds run create-packages --set ZARF_CREATE_ARCH="arm64" --set ZARF_CREATE_OPTIONS="--set PLATFORM=linux/arm64 --set VERSION=0.1.0"

# Publis package to registry
uds zarf package publish zarf-package-c-plus-plus-arm64-0.1.0-upstream.tar.zst oci://registry.uds.dev/public

# Deploy package from registry
uds zarf package deploy --confirm oci://registry.uds.dev/public/c-plus-plus:0.1.0-upstream
```
