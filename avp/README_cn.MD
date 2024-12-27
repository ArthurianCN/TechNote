# 音视频知识

<p ##align="center">
  <a href="./README_cn.md">简体中文 |
  <a href="./README.md">English</a>
</p>

## MPEG-TS
MPEG-TS 是一个音频和视频的传输协议，它被设计用来传输音频和视频数据。MPEG-TS 由多个 PES 包组成，每个 PES 包包含一个音频或视频帧。
MPEG-TS 每个包固定 188 字节，每个包由 TS 头和 TS 负载数据组成。


### TS 头部结构
1. 同步字（sync_byte）: 8 位，固定为 0x47。
2. 传输流 ID（transport_error_indicator, transport_priority, transport_scrambling_control, adaptation_field_control, continuity_counter）: 12 位，用于标识传输流 ID，以及是否包含 adaptation field 和 payload。
3. PID（program_number）: 13 位，用于标识 PID，每个PID 对应一个音频或视频流。

### PAT 包
PAT 包是节目关联表，它包含了所有的节目和对应的 PID。PAT 包的 pid 是 0x00，table_id 是 0x00。


### PMT 包
PMT 包是节目映射表，它包含了所有的节目和对应的 PID，table_id 是 0x02。


### 解析方法：
#### 基本思路
1. 找到 pid 是 0x00 的TS 包，这是 PAT 包，从中找到所有的 PMT 包的 pid。
2. 根据 PMT 包的 pid，找到对应的 PMT 包，从中找到所有的 PES 包的 pid，其中 stream_type 是 0x1B 的是H264，H265 的是 0x24。
3. 根据 PES 包的 pid，找到对应的 PES 包，从中解析出音频或视频帧。




<p ##align="center">
  <a href="./README.md">English |
  <a href="./README_cn.md">简体中文</a>
</p>