For Ubuntu 18.04/20.04

### Basic Install

Download the [install script](https://github.com/ARC-OPT/wbc/blob/master/scripts/install.sh) and type:

```
sh install.sh
```

### (Optional) With Python Bindings

Using Python2:

```
sudo apt-get install python-dev libboost-python-dev libboost-numpy-dev python-numpy
mkdir wbc/build && cd wbc/build
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
