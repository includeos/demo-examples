### Starlight

This example shows VGA gfx demo showing animated starlight travel.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot starlight
  source deactivate.sh
```
