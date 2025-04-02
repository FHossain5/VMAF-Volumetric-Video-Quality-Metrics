# PSNR (Peak Signal-to-Noise Ratio) Explanation

## What is PSNR?
PSNR (Peak Signal-to-Noise Ratio) is a widely used metric for measuring the quality of compressed or distorted video compared to a reference video. It expresses the ratio between the maximum possible power of a signal and the power of distorting noise that affects the quality of its representation. Higher PSNR values indicate better quality.

## Computing PSNR Using FFmpeg
To compute PSNR between a reference video and a compressed/distorted video, use the following FFmpeg command:

```sh
ffmpeg -i <reference_video>.y4m -i <distorted_video>.y4m -lavfi psnr -f null - 2> <log_file>.log
```

### Explanation of Command:
- `<reference_video>.y4m` → Specifies the original high-quality reference video.
- `<distorted_video>.y4m` → Specifies the compressed/distorted version.
- `-lavfi psnr` → Uses FFmpeg's PSNR filter to compute the PSNR values.
- `-f null -` → Ensures no output video is generated.
- `2> <log_file>.log` → Redirects the PSNR log output to a file for analysis.

## Example Command (Windows)
```sh
C:\ffmpeg\bin\ffmpeg.exe -i "D:\geometry_and_texture_compression_mp4\R1\soldier_grey_vox10.y4m" \
-i "D:\geometry_and_texture_compression_vvc\R1\420p_R1\R1_soldier_gtc_grey_vox10.y4m" \
-lavfi "psnr" -f null - 2> "D:\psnr_outputs\R1_soldier_gtc_grey_vox10_psnr.log"
```

## How to Interpret PSNR Results
The output log file contains PSNR values for the entire video. Important values to analyze:
- `average`: The overall average PSNR score (higher is better).
- `min`: The minimum PSNR value in the video.
- `max`: The highest PSNR value in the video.

### Example Output Log:
```
[Parsed_psnr_0 @ 0000023f8b7e3c40] PSNR y:35.52 u:41.23 v:42.01 avg:37.12 min:30.45 max:45.67
```
- `PSNR y`: Luminance (Y-channel) PSNR.
- `PSNR u, v`: Chrominance PSNR values.
- `avg`: The overall PSNR score.

## Using PSNR for Quality Evaluation
- A PSNR value above **40 dB** indicates excellent quality.
- A value between **30-40 dB** is acceptable for most applications.
- Below **30 dB** suggests noticeable quality degradation.

