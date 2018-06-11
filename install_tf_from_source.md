# Install TensorFlow From Source

Well, since I need to mannualy hack a cuda function into TF, then I need to compile it from source.

Note that this tutorial only tested on Ubuntu16.04 on June 2018. As you know, things are changing fast :)

## Install Python

Personally I believe anaconda is the best way to do this:

1.  Download Anaconda Installer [Here](https://www.anaconda.com/download/)

2.  In terminal, type:

    ```
    sh {a-long-name-for-the-installer}.sh
    ```

3.  (Optional) If we need to switch python version (e.g 3.5):

    ```
    conda install python=3.5
    ```

    Note that the recommanded way to select python version is to create a env. The instructions can be found [Here](https://conda.io/docs/user-guide/tasks/manage-python.html)

4.  Anaconda should contains most python packages needed for TF.

## Install Bazel

Bazel is required to compile TF from source code

1.  Download Bazel binary installer [Here](https://github.com/bazelbuild/bazel/releases)

2.  Install dependencied for installer

    ```
    sudo apt-get install pkg-config zip g++ zlib1g-dev unzip
    ```

3.  Run the installer

    ```
    sh bazel-<version>-installer-linux-x86_64.sh --user
    ```

## Compile and Install TF

Note that we skipped the cuda/cudnn/tensorRT parts. You can find the instructions in another blog

1.  Clone TF repo

    ```
    git clone https://github.com/tensorflow/tensorflow
    cd tensorflow 
    ```

2.  Switch to your desired TF version (e.g, 1.8)

    ```
    git checkout r1.8
    ```

    **Be wise to choose your TF version, it should be compatible with your CUDA/cudnn/TensorRT versions**

3.  Install the python packages if they have not been installed by conda

    ```
    pip install six numpy wheel
    ```

4.  Select configurations

    ```
    ./configure
    ```

    There are loooots of y/n questions, just make sure you enabled CUDA

    **Don't care about the cudnn library path if you installed it from deb package**

5.  Compile TF

    ```
    bazel build --config=opt --config=cuda --cxxopt="-D_GLIBCXX_USE_CXX11_ABI=0" //tensorflow/tools/pip_package:build_pip_package
    ```

    This will take a long time. Take a coffe and just wait it complete.

6.  Build pip package

    ```
    bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
    ```

7.  Install pip package

    ```
    sudo pip install /tmp/tensorflow_pkg/tensorflow-{xxxx}.whl
    ```

8.  Test if we succeed, lets open python and take a try.

    ```
    import tensorflow as tf
    hello = tf.constant('Hello, TensorFlow!')
    sess = tf.Session()
    print(sess.run(hello))
    ```


