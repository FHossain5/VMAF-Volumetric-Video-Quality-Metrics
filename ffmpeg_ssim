# SSIM (Structural Similarity Index) Evaluation using FFmpeg

## Overview
The Structural Similarity Index (SSIM) is a metric used to assess the quality of compressed or distorted images and videos in relation to their original versions. It evaluates structural similarities rather than pixel-wise differences, making it more aligned with human perception.

This script utilizes `FFmpeg` to compute SSIM values for volumetric videos that have been compressed using VVC and MP4 formats. 

## Prerequisites
Ensure that `FFmpeg` is installed and accessible via the command line. Download it from [FFmpeg's official website](https://ffmpeg.org/download.html) if needed.

## Input Data
- **Reference Video:** The original uncompressed Y4M video.
- **Distorted Video:** The compressed version of the reference video.
- **Output Log File:** A text file storing SSIM values.

## FFmpeg Command to Compute SSIM
```python
import subprocess

def compute_ssim(ffmpeg_path, ref_file, dist_file, log_file):
    command = [
        ffmpeg_path,
        "-i", ref_file,
        "-i", dist_file,
        "-lavfi", "ssim",
        "-f", "null", "-",
        "2>", log_file  # Redirect stderr (log output) to file
    ]
    
    process = subprocess.run(" ".join(command), shell=True, capture_output=True, text=True)
    if process.returncode == 0:
        print("SSIM computation successful. Log saved to", log_file)
    else:
        print("Error computing SSIM:", process.stderr)
```

## Usage
Modify the script according to your file paths and execute:
```python
ffmpeg_path = "C:/ffmpeg/bin/ffmpeg.exe"
ref_file = "D:/geometry_and_texture_compression_mp4/R1/loot_black_11_vox10.y4m"
dist_file = "D:/geometry_and_texture_compression_vvc/R1/420p_R1/R1_loot_gc_black_11_vox10.y4m"
log_file = "D:/ssim_outputs/R1_loot_gc_black_11_vox10_ssim.txt"

compute_ssim(ffmpeg_path, ref_file, dist_file, log_file)
```

## Explanation of the Command
- `-i <input>`: Specifies the reference and distorted video inputs.
- `-lavfi "ssim"`: Uses FFmpeg's SSIM filter for quality evaluation.
- `-f null -`: Discards the processed output as the goal is quality measurement.
- `2> log_file`: Redirects SSIM results to a log file.

## Example Log Output
A sample SSIM result from `R1_loot_gc_black_11_vox10_ssim.txt`:
```
SSIM Y:0.975432 (12.34db) U:0.988234 (15.56db) V:0.987654 (15.34db) All:0.982154 (14.00db)
```
- `SSIM Y`: Luminance component quality score.
- `SSIM U & V`: Chrominance component quality scores.
- `All`: Overall SSIM score, higher values indicate better quality.

## Notes
- Ensure the reference and distorted files exist at the specified paths.
- If FFmpeg throws an error like `No such file or directory`, check that the file paths are correct.

## Conclusion
This script automates SSIM computation for VVC and MP4 compressed Y4M videos, helping assess video compression quality using a perceptually relevant metric.
