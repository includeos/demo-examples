# Transfer Service

This is a TCP example service that demonstrates sending a file over a tcp connection.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot transfer_service
  source deactivate.sh
```
