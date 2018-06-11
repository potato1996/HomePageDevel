# Setting Up CUDA Environment on Ubuntu

Well it was a long time since last time I set up CUDA Environment on a x86 Linux System.(It was CUDA6, bumblebee, blacklist nouveau etc..)

Now things get surprisingly simpler on Ubuntu!

Note that this tutorial only tested on Ubuntu16.04 on June 2018. As you know, things are changing fast :)

## 0. Important Tips: Forget about the old traps!

Forget about the bumblebee and traps on switching nouveau. Now Ubuntu has offical
ppa for NVIDIA drivers, just use the system provided installer.

**Solve Annoying sudo env**

Add following into `~/.bashrc`: `alias sudo='sudo env PATH=$PATH'`

## 1. Install NVIDIA Driver

Add the offical graphics drivers PPA

    ```
    sudo add-apt-repository ppa:graphics-drivers
    sudo apt-get update
    ```

Just use Ubuntu built-in 3rd party driver installer:

System Settings - Software Update - Additional Drivers - selece the version we need

or

`sudo apt-get install nvidia-{version-num}`

Test if we success:

`nvidia-smi`

## 2. Install CUDA

Download CUDA Toolkit form [NVIDIA Website](https://developer.nvidia.com/cuda-zone)

### Install From Deb(recommended)

Will get something like `{a-long-name}.deb`, then install it:

    ```
    sudo dpkg -i {a-long-name}.deb
    sudo apt-get install cuda-{version}
    ```

### Install From Run

Will get something like `{a-long-name}.run`

Then `sudo sh {a-long-name}.run --override`

**Important Notes**

1. Answer "no" for installing driver

2. Answer "yes" for creating softlink

3. Set environment variable, add follwing in `~/.bashrc`

    ```
    export PATH=/usr/local/cuda/bin:$PATH
    export LD_LIBRARY_PATH=/user/local/cuda/lib64:$LD_LIBRARY_PATH
    ```

4. activate changing to env: `source ~/.bashrc` or just open a new terminal..

Test if we success

Compile a CUDA sample program and run it-.-

## 3. Install cuDNN

1. Download cuDNN tar package from [NVIDIA Website](https://developer.nvidia.com/cudnn)

### Install From Deb(Recommended)

2. Install the deb packages

    ```
    dpkg -i libcudnn*
    ```

### Install Compiled Lib


2. Unzip the package

    ```
    tar -xzvf cudnn-{version}.tgz
    ```

3. copy into cuda install directory

    ```
    sudo cp cuda/include/cudnn.h /usr/local/cuda/include
    sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
    sudo chmod a+r /usr/local/cuda/include/cudnn.h
    /usr/local/cuda/lib64/libcudnn*
    ```

    Note that differ from apt, download the compile lib mannually will not affect ld lib cache, etc. Be care to deal with the path problems by yourself :P 

## 4. Install TensorRT

1. Download TensorRT tar package from [NVIDIA Website](https://developer.nvidia.com/tensorrt)

2. Follow the offical installation guide

PS: It's not because I'm lazy here. Unlike CUDA, TensorRT is changing fast and the way to install is tend to be inconsistent in the future. I will wait for a more stable installation way and update it here (like, apt-get or release page with deb packages)

## 5. Setup paths in your bashrc

1.  Open your bashrc

    ```
    vim ~/.bashrc
    ```

2.  Add following at the end of the file

    ```
    # HOME Executable Path
    export PATH=$HOME/bin:$PATH

    # CUDA Executable Path
    export PATH=/usr/local/cuda/bin:$PATH

    # CUDA Library Path
    export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH

    # CUPTI Library Path
    export LD_LIBRARY_PATH=/usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH

    # TensorRT Library Path
    export LD_LIBRARY_PATH=/usr/local/TensorRT/lib:$LD_LIBRARY_PATH

    # Anaconda3 Executable Path
    export PATH="/home/potato/anaconda3/bin:$PATH"
    ```
3.  Save the file, and activate it: `source ~/.bashrc`