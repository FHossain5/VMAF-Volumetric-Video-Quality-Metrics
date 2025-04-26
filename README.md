# VMAF Volumetric Video Quality Metrics

This project provides simple, reliable scripts to convert volumetric videos into a common format and measure their quality. You can quickly see how different compression methods affect video clarity.

## What You’ll Find Here
- **Conversion Tools** to transform VVC and MP4 files into Y4M format
- **Multiview Processing** scripts to generate front, back, left, and right views from an MP4
- **Quality Metrics** examples: VMAF, PSNR, SSIM, and human-based MOS ratings

## Getting Started
1. **Install Requirements**
   - [FFmpeg](https://ffmpeg.org/) (make sure it has libvmaf enabled)
   - `vvencapp` and `vvdecapp` for VVC encoding/decoding
   - Netflix’s `vmaf` tool for detailed VMAF analysis
   - Python 3.x (for any helper scripts)

2. **Convert Videos to Y4M**
   - **VVC to Y4M**:
     ```bash
     vvdecapp -b input.vvc -o temp.y4m --y4m
     ffmpeg -pix_fmt yuv420p temp.y4m output.y4m
     ```
   - **MP4 to Y4M**:
     ```bash
     ffmpeg -i input.mp4 -pix_fmt yuv420p output.y4m
     ```

3. **Generate Multiview Projections**
   ```bash
   ffmpeg -i input.mp4 -vf "stereo3d=sbsl:ml,scale=1280x720" front.y4m
   ffmpeg -i input.mp4 -vf "hflip,scale=1280x720" back.y4m
   ffmpeg -i input.mp4 -vf "crop=iw/2:ih:0:0,scale=1280x720" left.y4m
   ffmpeg -i input.mp4 -vf "crop=iw/2:ih:iw/2:0,scale=1280x720" right.y4m
   ```

4. **Measure Quality**
   - **VMAF (command-line)**:
     ```bash
     vmaf --reference ref.y4m --distorted dist.y4m --output score.json --json
     ```
   - **FFmpeg + libvmaf**:
     ```bash
     ffmpeg -i ref.y4m -i dist.y4m \
       -filter_complex "[0:v][1:v]libvmaf=log_fmt=json:log_path=out.json" -f null -
     ```
   - **PSNR**:
     ```bash
     ffmpeg -i ref.y4m -i dist.y4m -lavfi psnr -f null - 2> psnr.log
     ```
   - **SSIM**:
     ```bash
     ffmpeg -i ref.y4m -i dist.y4m -lavfi ssim -f null - 2> ssim.log
     ```
   - **MOS**:
     Collect ratings from human evaluators (scale 1–5) and average their scores.

## Examples
- Quickly convert a VVC file and compute SSIM in one go.
- Generate all four views from a single MP4.
- Compare multiple compression settings side by side.


## Detailed Documentation
For in-depth guides, see:
- [VMAF CLI Usage](vmaf.md)
- [FFmpeg with libvmaf](ffmpeg_libvmaf.md)
- [PSNR Computation](ffmpeg_psnr.md)
- [SSIM Computation](ffmpeg_ssim.md)
- [Mean Opinion Score (MOS)](mos.md)
- [Multiview Processing](multiview_processing.md)
- [VVC & MP4 to Y4M Conversion](vvc_mp4_to_y4m.md)


