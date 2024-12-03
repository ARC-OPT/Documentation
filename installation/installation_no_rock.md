For Ubuntu 20.04/22.04

### Basic Install

This will install the WBC core library with a single robot model and QP solver respectively. Download this [install script](https://github.com/ARC-OPT/wbc/blob/master/scripts/install.sh?raw=1), store it in a folder of your choice (e.g., `arc-opt`), and execute it:

```
mkdir ~/arc-opt && cd ~/arc-opt
wget https://raw.githubusercontent.com/ARC-OPT/wbc/master/scripts/install.sh
sh install.sh
```
### Full Install

This will install the WBC core library alongside with different robot models, solvers, and Python bindings. Download this [install script](https://github.com/ARC-OPT/wbc/blob/master/scripts/full_install.sh?raw=1), store it in a folder of your choice (e.g., `arc-opt`), and execute it:

```
mkdir ~/arc-opt && cd ~/arc-opt
wget https://raw.githubusercontent.com/ARC-OPT/wbc/master/scripts/full_install.sh
sh full_install.sh
```

# Docker install

This requires [docker](https://docs.docker.com/engine/install/ubuntu/) to be installed beforehand.

```
git clone git@github.com:ARC-OPT/wbc.git
cd wbc/docker
docker build -t <image_name> .
docker run -i -t <image_name>
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

### (Optional) Python Bindings

Note that the Python3 bindings are not maintained as regularly as the core WBC lib.

```
wget https://raw.githubusercontent.com/ARC-OPT/wbc_py/master/scripts/install.sh
sh install.sh
```

### Known Issues

- If shared libraries cannot be found when testing WBC, please update the `LD_LIBRARY_PATH`:
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
```
- The Python bindings are currently not installed as a Python package, thus the `PYTHONPATH` environment variable has to be adapted, so that they can be found by Python:
```
export PYTHONPATH=$PYTHONPATH:/usr/local/lib/pythonX.X/site_packages
```

[[Back to Main Page]](https://arc-opt.github.io/Documentation)
