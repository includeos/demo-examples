# demo-examples
IncludeOS demonstration example

# Dependencies
 - conan
 - cmake
 - git
 - clang-6.0

# Make sure you have the right conan settings
Install profiles `conan config install https://github.com/includeos/conan_config.git`.

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
