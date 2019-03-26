### Snake game

Using VGA text-mode in qemu (or possibly VirtualBox) we can play snake!

> NOTE: This example requires the use of a video device. Otherwise it is unable
to initialize SDL, thus the service will fail.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot snake_example
  source deactivate.sh
```

Use arrow keys to change the snakes direction. Press spacebar to restart the game.
