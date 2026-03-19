This repo is archived as a similiar example was moved into: https://github.com/farsounder/SDK-Integration-Examples/tree/master/using_sdk

# Build notes

## Windows
``` cmd
cmake -S . -B build
cmake --build build --config Release
```

And you should be able to run the example with:
```
build\Release\farsounder_client_example.exe
```

## Ubuntu 24.04
``` cmd
cmake -S . -B build
cmake --build build-wsl --config Release
```

And you should be able to run the example with:
```
build-wsl/farsounder_client_example
```

To run on another platform, build from source: https://github.com/farsounder/farsounder-cpp-client
