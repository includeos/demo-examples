# acorn
Acorn Web Server Appliance running on IncludeOS.

### Features

* Serve static content from a disk with just a few lines of code.
* RESTful API service reading and posting JSON.
* Real-time information about the server with an interactive Dashboard

Acorn is a simple web server using a collection of libraries and extensions:

* [Mana](https://github.com/includeos/mana) - IncludeOS Web Appliance Framework
* [Bucket](https://github.com/includeos/bucket) - Simplified in-memory database

Content to be served can be found (and edited) in the directory [disk1](disk1/).

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot acorn
  source deactivate.sh
```
