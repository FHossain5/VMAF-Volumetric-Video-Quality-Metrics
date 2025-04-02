# Multiview Video Processing and Quality Assessment

## Overview
This document provides step-by-step instructions for processing 44 MP4 files to generate multiview videos, convert them to YUV format, apply compression, and evaluate quality metrics including VMAF, PSNR, SSIM, and MOS.

---

## 1. Generating Multiview Videos
We generate four views (front, back, left, and right) from each MP4 file using FFmpeg.

### **Commands:**
```bash
ffmpeg -i "{input_path}" -vf "stereo3d=sbsl:ml,scale=1280x720" -c:v libx264 -crf 18 -t 12 "{output_files['front']}"
ffmpeg -i "{input_path}" -vf "hflip,scale=1280x720" -c:v libx264 -crf 18 -t 12 "{output_files['back']}"
ffmpeg -i "{input_path}" -vf "crop=iw/2:ih:0:0,scale=1280x720" -c:v libx264 -crf 18 -preset slow -t 12 "{output_files['left']}"
ffmpeg -i "{input_path}" -vf "crop=iw/2:ih:iw/2:0,scale=1280x720" -c:v libx264 -crf 18 -preset slow -t 12 "{output_files['right']}"
```

---

## 2. Converting MP4 Files to YUV
Each MP4 file is converted into the YUV format using FFmpeg.

### **Command:**
```bash
ffmpeg -i "{input_path}" -pix_fmt yuv420p -c:v rawvideo "{output_path}"
```

---

## 3. Applying Compression
We apply VVC compression to the YUV files.

### **Command:**
```bash
vvencapp --input "{input_path}" --size 1280x720 --framerate 25 --format yuv420 --qp 25 --preset medium --output "{output_path}"
```

---

## 4. Converting VVC to Y4M
We decode the VVC-compressed file back into Y4M format.

### **Command:**
```bash
vvdecapp -b "F:\Dataset\.vvc_dataset\50_videos_different_background\loot_grey_vox10_03.vvc" -o "F:\Dataset\.vvc_dataset\loot_grey_vox10.y4m" --y4m
```

```bash
ffmpeg -i "G:\longdress\Longdress-y4m\geometry_and_texture_compression_L\geometry_and_texture_compression_l\R2\longdress_11_black_vox10.y4m" -pix_fmt yuv420p "G:\longdress\Longdress-y4m\geometry_and_texture_compression_L\geometry_and_texture_compression_l\R2\R2_420p\R2_longdress_black_11_vox10.y4m"
```

---

## 5. Converting MP4 to Y4M
This step converts MP4 files directly to Y4M format.

### **Command:**
```bash
ffmpeg -i "F:\Dataset\.mp4_dataset\50_videos_different_background\loot_vox10_grey_05.mp4" -pix_fmt yuv420p "F:\loot_grey_vox10.y4m"
```

---

## 6. Quality Assessment
After processing, the files are evaluated using multiple quality metrics:
- **[VMAF](./vmaf.md)** – Video Multi-Method Assessment Fusion
- **[FFmpeg LibVMAF](./ffmpeg_libvmaf.md)** – FFmpeg-based VMAF calculation
- **[PSNR](./psnr.md)** – Peak Signal-to-Noise Ratio
- **[SSIM](./ssim.md)** – Structural Similarity Index
- **[MOS](./mos.md)** – Mean Opinion Score from human evaluators

Each metric is detailed in its respective file linked above.

---

## Conclusion
This process ensures high-quality multiview video generation, compression, and evaluation. The provided scripts and commands automate the workflow for efficiency and reproducibility.

