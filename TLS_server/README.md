### IncludeOS TLS Server

This TLS Server example should start an instance of [IncludeOS](https://github.com/includeos/includeos) that brings up a minimal web service on HTTPS port 443 with static content.

The default static IP is 10.0.0.42, unless running on a network with DHCP.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot tls_service
  source deactivate.sh
```
