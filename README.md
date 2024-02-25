# TeacherCast
Shares Teacher Screen to network

# Features
- No installation needed
- Free
- Open Source
- 3-step, 5-min to only-once initial setup
- Clients can view Teacher Screen through any Browser
  
# How it works
On teacher computer:
  - Run standalone, open-source FFMPEG.exe command to stream local desktop to local Media Server
  - Run standaloone, open-source local Media Server (MediaMTX.exe)

On clients (students) device:
  - Open a browser to "http://Teacher_IP:8889/stream".
![how](https://github.com/blanes/TeacherCast/assets/3591929/9e5a1afc-0a0f-40e7-8a90-441f4f6ed64b)

# Protocols involved
1) FFMPEG.EXE -> MediaMTX.exe: UDP
2) Client Browser -> MediaMTX.exe: WebRTC


# stream.bat. Command script to execute. Contains full instructions.

@echo off__
::__
:: TeacherCast (Windows Version).__
::__
:: Shares Teacher's screen to Network, through a local Media Server.__
:: Any browser (student) can view, at the address: http://Teacher_IP:8889/stream
::
:: PREREQUISITES - BEGIN:
::
:: - Create a folder (in you Teacher Computer, or in Flash Drive, or in network folder...)
:: 
:: - PUT the following 4 files on it:
::
:: - 1) Download FFMPEG.EXE for Windows from:
::	https://www.ffmpeg.org/download.html#build-windows
::
:: - 2) Download Media Server (MediaMTX.EXE) from:
::	https://github.com/bluenviron/mediamtx/releases (Select last *Windows_amd64* and unzip)
::
:: - 3) From the same above ZIP, extract config file: MediaMTX.yml
::	Edit this file, just appending the following text at the end:
::	"paths:
::         stream:
::            source: udp://127.0.0.1:1234"
::
:: -> (OPTIONAL) you can also save resources disabling unused protocols on MediaMTX.yml, setting:
::    rtsp: no
::    rtmp: no
::    hls: no
::    srt: no
:: 
::
:: - 4) PUT this "stream.bat" file on the same folder.
::
::
:: PREREQUISITES - END
::
::
:: **** ALL DONE! NOW BEGIN SERVING: !! ****
::	
Set ROOT=%~dp0%
::
:: 1) Add Firewall rule to allow MediaMTX app. This has to be executed ELEVATED:
::
netsh advfirewall firewall show rule name="MediaMTX"
if errorlevel 1 goto ADDRULE
goto CONTINUE
:ADDRULE
netsh advfirewall firewall add rule name="MediaMTX" dir=in action=allow program="%~dp0%mediamtx.exe" enable=yes
:CONTINUE
::
:: 2) Starts Local Media Server:
start %ROOT%mediamtx.exe
::
:: 3) Stream desktop to Local Media Server:
start %ROOT%ffmpeg -f gdigrab -i desktop -c:v libx264 -preset ultrafast -f mpegts udp://127.0.0.1:1234?pkt_size=1316
::
:: 
:: *** AT THIS POINT YOU ARE CASTING TEACHER SCREEN AND CAN CAPTURE IT FROM BROWSERS: ***
::
::	-> OPEN A BROWSER IN YOUR NETWORK AND ENTER THE FOLLOWING URL:
::	-> "http://TEACHER_IP:8889/stream"
::
::	** can last 10 seconds or so to begin showing content, due to buffering.
::	** minimal delay can occur (between 0.2-1.5s) depending on number of clients connected.
::


stream.bat…]()
