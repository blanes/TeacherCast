# TeacherCast
Shares Teacher Screen to network

# Features
- No installation needed
- Free
- Open Source
- 3-step, 5-min to inicital setup
- Clients can view Teacher Screen through any Browser
  
# How it works
On teacher computer:
  - Run standalone, open-source FFMPEG.exe command to stream local desktop to local Media Server
  - Run standaloone, open-source local Media Server (MediaMTX.exe)

On clients (students) device:
  - Open a browser to "http://Teacher_IP:8889/stream".
![how](https://github.com/blanes/TeacherCast/assets/3591929/31753a92-a206-4d37-bed6-8c480f4a3c88)

# Protocols involved
1) FFMPEG.EXE -> MediaMTX.exe: UDP
2) Client Browser -> MediaMTX.exe: WebRTC
