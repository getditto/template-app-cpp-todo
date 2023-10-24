# template-app-cpp-todo

## Downloading and Unpacking Ditto

Download Ditto.tar.gz and unpack an archive containing the libditto.a static library and Ditto header:

```
//Linux aarch64
curl -O https://software.ditto.live/cpp-linux-aarch64/Ditto/4.3.0/dist/Ditto.tar.gz && tar xvfz Ditto.tar.gz

//Linux x86_64
curl -O https://software.ditto.live/cpp-linux-x86_64/Ditto/4.3.0/dist/Ditto.tar.gz && tar xvfz Ditto.tar.gz
```

## Linking to Ditto

Add -lditto as a compilation step in the main.cpp source file: 
```
# This command assumes:
# You have unzipped the Ditto.tar.gz in a relative directory ./sdk/
# Your main code entry point is in ./src/main.cpp

g++ -std=c++17 ./src/main.cpp -I ./sdk -lditto -ldl -lrt -pthread -L ./sdk -o dist/main;

 # Once executed, your output will be available at: ./dist/main
```

## Importing Ditto

From the source code of your app, using #include <Ditto.h>,  import Ditto and provide your access credentials:
```
auto identity =
    Identity::OnlinePlayground("YOUR_APP_ID", "PLAYGROUND_TOKEN", true);
try {
  Ditto ditto = Ditto(identity, dir);
  ditto.set_minimum_log_level(LogLevel::debug);
  ditto.start_sync();
} catch (const DittoError &err) {
}
```

