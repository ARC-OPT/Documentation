## Ubuntu 18.04/20.04

1. Install pre-requisites
    ```bash
    sudo apt-get install ruby-dev git build-essential cmake
    ```

2. If not done yet, setup a ssh key pair using the command `ssh-keygen` and add the key from `~/.ssh/id_rsa.pub ` to the keys in your Github account.  

3. If not done yet, setup your gitconfig

    ```bash
    git config --global user.email yourmail@adress.com
    git config --global user.name yourname
    ```

4. Bootstrap

    Get buildconf

    ```bash
    mkdir ~/rock && cd ~/rock
    wget http://rock-robotics.org/autoproj_bootstrap
    ruby autoproj_bootstrap git git@github.com:ARC-OPT/buildconf.git
    ```

    Source you environment

    ```bash
    source ~/rock/env.sh
    ```

    or make the environment persistent by adding the following lines to your .bashrc file
    
    ```bash
    echo "source ~/rock/env.sh" >> ~/.bashrc
    ```
   
    Update

    ```bash
    aup orogen/wbc
    aup orogen/ctrl_lib
    ```  

    Select default options everywhere. In order to speed up the build process you can select: 

    ```bash
    Do you want to use icecc for compiling sources [yes/no] [no] yes
    Do you want to use ccache for compiling sources [yes/no] [no] yes
    ```
    
    Build
    
    ```bash
    amake orogen/wbc
    amake orogen/ctrl_lib
    ```
