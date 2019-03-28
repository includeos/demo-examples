# STREAM

STREAM is Sustainable Memory Bandwidth in High Performance Computers. The output from this service should show estimated memory bandwidth inside a virtual machine.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot stream
  source deactivate.sh
```
