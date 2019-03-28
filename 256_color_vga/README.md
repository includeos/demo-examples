# 256 color VGA demo

An example of enabling and using 256-color pixel graphics to draw a [Mandelbrot set](https://en.wikipedia.org/wiki/Mandelbrot_set).

> To run this example you need to have a GUI.

### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot 256_color_vga
  source deactivate.sh
```
