### IncludeOS Scoped Profiler Demo

Add `ScopedProfiler sp;` in the scopes that you want to profile. Don't forget to `#include <profile>`.

Rebuild / install IncludeOS:

```
cd IncludeOS
mkdir build
cd build
cmake ..
make
make install
```


### Build and run service

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot scoped_profiler_example
  source deactivate.sh
```

Make something happen in the OS and then use wget or curl to `GET /profile` to see statistics:

```
curl 10.0.0.42/profile
```
