# Jetson nano tricks
Things to do before starting

```
sudo apt-get update && sudo apt-get install python3-pip python3-dev nano
```
How install cmake update (required by many programs)
```
sudo apt-get remove --purge cmake
sudo apt-get install libssl-dev
wget https://cmake.org/files/v3.21/cmake-3.21.1.tar.gz
tar -xzvf cmake-3.21.1.tar.gz
cd cmake-3.21.1
./bootstrap
make -j4
sudo make install
```
# How install numba (essential for many projects)
Fast way:
```
git clone https://github.com/wjakob/tbb.git
cd tbb/build
cmake ..
make -j
sudo make install
sudo apt install llvm-10
export LLVM_CONFIG=/usr/bin/llvm-config-10
pip3 install llvmlite
pip3 install numba
```

For this it takes 30 hours for the nano jetson 2gb
```
wget https://github.com/llvm/llvm-project/releases/download/llvmorg-10.0.1/llvm-10.0.1.src.tar.xz
tar -xvf llvm-10.0.1.src.tar.xz
cd llvm-10.0.1.src.tar.xz
mkdir llvm_build_dir
cd llvm_build_dir/
cmake ../ -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD="ARM;X86;AArch64"
make -j4
sudo make install
cd bin/
echo "export LLVM_CONFIG=\""`pwd`"/llvm-config\"" >> ~/.bashrc
echo "alias llvm='"`pwd`"/llvm-lit'" >> ~/.bashrc
source ~/.bashrc
cd
git clone https://github.com/wjakob/tbb.git
cd tbb/build
cmake ..
make -j
sudo make install
pip3 install llvmlite
pip3 install numba
```

# Build Face Recognition
Before that install numba
```
wget http://dlib.net/files/dlib-19.17.tar.bz2
tar jxvf dlib-19.17.tar.bz2
cd dlib-19.17
nano dlib/cuda/cudnn_dlibapi.cpp
```
Search the file for the following line of code (which should be line 854):
```
forward_algo = forward_best_algo;
```
And comment it out by adding two slashes in front of it, so it looks like this:
```
//forward_algo = forward_best_algo;
```
Then: 
```
sudo python3 setup.py install
```
and at the end
```
sudo pip3 install face_recognition
```


