# 多媒体常识


HLS:
HTTP Live Streaming, 索引文件为m3u8，数据文件原为ts，目前也支持fmp4，原来只支持H.264，后增加支持H.265

DASH:
Dynamic Adaptive Streaming over HTTP, 索引文件为mpd，数据文件支持fmp4和ts，对编码格式无限制

mpd : Media Presentation Description
fmp4: Fragmented MP4

HLS with fmp4:
Apple增加HLS对fmp4的支持后，由于DASH也支持fmp4，HLS和DASH可以共用fmp4文件，不再需要分别存储两份视频数据，节省了存储空间。

Fmp4与mp4区别:
mp4只包含一个巨大的mdat box，不方便seek码流位置和切换流。fmp4包含一个sidx box和一系列的moof+mdat box，一般使用固定的时间段来划分fragment，方便关键帧对齐和seek码流位置，更加适合于切换不同码流和清晰度的流的场景

ISO/IEC 14496-15标准文档针对HEVC定义了hvc1与hev1两种封装格式，两者的区别在于：
hvc1: VPS/SPS/PPS只能出现在码流最前面
hev1: VPS/SPS/PPS可以出现在码流中间

声道正常顺序
```
L R C LFE Ls Rs          # 5.1声道
L R C LFE BL BR          # 5.1声道
L R C LFE Ls Rs Lrs Rrs  # 7.1声道
```
多声道音轨名称对应关系
```
L = (Front) Left
R = (Front) Right
C = Center
LFE = Low Frequency Effects
Ls = Left Surround (Rear Left)
Rs = Right Surround (Rear Right)
Lrs = Left Rear Surround
Rrs = Right Rear Surround

Lc = Left Center
Rc = Right Center
Lm = Left Mid
Rm = Right Mid
S = Surround (Rear Center)
```

