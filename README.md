## Description
This is a fixed version of the dlib library source for own needs.

## Dependencies

#### General
- gcc & g++ version 8 and below.

#### With CUDA support
- cuda
- cudnn
- cublas

## Building & Installation
#### Preparing
Before building, add following lines to **setup.py** file:
````PYTHON
import sys
os.environ["CC"] = "gcc-{your_version}"
````
Notice that **{your_version}** must be manually changed to your gcc compiler version number.

#### With CUDA support:
If you have another path of **CMAKE_PREFIX_PATH** and **CUDA_HOST_COMPILER** options, you must change it.
````BASH
mkdir build && cd build

cmake .. \
    -DCUDA_HOST_COMPILER=/usr/bin/gcc-{your_version} \
    -DCMAKE_PREFIX_PATH=/usr/lib/x86_64-linux-gnu/ \
    -DDLIB_USE_CUDA=1 \
    -DUSE_AVX_INSTRUCTIONS=1 \
    -DUSE_F16C=1

cmake --build . --config Release -j($nproc)
sudo ldconfig

cd ..

python setup.py install \
      --record files.txt \
      --compiler-flags "-DCUDA_HOST_COMPILER=/usr/bin/gcc-{your_version}" \
      --yes USE_AVX_INSTRUCTIONS \
      --yes DLIB_USE_CUDA \

````
