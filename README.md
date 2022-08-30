<div align='center'>
  <img src="./assets/skippy-logo.png">
</div>

Skip.py is a video editing Python script. Based on a silent threshold, it can automatically speed up silent sections of a video, or cut them completely. It uses `ffmpeg` under the hood to process video and audio information.

![](assets/skippy-test.png)

It's based off of [carykh's jumpcutter](https://www.github.com/carykh/jumpcutter), but it has a full built in command line interface to let the user decide whether it wants to process the video or not, showing an estimate of the minimum possible time after the time warping. It also autodetects the input's framerate and samplerate using `ffprobe` to avoid errors. It also uses [`ffpb`](https://www.github.com/althonos/ffpb) for tracking the progress of `ffmpeg`.



# Requirements

- A working Python installation.
  You may need to install aditional libraries. (See `skip.py` for the imports).

- A working FFMPEG installation added to `PATH`.



# Usage

```powershell
python .\skip.py --input_file 'path/to/video.mp4' --silent_threshold 0.11 --frame_margin 1 --frame_quality 3
```

Args:
- `--h` for help
 - `--input_file`: Input file to be modified.
 - `--silent_threshold`: A value between 0 and 1. It determines the sections to be sped up. Default value: 0.12
 - `--frame_margin`: A frame margin for smoothing out the transitions. Default value: 1
 - `--sounded_speed`: The new speed of the loud portions of the video. Default value: 1.0
 - `--silent_speed`: The new speed of the silent portions of the video.  999999 cuts the sections entirely. Default value: 5.0
 - `--output_file`: The output file. By default its `[yourfile]_ALTERED.mp4`
 
 If the video gets loaded up correctly, the output should be something like:
 
 ```powerhsell
 skippy
https://www.github.com/Joan-GQ/skippy


Input file: video.mp4
Silent threshold: 0.11
Frame margin: 1.0
Frame quality: 3
Sounded speed: x1.0
Silent speed: x5.0
Output file: video_ALTERED.mp4
Detected framerate: 30.0 FPS
Detected samplerate: 44100 Hz

Processing chunks: 100%|█████████████████████████████████████████████████████| 8.99k/8.99k [00:00<00:00, 72.0k chunk/s]
Processing frame spreadage: 100%|█████████████████████████████████████████████| 8.99k/8.99k [00:00<00:00, 198k frame/s]
Input time = 4.997 minutes
Skippy'd = 3.113 minutes. 62.3% of total duration. Reduced by 1.884 minutes.
```

The green and red bar is an approximated version of the video. It indicates which portions of the video have been marked as 'silent' (In red) or 'loud' (In green). The `Skippy'd` time, is the new estimated time after deleting the silent portions.

*Note that if the silent speed is not that fast, the actual time will be noticeably different that the estimate.*
