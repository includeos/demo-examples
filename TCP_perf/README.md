# IncludeOS TCP Performance

This service demonstrates TCP performance by sending and receiving data.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot tcp_perf_service
  source deactivate.sh
```

### Howto:

Receive data from the instance:
```
ncat 10.0.0.42 1337 --recv-only > bla.txt
```

Send data to the instance:
```
cat bla.txt | ncat 10.0.0.42 1338 --send-only
```

Configure by changing the variables at the top.
