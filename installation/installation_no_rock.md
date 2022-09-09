For Ubuntu 18.04/20.04

### Basic Install

Download the [install script](https://github.com/ARC-OPT/wbc/blob/master/scripts/install.sh), store it in a folder of your choice (e.g., arc-opt) and execute it:

```
mkdir ~/arc-opt && cd ~/arc-opt
sh install.sh
```

### (Optional) Additional Solvers

Eiquadprog:

```
cd ~/arc-opt
git clone --recurse-submodules https://github.com/stack-of-tasks/eiquadprog.git
cd eiquadprog
cp ../wbc/patches/eiquadprog.patch . && git apply eiquadprog.patch
mkdir build && cd build
cmake .. && sudo make -j8 install
cd ~/arc-opt/wbc/build
cmake .. -DUSE_EIQUADPROG=1
sudo make -j8 install
```

qpSWIFT:

```
cd ~/arc-opt
git clone https://github.com/qpSWIFT/qpSWIFT.git
cd qpSWIFT
cp ../wbc/patches/qpSWIFT.patch . && git apply qpSWIFT.patch
mkdir build && cd build
cmake .. && sudo make -j8 install
cd ~/arc-opt/wbc/build
cmake .. -DUSE_QPSWIFT=1
sudo make -j8 install
```

### (Optional) Additional Robot Models

Pinnocchio:

```
cd ~/arc-opt
git clone --recurse-submodules https://github.com/stack-of-tasks/pinocchio.git
cd pinocchio
cp ../wbc/patches/pinocchio.patch . && git apply pinocchio.patch
mkdir build && cd build
cmake .. -DBUILD_PYTHON_INTERFACE=OFF -DBUILD_UNIT_TESTS=OFF && sudo make -j8 install
cd ~/arc-opt/wbc/build
cmake .. -DUSE_PINOCCHIO=1
sudo make -j8 install
```

RBDL (This currently requires an account on https://git.hb.dfki.de)

```
sudo apt-get install libyaml-cpp-dev liblua5.1-0-dev
cd ~/arc-opt
git clone git@git.hb.dfki.de:dfki-mechanics/hyrodyn/rbdl.git
cd rbdl && mkdir build
cd build && cmake ..
sudo make -j8 install && cd ..
cd ~/arc-opt/wbc/build
cmake .. -DUSE_RBDL=1
sudo make -j8 install
```

### (Optional) With Python Bindings

Using Python2:

```
sudo apt-get install python-dev libboost-python-dev libboost-numpy-dev python-numpy
cd ../wbc/build
cmake .. -DUSE_PYTHON=1
sudo make -j8 install
```
Using Python3:
```
TODO
```

### (Optional) With Hyrodyn-based robot model
This currently requires an account on https://git.hb.dfki.de
```
sudo apt-get install libyaml-cpp-dev liblua5.1-0-dev

git clone git@git.hb.dfki.de:dfki-mechanics/hyrodyn/rbdl.git
cd rbdl && mkdir build
cd build && cmake ..
sudo make -j8 install && cd ../..

git clone git@git.hb.dfki.de:dfki-mechanics/hyrodyn/hyrodyn.git
cd hyrodyn && mkdir build
cd build && cmake ..
sudo make -j8 install && cd ../..

mkdir wbc/build && cd wbc/build
cmake .. -DUSE_HYRODYN=1
sudo make -j8 install && cd ../..
```

### Known Issues

- If shared libraries cannot be found when testing WBC, please update the LD_LIBRARY_PATH:
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
```
- The cmake option `-DUSE_PYTHON=1` currently only works together with `-DUSE_HYRODYN=1`
