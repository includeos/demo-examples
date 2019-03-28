### Test service for Google's protobuf runtime library

This service is to test our build of the protobuf runtime library, therefore it can only be built if [IncludeOS](https://github.com/includeos/includeos) was installed with the `libprotobuf` option set to `ON`.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot protobuf_test_service
  source deactivate.sh
```
