# demo-examples
IncludeOS demonstration example

# Dependencies
 - conan
 - cmake 
 - git
 - clang-6.0

# Make sure you have the right conan settings
Install profiles `conan config install https://github.com/includeos/conan_config.git`.

Verify remotes
```bash
#conan remote list
includeos-test: https://api.bintray.com/conan/includeos/test-packages [Verify SSL: True]
bincrafters: https://api.bintray.com/conan/bincrafters/public-conan [Verify SSL: True]
```

# building and running a single example
```bash
cd <example>
mkdir build
cd build
conan install .. -pr clang-6.0-linux-x86_64
cmake ..
cmake --build .
source activate.sh
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
