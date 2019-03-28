# IncludeOS Demo Service

This demo-service should start an instance of [IncludeOS](https://github.com/includeos/includeos) that brings up a minimal web service on port 80 with static content.

The default static IP is `10.0.0.42`, unless running on a network with DHCP.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot demo
  source deactivate.sh
```
