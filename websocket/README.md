# IncludeOS WebSocket Example

This service demonstrates websocket, and utilizes memdisk, autoconf and http server.

Start with service and visit [http://10.0.0.42](http://10.0.0.42) from a browser that supports WebSocket.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot websocket_service
  source deactivate.sh
```
