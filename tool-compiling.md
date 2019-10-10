# 音视频转码与处理常用命令

GLIBC 2.18编译和安装
```
wget http://mirrors.ustc.edu.cn/gnu/libc/glibc-2.18.tar.gz
tar -zxvf glibc-2.18.tar.gz
cd glibc-2.18
mkdir build
cd build
../configure --prefix=/usr
make -j4
sudo make install
```

MP4Box编译
```
./configure --static-mp4box --enable-debug
```

x265 cmake增加-pg编译和链接选项，为了做gprof profiling，需要使用静态编译，动态编译无法分析动态库的函数耗时
```
cmake -DCMAKE_INSTALL_PREFIX=../bin/debug/ -DCMAKE_BUILD_TYPE=Debug -DENABLE_SHARED=OFF -DCMAKE_C_FLAGS=-pg -DCMAKE_CXX_FLAGS=-pg -DCMAKE_EXE_LINKER_FLAGS=-pg -DCMAKE_SHARED_LINKER_FLAGS=-pg -G "Unix Makefiles" ../source/
```

