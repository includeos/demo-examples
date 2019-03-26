# IRCd

This example sets up an IRC server using [IncludeOS](https://github.com/includeos/includeos).

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot ircd_example
  source deactivate.sh
```
