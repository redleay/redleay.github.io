# 音视频转码与处理常用命令

视频裁剪
```
ffmpeg -ss 01:00:00 -i input.mp4 -codec copy -t 06:00 output.mp4
```

视频拼接
```
ffmpeg -f concat -i list.txt -c copy concat.mp4
```
其中list.txt的内容为：
```
file ./1.mp4
file ./2.mp4
```

音视频合并
```
MP4Box -add video_file#video -add audio_file#audio -new mp4_file
```

提取视频码流
```
MP4Box test.mp4 -raw 1  # 提取轨道1，生成test_track1.xxx
ffmpeg -i hevc.mp4 -an -vcodec copy -f hevc bitstream.265
ffmpeg -i h264.mp4 -an -vcodec copy -f h264 bitstream.264
ffmpeg -i in.mp4 -c:v copy -bsf hevc_mp4toannexb out.h265
ffmpeg -i in.mp4 -c:v copy -bsf h264_mp4toannexb out.h264
```

提取音频码流
```
ffmpeg -i test.mp4 -map 0:0 -c:a copy -vn out.ec3
```

提取音视频信息
```
mediainfo --Inform="Video;%Duration%,%BitRate%" input.mp4
```

混音(多声道向下混成2声道)
```
ffmpeg -i db.wav -c:a pcm_s24le -ac 2 db.ac2.wav
ffmpeg -i db.wav -af "pan=stereo | FL < FL + 0.5*FC + 0.6*BL + 0.6*SL | FR < FR + 0.5*FC + 0.6*BR + 0.6*SR" db_stereo_DIY.wav
ffmpeg -i "xxxx" -map 0:v -vcodec libx264 -b:v 15000k -filter_complex "[0:1][0:2][0:3][0:4][0:5][0:6[0:7][0:8] amerge=inputs=8" -acodec libfdk_aac -b:a 384k -strict -2 -y "xxxx"
```

MP4Box编译
```
./configure --static-mp4box --enable-debug
```

x265 cmake增加-pg编译和链接选项，为了做gprof profiling，需要使用静态编译，动态编译无法分析动态库的函数耗时
```
cmake -DCMAKE_INSTALL_PREFIX=../bin/debug/ -DCMAKE_BUILD_TYPE=Debug -DENABLE_SHARED=OFF -DCMAKE_C_FLAGS=-pg -DCMAKE_CXX_FLAGS=-pg -DCMAKE_EXE_LINKER_FLAGS=-pg -DCMAKE_SHARED_LINKER_FLAGS=-pg -G "Unix Makefiles" ../source/
```
