# Description 
Decode `message` from the moon.
# Hints
- How did pictures from the moon landing get sent back to Earth?
- What is the CMU mascot?, that might help select a RX option
# Solution
The audio isn't morse code so first I googled how the images captured from the moon are transmitted back to earth. Most of the webpages mentioned "TV Scan". In [wikipedia](https://en.wikipedia.org/wiki/Apollo_11_missing_tapes), the article about Apollo 11 mentioned `slow-scan television (SSTV)` which transmits and receives still images over radio frequenices.
So, I looked up how to use sstv online and got a [webpage](https://ourcodeworld.com/articles/read/956/how-to-convert-decode-a-slow-scan-television-transmissions-sstv-audio-file-to-images-using-qsstv-in-ubuntu-18-04) which showed how to do it on linux.
The first hint tells us that SSTV has to be used and when I copy pasted the 2nd hint in google, it showed Scotty/Scottie which I later found out that it is the mode that I have to use in qsstv. 
## Commands: 
```
1) sudo apt-get install qsstv
2) yasho@DESKTOP-6ND4URA:~$ qsstv
3) yasho@DESKTOP-6ND4URA:~$ pactl load-module module-null-sink sink_name=virtual-cable
```
Output: 

Command 'pactl' not found, but can be installed with:

sudo apt install pulseaudio-utils
```
4) yasho@DESKTOP-6ND4URA:~$ sudo apt-get install pavucontrol
5) yasho@DESKTOP-6ND4URA:~$ pavucontrol
6) yasho@DESKTOP-6ND4URA:~$ pactl load-module module-null-sink sink_name=virtual-cable
```
Output: 22
```
7) yasho@DESKTOP-6ND4URA:~$ qsstv &
8) yasho@DESKTOP-6ND4URA:~$ pavucontrol &
9) yasho@DESKTOP-6ND4URA:~$ paplay -d virtual-cable /mnt/c/Users/hvpan/Downloads/messages.wav
```
![Screenshot (4608)](https://github.com/user-attachments/assets/56e8b302-194b-45e2-85dd-c06b25af801e)
# Flag
>picoCTF{beep_boop_im_in_space}

# Explanation: 
the 1st and 4th commands are for installing the `qsstv` and `pavucontrol` (PulseAudio Volume Control) softwares respectively. The 2nd and 5th commands run the softwares respectively. 

_Command 3_:

```
pactl load-module module-null-sink sink_name=virtual-cable
```
**What it does**: This command creates a virtual audio sink (a type of audio output) named "virtual-cable."

**Breaking it down**:

**pactl**: This is a command-line tool to control the PulseAudio sound server.

**load-module**: This tells PulseAudio to load a specific module.

**module-null-sink**: This is the module that creates a virtual audio output.

**sink_name=virtual-cable**: This specifies the name of the virtual audio output you’re creating, which will be referred to as "virtual-cable."

**Output Explanation**: The output message indicates that the command pactl is not found, meaning the system does not have the PulseAudio utilities installed yet.

It worked after installing pavucontrol. After setting everything up with the help of website, I ran qsstv and pavucontrol in bg so that I can run them both simultaneously and then play the wav audio file too.
The last command plays the audio file which is received by qsstv.

_Command 9_: `paplay -d virtual-cable /mnt/c/Users/hvpan/Downloads/messages.wav`

**What it does**: This command plays an audio file through the virtual audio sink you created earlier.

**Breaking it down**:

**paplay**: This command plays audio files using PulseAudio.

**-d virtual-cable**: This specifies that the audio should play through the "virtual-cable" you set up.

**/mnt/c/Users/hvpan/Downloads/messages.wav**: This is the path to the WAV audio file.

# Understanding Virtual Audio Sinks and Scottie 1 in SSTV

## Virtual Audio Sink

A **virtual audio sink** is a software-based audio output that allows audio data to be routed or redirected to a virtual channel rather than to a physical sound device (like speakers or headphones). This is particularly useful in audio processing, streaming, and recording applications. Here's how it works:

- **Purpose**: Virtual audio sinks enable applications to send audio to a virtual output, which can then be captured or processed by other software instead of being played out loud. This is beneficial for tasks like mixing, recording, or transmitting audio without actually producing sound through speakers.

- **Use Cases**: Common uses include:
  - **Audio Routing**: Sending audio from one application to another (e.g., routing audio from a media player into a streaming application).
  - **Recording**: Capturing audio output from applications without needing a physical microphone.
  - **Signal Processing**: Analyzing or modifying audio before it reaches the final output device.

## Command Breakdown: `pactl load-module module-null-sink sink_name=virtual-cable`

This command specifically creates a virtual audio sink in the PulseAudio sound server. Let’s break it down:

1. **`pactl`**: This is a command-line utility used to interact with the PulseAudio sound server, allowing you to control audio settings and devices.

2. **`load-module`**: This command instructs PulseAudio to load a specific module, which adds functionality to the audio server.

3. **`module-null-sink`**: This is the specific module being loaded. The `null-sink` module creates a virtual audio output that does not connect to any physical hardware. Instead, it allows audio to be sent to this virtual sink.

4. **`sink_name=virtual-cable`**: This parameter assigns a name to the newly created virtual audio sink. In this case, it’s named "virtual-cable." You can use this name later to refer to this audio sink when routing audio.

### How the Command Works
When you run this command:
- A virtual audio sink called "virtual-cable" is created.
- Applications can now send audio to "virtual-cable" instead of a physical output.
- You can use tools like `pavucontrol` to manage and monitor audio going through this virtual sink.

## Scottie 1 in SSTV

**Scottie 1** is one of the many modes used in SSTV for transmitting still images over radio. Here’s an overview of what it is and how it works:

- **Transmission Format**: Scottie 1 is a specific SSTV format that defines how the image data is encoded and transmitted. It’s known for a good balance between image quality and transmission speed, making it suitable for real-time SSTV communication.

- **Resolution and Quality**: The Scottie 1 mode typically has a resolution of 128x128 pixels and uses a color palette to encode images. This allows for reasonable quality while keeping transmission time relatively short.

- **Usage**: When you set QSSTV to use Scottie 1 mode, the software will expect to receive images that are transmitted in this specific format. It will decode the incoming audio signals into a still image using the Scottie 1 encoding scheme.

- **Compatibility**: This mode is commonly used among amateur radio operators and is supported by many SSTV applications, making it popular for transmitting images during contests, special events, or casual communication.

## Summary
- A **virtual audio sink** like the one created with `pactl load-module module-null-sink sink_name=virtual-cable` allows audio to be sent to a non-physical output for processing, recording, or routing purposes.
- **Scottie 1** is a specific SSTV mode designed for efficient image transmission, balancing quality and speed, and is widely used in amateur radio for sharing images.

