# FFmpeg with libvmaf for Video Quality Assessment

## Introduction
This document explains how to use **FFmpeg with libvmaf** to compute VMAF (Video Multi-Method Assessment Fusion) scores for compressed video files. We are working with:
- **Compressed VVC Y4M files** (encoded using VVC compression)
- **Compressed MP4 Y4M files** (standard MP4 format converted to Y4M)

FFmpeg provides an easy way to calculate **VMAF scores** between a reference video and a distorted (compressed) version.

---

## **Installing FFmpeg with libvmaf**
To use FFmpeg with libvmaf, ensure that you have FFmpeg installed with **libvmaf** enabled.

### **Installation Steps for Windows**
1. **Download FFmpeg**:
   - Get the latest static build from [FFmpeg official website](https://ffmpeg.org/download.html).
   - Extract the downloaded ZIP file to `C:\ffmpeg`.
2. **Verify Installation:**
   - Open Command Prompt (`cmd`) and run:
     ```sh
     C:\ffmpeg\bin\ffmpeg.exe -version
     ```
   - Ensure that **libvmaf** is included in the build.

---

## **Running FFmpeg with libvmaf for VMAF Score Calculation**
We compare a **reference Y4M video** (high-quality) with a **compressed Y4M video** (VVC-encoded) using FFmpeg’s libvmaf filter.

### **Command to Run FFmpeg with libvmaf**
```sh
"C:\ffmpeg\bin\ffmpeg.exe" -v verbose -i "D:\geometry_and_texture_compression_mp4\R1\soldier_grey_vox10.y4m" -i "D:\geometry_and_texture_compression_vvc\R1\420p_R1\R1_soldier_gtc_grey_vox10.y4m" -filter_complex "[0:v][1:v]libvmaf=log_fmt=json:log_path='D\:\\vmaf_outputs\\R1_soldier_gtc_grey_vox10_ffmpeg.json'" -f null -
```

### **Explanation of Command:**
- **`-i "input_file.y4m"`** → Specifies the input video files:
  - First input (`[0:v]`): The **reference video** (original, uncompressed)
  - Second input (`[1:v]`): The **distorted video** (compressed version)
- **`-filter_complex "[0:v][1:v]libvmaf=log_fmt=json:log_path='output.json'"`** → Runs the **libvmaf** filter to compute VMAF scores:
  - `log_fmt=json`: Saves the results in JSON format.
  - `log_path='D:\vmaf_outputs\R1_soldier_gtc_grey_vox10_ffmpeg.json'` → Specifies the output path for the JSON file.
- **`-f null -`** → Discards the output video since we only need the VMAF scores.

---

## **Understanding the VMAF Output JSON**
The output file (`.json`) contains detailed quality assessment scores. Key values include:
- **VMAF_score** → The final quality score (ranges from 0 to 100; higher is better).

---

## **Interpreting VMAF Scores**
| **VMAF Score** | **Perceived Quality** |
|--------------|------------------|
| 90 – 100    | Excellent        |
| 70 – 89     | Good             |
| 50 – 69     | Fair             |
| Below 50    | Poor             |

A higher score means better quality retention after compression.

---

## **Next Steps**
- Convert all required videos to **Y4M format** before running VMAF.
- Store all computed JSON outputs in a structured folder.
- Compare different compression levels using VMAF.

This ensures a thorough analysis of video compression effects on quality. 

