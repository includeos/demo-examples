### microLB demo

Start the nodeJS demo services first:

```
  $ node server.js
```

### Build and run service

Build and run the load balancer.

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot microlb_example
  source deactivate.sh
```

### Connect to the load balancer
```
  curl 10.0.0.42
```

The load balancer should be configured to round-robin on `10.0.0.1` ports 6001-6004.
