## Ubuntu 18.04/20.04

1. Install pre-requisites
    ```bash
    sudo apt-get install ruby-dev git build-essential
    ```

2. If not done yet, setup a ssh key pair using the command `ssh-keygen` and add the key from `~/.ssh/id_rsa.pub ` to the keys in your Gitlab account.  

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
   
    Update and compile

    ```bash
    aup
    ```

    Select the following options (default everywhere else):

    ```bash
    How should I interact with github.com? git
    How should I interact with git.hb.dfki.de? ssh
    Which flavor of Rock do you want to use? master
    Whether C++11 should be enabled for Rock packages? yes
    ```
