The program works on Ubunutu 14.04, 15.04 and 15.10 with gcc 4.8 and later version (tested with gcc 5.2).

In the workspace, there should be four other folders, namely, dataset, query, dataset_sim and query_sim, containing database images, query images, descriptors for database images and descriptors for query images, respectively. Due to the limitation of the uploaded file size, they are not uploaded to github. It should be noticed that the folders with "_sim" should be left empty before runing the program because the sift files are expected to be generated after runing the program. It should always be fine to have generated sift files inside the dataset_sim folder for future usage which is the offline part of the program.

To install the dependencies,
make sure the programs are installed either in subfolders of usr/ or subfolders of /usr/local

1. install cuda
cuda 6.5 together with nVidia driver 340 has been tested.
For computers without cuda, you should go to src/imret/imretFuncs.hpp and change in function simprep_gpu 
from char * argv[] = {"-fo", "-1","-v", "0","-b", "1","-cuda"} 
to char * argv[] = {"-fo", "-1","-v", "0","-b", "1"}
To use siftgpu, 
sudo cp imretOpenMVG/src/thirdparty/SiftGPU/bin/libsiftgpu.so /usr/lib

2. install openmvg (https://github.com/openMVG/openMVG.git)
openMVG itself includes most of the dependencies such as eigen and stlplus3.
After openMVG being installed on the local machine, there is a bug that makes the nonFree library cannot be included correctly. To fix it:
sudo mkdir /usr/local/include/openMVG_dependencies/nonFree/sift
sudo cp -r vl sift
sudo cp SIFT_describer.hpp sift

3. install flann (https://github.com/mariusmuja/flann.git)

4. install qt5

5. install libconfig++
sudo apt-get install libconfig++-dev

6 install cmake
sudo apt-get install cmake

To compile,
in imretOpenMVG,
mkdir build
cd build
cmake . ../src
make

There might be several warnings during the compiling process which is fine.

When running the program, one should use the generated "main" file in the build folder.
An example to run it could be:
cd build
./main

Then a window form pops up. 

Possible issues for Ubuntu 14.04
If you encounter the error "/usr/lib/gcc/x86_64-linux-gnu/4.8/../../../../lib/libsiftgpu.so: undefined reference to `std::__throw_out_of_range_fmt(char const*, ...)@GLIBCXX_3.4.20'" or something similar, you need to upgrade libstdc++.
Following commands solve this problem:
sudo apt-get install libstdc++6 (do this if libstdc++ was not installed)
sudo add-apt-repository ppa:ubuntu-toolchain-r/test 
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade

