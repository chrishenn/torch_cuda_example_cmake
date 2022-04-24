<h1 align="center" style="margin-top: 0px;">Build Cuda and Torch-C++ Extensions with Cmake</h1>

This provides a minimal framework to build a libtorch / cuda extension to our python application/script. With this project, we can verify that each component is compatible, configured and installed correctly, and is in the right place.

CMake is the preferred build system for Torch / libtorch extensions. CMake will detect the supported Nvidia compute capabilities of all Nvidia gpus on the system - and automatically build for those architectures as needed.

---


## Environment

It is crucial that the versions of the CUDA toolkit agree accross pytorch, libtorch, and the nvcc version used. Check the pytorch website to find out wich version of CUDA is used to build the pytorch binaries you have installed through your python environment manager. Your system version of CUDnn must be compatible with the CUDA version, and the Nvidia driver installed on your system must also be compatible; see the Nvidia compatibility matrices.

Here I'm using CUDA 11.1, pytorch / libtorch 1.8.2, CUDnn 8.4.0, gcc 9.4.0, and CMake 3.16.3.

To create a conda environment:

    conda env create -f env182.yml

Or, update an existing environment:

    conda env update -f env182.yml

This conda .yml specifies the python version for the environment, then calls "pip install -r env182.txt" for all packages.

---


## Set Paths in CMakeLists.txt
Modify the "CMAKE_PREFIX_PATH" in the CMakeLists.txt file to point to your libtorch folder.

    list(APPEND CMAKE_PREFIX_PATH "/home/chris/Documents/libtorch")

Or, you can override the path in the CMakeLists.txt by passing this flag with the cmake command, as in:

    cmake -DCMAKE_PREFIX_PATH=["/home/chris/Documents/libtorch"] ..

You may also need to specify paths to the correct versions of gcc / g++ / nvcc if your system has multiple versions installed. My compilers are the defaults on the system path, but you can specify full paths here in CMakeLists.txt:

    SET(CMAKE_C_COMPILER gcc)
    SET(CMAKE_CXX_COMPILER g++)
    SET(CMAKE_CUDA_COMPILER nvcc)

---


## Apptainer Build and Run

I'm running Apptainer 1.0.1 on my system. To install, see: [Apptainer Quick Start](https://apptainer.org/docs/user/main/quick_start.html)

Build an apptainer image from env182.def:

    sudo apptainer build ./env182.sif env182.def

Build the project in the container:

    ./install_appt.sh

Run the project in the container: 

    ./train_appt.sh

---


## Local Build and Run
    
The binary is put in the build/ dir and has 'lib' tacked onto the beginning of the filename.

    ./install.sh

To run:

    ./train.sh







