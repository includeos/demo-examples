# Demo-examples

Here you will find a number of [IncludeOS](https://github.com/includeos/IncludeOS) demo examples.
The examples demonstrate various features of IncludeOS. The examples
are also built and started with conan.

Each example folder contains:
- `README.md`: Instructions on how to build/start the example
- `CMakeLists.txt`: Build requirements
- `config.json`: Network configurations required for the example
- `service.cpp` : the `c++` example service
- `conanfile.txt`: the library/tool dependencies the example requires
- `vm.json`: some examples may have a `vm.json` if it requires some virtual configuration.


## Dependencies
To build and start the examples, ensure the following dependencies are installed on your system.
 - conan
 - cmake
 - git
 - clang-6.0

> NOTE: If you are on MacOS and would like to try our `brew` to install IncludeOS, you can follow the instructions in our [includeos/homebrew-includeos](https://github.com/includeos/homebrew-includeos).

### Making sure you have the right conan settings

__Install profiles and IncludeOS remotes__

```
  $ conan config install https://github.com/includeos/conan_config.git
```

__Add the bincrafters remote__

```
  $ conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan
```

__Verify remotes__

### Building and running a single example
To build and run a single example, go into one of the examples and do;

```bash
  cd <example>
  mkdir build
  cd build
  conan install .. -pr clang-6.0-linux-x86_64
  source activate.sh
  cmake ..
  cmake --build .
  boot (service_name)
  source deactivate.sh
```


# Building all the examples
Create a build folder and do

```bash
  export CC=clang
  export CXX=clang
  mkdir build_all
  cd build_all
  cmake <path_to_repo> -DCONAN_PROFILE=clang-6.0-linux-x86_64 -DPROTOBUF=ON
```
