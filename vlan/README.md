### IncludeOS VLAN example

This service demonstrates how VLAN works in [IncludeOS](https://github.com/includeos/includeos)


### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot vlan_service
  source deactivate.sh
```
