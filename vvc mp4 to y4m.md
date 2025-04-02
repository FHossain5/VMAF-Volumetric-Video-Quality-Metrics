# VVC to Y4M Conversion

## Overview
This script explains the conversion of VVC (Versatile Video Coding) compressed video files into Y4M format, which is essential for quality assessment. The conversion is done using `vvdecapp` and `ffmpeg`.

## Step 1: Decode VVC to Y4M
To convert a VVC file to Y4M, use the following command:

```bash
vvdecapp -b "F:\Dataset\.vvc_dataset\50_videos_different_background\loot_grey_vox10_03.vvc" -o "F:\Dataset\.vvc_dataset\loot_grey_vox10.y4m" --y4m
```

Explanation:
- `-b`: Specifies the input VVC bitstream file.
- `-o`: Defines the output Y4M file.
- `--y4m`: Ensures that the output format is Y4M.

## Step 2: Standardize Y4M Format
After decoding, use FFmpeg to convert the Y4M file to a standardized pixel format:

```bash
ffmpeg -i "G:\longdress\Longdress-y4m\geometry_and_texture_compression_L\geometry_and_texture_compression_l\R2\longdress_11_black_vox10.y4m" -pix_fmt yuv420p "G:\longdress\Longdress-y4m\geometry_and_texture_compression_L\geometry_and_texture_compression_l\R2\R2_420p\R2_longdress_black_11_vox10.y4m"
```

Explanation:
- `-i`: Input Y4M file.
- `-pix_fmt yuv420p`: Converts the file to YUV 4:2:0 format, ensuring compatibility with analysis tools.
- The output file is stored in a structured directory.

---

# MP4 to Y4M Conversion

## Overview
MP4 files need to be converted to Y4M format for consistency in quality evaluation. The process is done using FFmpeg.

## Conversion Command
```bash
ffmpeg -i "F:\Dataset\.mp4_dataset\50_videos_different_background\loot_vox10_grey_05.mp4" -pix_fmt yuv420p "F:\loot_grey_vox10.y4m"
```

Explanation:
- `-i`: Specifies the input MP4 file.
- `-pix_fmt yuv420p`: Converts the video to YUV 4:2:0 format.
- The output file is saved in Y4M format, ready for quality analysis.

This ensures that both compressed VVC and MP4 videos are in a standardized format for further evaluation.
