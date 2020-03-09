# 音视频转码与处理常用命令

视频裁剪
```
ffmpeg -ss 01:00:00 -i input.mp4 -codec copy -t 06:00 output.mp4
```

视频拼接
```
MP4Box -cat 1.mp4 -cat 2.mp4 concat.mp4
ffmpeg -f concat -i list.txt -c copy concat.mp4
```
其中list.txt的内容为：
```
file ./1.mp4
file ./2.mp4
```

视频缩放
```
ffmpeg -i input.mp4 -vf scale=w=1920:h=1080:force_original_aspect_ratio=decrease:flags=lanczos -c:v libx265 output.mp4
```

添加静态logo
```
ffmpeg -i input.mp4 -i logo.png -lavfi "overlay=W-54-w:54" -c:a copy -c:v libx265 -x265-params crf=22 output.logo.mp4
```

音视频合并
```
MP4Box -add video_file#video -fps 25 -add audio_file#audio -new mp4_file
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

增加静音轨(FFmpeg版本需要在v4.1.0之上)
```
ffmpeg -i video.mp4 -an -f lavfi -i anullsrc=channel_layout=stereo:sample_rate=44100 -c:v copy -shortest -f mp4 video.mute.mp4
```

计算PSNR, SSIM和VMAF
```
ffmpeg -i output.mp4 -i orignal.mxf -filter_complex "psnr=f=output.psnr.log;[0:v][1:v]ssim=f=output.ssim.log" -f null - > output.metric.log 2>&1
ffmpeg -i output.mp4 -i orignal.mp4 -lavfi libvmaf="model_path=release/model/vmaf_v0.6.1.pkl:log_path=output.vmaf.json:log_fmt=json" -f null - > output.metric.log 2>&1
```

