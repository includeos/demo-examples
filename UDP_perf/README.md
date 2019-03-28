# IncludeOS UDP Performance
Runs a udp server or a client as a [IncludeOS](https://github.com/includeos/includeos) unikernel

### Pre-requistes
Requires `ncat`

## Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
```


### Howto run as a Server:

```
  boot udp_service

```

To create and send a file, on another terminal run: `./send.sh`

### Howto run as a Client:

To start the client on other terminal run:

```
  boot udp_service client
```

To listen on port 1338 and dump received data to `recv.txt`,
on another terminal run: `./receive.sh`


### Closing the service

```
  source deactivate.sh
```

### How sampling is done
Sampling is collected approximately every 5 seconds when the unikernel is run as a server.
Sampling is collected approximately every second when the unikernel is run as a client. The test runs for 10 seconds.
