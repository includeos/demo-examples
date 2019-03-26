# IncludeOS HTTP Client example

This example will send a GET request to http://www.google.com with our Basic_client, and to https://www.google.com with our HTTPS supported Client.
For the example to succeed, make sure your virtual machine can reach the internet (ip forward & nat).

For example purpose only. Don't reuse the `server.pem` certificate.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot http_demo
  source deactivate.sh
```
