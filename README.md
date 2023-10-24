# template-app-cpp-todo

To install the C++ SDK:
1. Fetch and extract the Ditto package. [Downloading and Unpacking Ditto](https://docs.ditto.live/installing-cpp#mNh1p:~:text=)-,Downloading%20and%20Unpacking%20Ditto,-Download%20Ditto.tar)
2. Configure your app to link to the Ditto static library. [Linking to Ditto](https://docs.ditto.live/installing-cpp#KF0yE:~:text=Add%20%2Dlditto%20as%20a%20compilation%20step%20in%20the%20main.cpp%20source%20file%3A)

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

