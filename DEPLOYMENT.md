# EBS Volume

lsblk
lsblk -f

sudo file -s /dev/xvdb
sudo file -s /dev/sdb
sudo mkfs -t xfs /dev/xvdb
sudo mkfs -t xfs /dev/sdb

sudo mount /dev/xvdb /mnt/volume/
sudo mount /dev/sdb /mnt/volume/

# Development Tools

sudo yum groupinstall "Development Tools"
sudo yum install mesa-libOpenCL-devel.x86_64

# Drivers

sudo dnf install kernel-modules-extra

chmod +x NVIDIA-Linux-x86_64-535.86.10.run 
sudo ./NVIDIA-Linux-x86_64-535.86.10.run

nvidia-smi

# Build & Run

g++ ./src/*.cpp -o ./bin/FluidX3D -std=c++17 -pthread -I./src/OpenCL/include -L./src/OpenCL/lib -lOpenCL
g++ ./src/*.cpp -o ./bin/FluidX3D_X_Wing -std=c++17 -pthread -I./src/OpenCL/include -L./src/OpenCL/lib -lOpenCL
g++ ./src/*.cpp -o ./bin/FluidX3D_Concord -std=c++17 -pthread -I./src/OpenCL/include -L./src/OpenCL/lib -lOpenCL
g++ ./src/*.cpp -o ./bin/FluidX3D_TIE -std=c++17 -pthread -I./src/OpenCL/include -L./src/OpenCL/lib -lOpenCL
g++ ./src/*.cpp -o ./bin/FluidX3D_R_Fan -std=c++17 -pthread -I./src/OpenCL/include -L./src/OpenCL/lib -lOpenCL

./bin/FluidX3D 

# Video

ffmpeg -pattern_type glob -i "*/image-*.png" -pix_fmt yuv420p FluidX3D_F1_670_7E6.mp4
ffmpeg -i FluidX3D_F1_670_7E6.mp4 -i Formula\ 1\ \(First\ Export\).wav -shortest -c:v copy -map 0:v:0 -map 1:a:0 -c:a aac -b:a 192k FluidX3D_F1_670_7E6_wAudio.mp4
ffmpeg -i FluidX3D_F1_670_7E6_wAudio.mp4 -r 40 FluidX3D_F1_670_7E6_Twitter.mp4
ffmpeg -i FluidX3D_F1_670_7E6_Twitter2.mp4 -vcodec libx264 -crf 28 FluidX3D_F1_670_7E6_Twitter28.mp4

ffmpeg -pattern_type glob -i "*/image-*.png" -pix_fmt yuv420p FluidX3D_X_Wing.mp4
ffmpeg -framerate 60 -pattern_type glob -i "*/image-*.png" -pix_fmt yuv420p FluidX3D_X_Wing.mp4
ffmpeg -framerate 60 -pattern_type glob -i "*/image-*.png" -c:v libx264 -pix_fmt yuv420p -b:v 24M FluidX3D_X_Wing.mp4
ffmpeg -i FluidX3D_X_Wing_15100MB_NU7E4.mp4 -i The\ Force\ \(Piano\ \&\ Strings\)\ \[Mastered\].mp3 -shortest -c:v copy -map 0:v:0 -map 1:a:0 -c:a aac -b:a 192k FluidX3D_X_Wing_15100MB_NU7E4_WA.mp4
ffmpeg -i FluidX3D_X_Wing_15100MB_NU7E4_WA.mp4 -r 30 FluidX3D_X_Wing_15100MB_NU7E4_30FPS.mp4