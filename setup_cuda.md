# Setting Up CUDA Environment on Ubuntu

Well it was a long time since last time I set up CUDA Environment on a x86 Linux System.(It was CUDA6, bumblebee, blacklist nouveau etc..)

Now things get surprisingly simpler on Ubuntu!

## 0. Important Tips: Forget about the old traps!

Forget about the bumblebee and traps on switching nouveau. Now Ubuntu has offical
ppa for NVIDIA drivers, just use the system provided installer.

## 1. Install NVIDIA Driver

Add the offical graphics drivers PPA

```
sudo add-apt-repository ppa:graphics-drivers
sudo apt-get update
```

Just use Ubuntu built-in 3rd party driver installer:

system settings - software update - additional driver - selece the version we need

or

`sudo apt-get install nvidia-{version-num}`

Test if we success:

`nvidia-smi`

## 2. Install CUDA

Download CUDA Toolkit form [NVIDIA Website](https://developer.nvidia.com/cuda-zone)

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

### 3. Test if we success

Compile a CUDA sample program and run it-.-
