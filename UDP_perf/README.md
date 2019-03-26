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

<!-- TODO: How this servier client test works now?

### Howto run as a Server:

```
  boot udp_service

```

On other terminal run: `./send.sh`

### Howto run as a Client:
On a terminal run: `./receive.sh`
On other terminal run: `boot --create-bridge . client`

-->

### Closing the service

```
  source deactivate.sh
```

### How sampling is done
Sampling is collected approximately every 5 seconds when the unikernel is run as a server.
Sampling is collected approximately every second when the unikernel is run a client. The test runs for 10 seconds.
