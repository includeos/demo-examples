# mender example

Example using the [IncludeOS](https://github.com/includeos/includeos) [mender.io](https://github.com/includeos/mender) client.

To try it out you need to run the [mender integration (v1.0.x)]().

# Mender integration service

```
  git clone -b 1.0.x https://github.com/mendersoftware/integration.git
  cd integration/
  ./demo -f docker-compose.no-ssl.yml up
```

# Artifact
To deploy updates you need to create a mender artifact from a IncludeOS service binary.



### Build and run service
To create a binary inside the service folder and run the serivce;

```
  mkdir build
  cd build
  conan install .. -pr <profile-name>
  source activate.sh
  cmake ..
  cmake --build .
  boot mender
  source deactivate.sh
```

Information on how to create a mender artifact can be found here:
https://docs.mender.io/1.0/artifacts/modifying-a-mender-artifact
