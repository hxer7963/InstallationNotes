#### 更新cmake

Note: 如果只安装CPU xgboost，CMake 3.2 or higher.安装GPU xgboost，CMake 

```sh
$ cmake --version
cmake version 3.5.1

CMake suite maintained and supported by Kitware (kitware.com/cmake).
$ mkdir /tmp/cmake
$ cd /tmp/cmake
$ wget https://github.com/Kitware/CMake/releases/download/v3.14.3/cmake-3.14.3.tar.gz
$ tar -xzvf cmake-3.14.3.tar.gz >> /dev/null
$ cd cmake-3.14.3
$ ./bootstrap
$ nproc
12
$ make -j12
$ sudo make install
$ cmake --version
cmake version 3.14.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
```

参考：[How do I install the latest version of cmake from the command line?](https://askubuntu.com/questions/355565/how-do-i-install-the-latest-version-of-cmake-from-the-command-line)

[CMake Download](<https://cmake.org/download/>) 

#### 安装NVCC

如果不使用NVIDIA GPU加速XGBoost，可跳过；

```sh
$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2017 NVIDIA Corporation
Built on Fri_Sep__1_21:08:03_CDT_2017
Cuda compilation tools, release 9.0, V9.0.176
$ which nvcc
/usr/local/cuda-9.0/bin/nvcc
$ git clone --recursive https://github.com/dmlc/xgboost
$ cd xgboost
$ mdkir build
$ cd build
$ cmake .. -DUSE_CUDA=ON
cmake .. -DUSE_CUDA=ON
-- CMake version 3.14.3
-- Configured CUDA host compiler: /usr/bin/c++
-- The CUDA compiler identification is unknown
-- Check for working CUDA compiler: /usr/local/cuda-9.0/bin/nvcc
-- Check for working CUDA compiler: /usr/local/cuda-9.0/bin/nvcc -- broken
CMake Error at /usr/local/share/cmake-3.14/Modules/CMakeTestCUDACompiler.cmake:46 (message):
  The CUDA compiler

    "/usr/local/cuda-9.0/bin/nvcc"

  is not able to compile a simple test program.

  It fails with the following output:

    Change Dir: /home/hxer/Project/xgboost/build/CMakeFiles/CMakeTmp

    Run Build Command(s):/usr/bin/make cmTC_5e369/fast
    /usr/bin/make -f CMakeFiles/cmTC_5e369.dir/build.make CMakeFiles/cmTC_5e369.dir/build
    make[1]: Entering directory '/home/hxer/Project/xgboost/build/CMakeFiles/CMakeTmp'
    Building CUDA object CMakeFiles/cmTC_5e369.dir/main.cu.o
    /usr/local/cuda-9.0/bin/nvcc -ccbin=/usr/bin/c++    -x cu -c /home/hxer/Project/xgboost/build/CMakeFiles/CMakeTmp/main.cu -o CMakeFiles/cmTC_5e369.dir/main.cu.o
    In file included from /usr/local/cuda-9.0/bin/..//include/host_config.h:50:0,
                     from /usr/local/cuda-9.0/bin/..//include/cuda_runtime.h:78,
                     from <command-line>:0:
    /usr/local/cuda-9.0/bin/..//include/crt/host_config.h:119:2: error: #error -- unsupported GNU version! gcc versions later than 6 are not supported!
     #error -- unsupported GNU version! gcc versions later than 6 are not supported!
      ^~~~~
    CMakeFiles/cmTC_5e369.dir/build.make:65: recipe for target 'CMakeFiles/cmTC_5e369.dir/main.cu.o' failed
    make[1]: *** [CMakeFiles/cmTC_5e369.dir/main.cu.o] Error 1
    make[1]: Leaving directory '/home/hxer/Project/xgboost/build/CMakeFiles/CMakeTmp'
    Makefile:121: recipe for target 'cmTC_5e369/fast' failed
    make: *** [cmTC_5e369/fast] Error 2




  CMake will not be able to correctly generate this project.
Call Stack (most recent call first):
  CMakeLists.txt:63 (enable_language)


-- Configuring incomplete, errors occurred!
See also "/home/hxer/Project/xgboost/build/CMakeFiles/CMakeOutput.log".
See also "/home/hxer/Project/xgboost/build/CMakeFiles/CMakeError.log".
$ export CUDAHOSTCXX=g++-5
$ cmake .. -DUSE_CUDA=ON
-- CMake version 3.14.3
-- Configured CUDA host compiler: /usr/bin/c++
-- The CUDA compiler identification is NVIDIA 9.0.176
-- Check for working CUDA compiler: /usr/local/cuda-9.0/bin/nvcc
-- Check for working CUDA compiler: /usr/local/cuda-9.0/bin/nvcc -- works
-- Detecting CUDA compiler ABI info
-- Detecting CUDA compiler ABI info - done
-- CUDA GEN_CODE: --generate-code=arch=compute_35,code=sm_35;--generate-code=arch=compute_50,code=sm_50;--generate-code=arch=compute_52,code=sm_52;--generate-code=arch=compute_60,code=sm_60;--generate-code=arch=compute_61,code=sm_61;--generate-code=arch=compute_70,code=sm_70;--generate-code=arch=compute_70,code=compute_70;
-- /home/hxer/Project/xgboost/dmlc-core/cmake/build_config.h.in -> /home/hxer/Project/xgboost/dmlc-core/include/dmlc/build_config.h
-- Using nccl library: NCCL_LIBRARY-NOTFOUND
CMake Error at /usr/local/share/cmake-3.14/Modules/FindPackageHandleStandardArgs.cmake:137 (message):
  Could NOT find Nccl (missing: NCCL_INCLUDE_DIR NCCL_LIBRARY)
Call Stack (most recent call first):
  /usr/local/share/cmake-3.14/Modules/FindPackageHandleStandardArgs.cmake:378 (_FPHSA_FAILURE_MESSAGE)
  cmake/modules/FindNccl.cmake:59 (find_package_handle_standard_args)
  src/CMakeLists.txt:49 (find_package)


-- Configuring incomplete, errors occurred!
See also "/home/hxer/Project/xgboost/build/CMakeFiles/CMakeOutput.log".
See also "/home/hxer/Project/xgboost/build/CMakeFiles/CMakeError.log".
```

> Could Not find Nccl (missing NCCL_INCLUDE_DIR NCCL_LIBRARY).

```sh
$ ls
nccl-repo-ubuntu1604-2.4.2-ga-cuda9.0_1-1_amd64.deb
$ sudo dpkg -i nccl-repo-ubuntu1604-2.4.2-ga-cuda9.0_1-1_amd64.deb
(Reading database ... 186993 files and directories currently installed.)
Preparing to unpack nccl-repo-ubuntu1604-2.4.2-ga-cuda9.0_1-1_amd64.deb ...
Unpacking nccl-repo-ubuntu1604-2.4.2-ga-cuda9.0 (1-1) over (1-1) ...
Setting up nccl-repo-ubuntu1604-2.4.2-ga-cuda9.0 (1-1) ...
$ sudo apt update
Get:1 file:/var/nccl-repo-2.4.2-ga-cuda9.0  InRelease
Ign:1 file:/var/nccl-repo-2.4.2-ga-cuda9.0  InRelease
Get:2 file:/var/nccl-repo-2.4.2-ga-cuda9.0  Release [574 B]
Get:2 file:/var/nccl-repo-2.4.2-ga-cuda9.0  Release [574 B]
Get:3 file:/var/nccl-repo-2.4.2-ga-cuda9.0  Release.gpg [801 B]
Get:3 file:/var/nccl-repo-2.4.2-ga-cuda9.0  Release.gpg [801 B]
Get:4 file:/var/nccl-repo-2.4.2-ga-cuda9.0  Packages [946 B]
...
$ sudo apt install libnccl2 libnccl-dev
The following NEW packages will be installed:
  libnccl-dev libnccl2
0 upgraded, 2 newly installed, 0 to remove and 30 not upgraded.
Need to get 0 B/68.8 MB of archives.
After this operation, 269 MB of additional disk space will be used.
Get:1 file:/var/nccl-repo-2.4.2-ga-cuda9.0  libnccl2 2.4.2-1+cuda9.0 [35.3 MB]
Get:2 file:/var/nccl-repo-2.4.2-ga-cuda9.0  libnccl-dev 2.4.2-1+cuda9.0 [33.4 MB]
Selecting previously unselected package libnccl2.
(Reading database ... 186993 files and directories currently installed.)
Preparing to unpack .../libnccl2_2.4.2-1+cuda9.0_amd64.deb ...
Unpacking libnccl2 (2.4.2-1+cuda9.0) ...
Selecting previously unselected package libnccl-dev.
Preparing to unpack .../libnccl-dev_2.4.2-1+cuda9.0_amd64.deb ...
Unpacking libnccl-dev (2.4.2-1+cuda9.0) ...
Setting up libnccl2 (2.4.2-1+cuda9.0) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Setting up libnccl-dev (2.4.2-1+cuda9.0) ...
$ ls /var/nccl-repo-2.4.2-ga-cuda9.0/
7fa2af80.pub  Release      libnccl-dev_2.4.2-1+cuda9.0_amd64.deb
Packages.gz   Release.gpg  libnccl2_2.4.2-1+cuda9.0_amd64.deb
(build) $ cmake .. -DUSE_CUDA=ON
-- CMake version 3.14.3
-- Configured CUDA host compiler: /usr/bin/c++
-- CUDA GEN_CODE: --generate-code=arch=compute_35,code=sm_35;--generate-code=arch=compute_50,code=sm_50;--generate-code=arch=compute_52,code=sm_52;--generate-code=arch=compute_60,code=sm_60;--generate-code=arch=compute_61,code=sm_61;--generate-code=arch=compute_70,code=sm_70;--generate-code=arch=compute_70,code=compute_70;
-- /home/hxer/Project/xgboost/dmlc-core/cmake/build_config.h.in -> /home/hxer/Project/xgboost/dmlc-core/include/dmlc/build_config.h
-- Using nccl library: /usr/lib/x86_64-linux-gnu/libnccl_static.a
-- Found Nccl: /usr/include
-- Found OpenMP_C: -fopenmp
-- Found OpenMP_CXX: -fopenmp
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hxer/Project/xgboost/build
$ make -j12
...
[ 97%] Linking CXX shared library ../lib/libxgboost.so
[ 97%] Built target xgboost
[ 98%] Linking CUDA device code CMakeFiles/runxgboost.dir/cmake_device_link.o
[100%] Linking CXX executable ../xgboost
[100%] Built target runxgboost
$ cd ../python-package
$ python setup.py install
...
Finished processing dependencies for xgboost==0.83.dev0
$ pip install libgcc
$ ipython
In [1]: import xgboost as xgb
# Initialize XGBoostClassifier with GPU support.
In [2]: clf = xgb.XGBClassifier(colsample_bytree=0.4603, learning_rate=0.02, max_depth=4, tree_method
   ...: ='gpu_hist')

In [3]:
```

#### check

```sh
$ cd xgboost/demo/gpu_acceleration
$ python cover_type.py
Downloading https://ndownloader.figshare.com/files/5976039 [ sklearn.datasets]
```

参考资料：[XGBoost Installation Guide](<https://xgboost.readthedocs.io/en/latest/build.html#building-with-gpu-support>) 、[xgboost_python_install.md](<https://gist.github.com/pratos/de49be8ec53378145ea0df0a04ea7b25>): for cpu.

[NVIDIA Collective Communications Library (NCCL)](<https://developer.nvidia.com/nccl>). [deep learning sdk documentation](<https://docs.nvidia.com/deeplearning/sdk/nccl-install-guide/index.html>) 

[CMake 3.8.2 fails to configure minimal CUDA project](<https://gitlab.kitware.com/cmake/cmake/issues/16933>) : `CUDAHOSTCXX=g++-5`.

xgboost相关资料：

[Anthony Goldbloom gives you the secret to winning Kaggle competitions](https://www.import.io/post/how-to-win-a-kaggle-competition/) 

