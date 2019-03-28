### LiveUpdate Demo Service

This service should start an instance of [IncludeOS](https://github.com/includeos/includeos) that brings up a minimal web service on port 80 with static content. When running update.sh the service should be updated with itself.


### Build and run service

* To Build:

```
  $ mkdir build
  $ cd build
  $ conan install .. -pr <profile-name>
  $ source activate.sh
  $ cmake ..
  $ cmake --build .
```

* To run the serive:

```
  $ boot ircd_example
```

* To update:

```
  $ ./update.sh
```

When finished, reset configurations:

```
  $ source deactivate.sh
```
