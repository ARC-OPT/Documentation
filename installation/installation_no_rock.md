For Ubuntu 18.04/20.04

### Basic Install

This will install the WBC core library with a single robot model and QP solver respectively. Download this [install script](https://github.com/ARC-OPT/wbc/blob/master/scripts/install.sh?raw=1), store it in a folder of your choice (e.g., arc-opt) and execute:

```
mkdir ~/arc-opt && cd ~/arc-opt
sh install.sh
```
### Full Install

This will install the WBC core library alongside with different robot models, solvers and python bindings. Download this [install script](https://github.com/ARC-OPT/wbc/blob/master/scripts/full_install.sh?raw=1), store it in a folder of your choice (e.g., arc-opt) and execute:

```
mkdir ~/arc-opt && cd ~/arc-opt
sh full_install.sh
```

### (Optional) With Python Bindings

This requires python3

```
sudo apt-get install python3-dev python3-numpy python3-nose libboost-python-dev libboost-numpy-dev
cd ~/arc-opt/wbc/build
cmake .. -DUSE_PYTHON=1
sudo make -j8 install
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
- The python bindings are currently not installed as python package, thus the PYTHONPATH has to be adapted, so that they can be fpund by python:
```
export PYTHONPATH=$PYTHONPATH:/usr/local/lib/pythonX.X/site_packages
```
