# EBS Volume

lsblk
lsblk -f

sudo file -s /dev/xvdb
sudo mkfs -t xfs /dev/xvdb

sudo mount /dev/xvdb /mnt/volume/

# Development Tools

sudo yum groupinstall "Development Tools"
sudo yum install mesa-libOpenCL-devel.x86_64

# Drivers

chmod +x NVIDIA-Linux-x86_64-535.86.10.run 
sudo ./NVIDIA-Linux-x86_64-535.86.10.run 

# Build & Run

g++ ./src/*.cpp -o ./bin/FluidX3D -std=c++17 -pthread -I./src/OpenCL/include -L./src/OpenCL/lib -lOpenCL
./bin/FluidX3D 