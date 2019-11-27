# Build and Install EVE Guest Services Libraries and Tools

## On Linux

### On Debian/Ubuntu

#### 1. Install the prerequisite libraries:
`sudo apt-get install -y docker.io libprotobuf-dev libprotoc-dev protobuf-compiler cmake g++ libssl-dev libcurl4-openssl-dev uuid-dev`

#### 2. [Install Azure IoT Edge Runtime](https://docs.microsoft.com/en-us/azure/iot-edge/how-to-install-iot-edge-linux)

#### 3. First build EVE TPM API library:
`cd eve-tools`
`make`
`sudo make install`
  
 #### 4. Then build the EVE specific HSM plugin for Azure IoT Edge:
`cd azure-on-eve`
`mkdir build; cd build`
`cmake -Drun_unittests=OFF -DUSE_TEST_TPM_INTERFACE_IN_MEM=OFF -DBUILD_SHARED=ON -Duse_cppunittest=OFF ..`
`cmake --build`
`sudo cp libiothsm.so* /usr/lib`

#### 5. After this restart IoT Edge Runtime, for the plugin to take effect:
`sudo /etc/init.d/iotedge restart`