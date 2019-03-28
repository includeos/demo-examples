## IncludeOS Routing Service

This example starts a [IncludeOS](https://github.com/includeos/includeos)routing service.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot router_service
  source deactivate.sh
```
