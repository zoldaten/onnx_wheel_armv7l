# onnx_wheel_armv7l
onnx_for_armv7l(raspberry pi raspbian buster)

---how to build onnx for armv7l from source----
sudo apt remove libprotobuf-dev protobuf-compiler
sudo apt autoremove
pip3 install --upgrade setuptools

git clone https://github.com/protocolbuffers/protobuf.git
cd protobuf
git checkout v3.20.2
git submodule update --init --recursive
mkdir build_source && cd build_source
cmake ../cmake -Dprotobuf_BUILD_SHARED_LIBS=OFF -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_INSTALL_SYSCONFDIR=/etc -DCMAKE_POSITION_INDEPENDENT_CODE=ON -Dprotobuf_BUILD_TESTS=OFF -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)
sudo make install

reboot

git clone https://github.com/onnx/onnx.git
cd onnx
git submodule update --init --recursive
export CMAKE_ARGS=-DONNX_USE_LITE_PROTO=ON
pip install -e .

sudo nano ~/.bashrc 
and put there:
export LD_PRELOAD=/usr/lib/arm-linux-gnueabihf/libatomic.so.1

reread bashrc:
source ~/.bashrc
