
#### **FFmpeg with libvmaf for Video Quality Assessment**  

### **Introduction**  
FFmpeg with **libvmaf** is used to compute **VMAF (Video Multi-Method Assessment Fusion) scores**. VMAF is a video quality metric developed by Netflix that provides a perceptual similarity score between a reference (original) and a distorted (compressed) video.  

In this guide, we will explain how to use **FFmpeg and libvmaf** to compare **compressed VVC Y4M videos** and **compressed MP4 Y4M videos** on **Windows**.  


## **1. Installation of FFmpeg with libvmaf**  
Before using **FFmpeg with libvmaf**, ensure that FFmpeg is installed on your Windows system **with libvmaf enabled**.

### **Step 1: Download FFmpeg**  
Download the latest static build of FFmpeg from:  
👉 [https://www.gyan.dev/ffmpeg/builds/](https://www.gyan.dev/ffmpeg/builds/)  

Make sure to download the **"full" version**, which includes the `libvmaf` filter.  

### **Step 2: Verify libvmaf Availability**  
After installing, open **Command Prompt (cmd)** and check if FFmpeg has libvmaf enabled:  
```sh
ffmpeg -filters | findstr "vmaf"
```
If you see `libvmaf`, you are good to go! ✅  

---

## **2. Using FFmpeg libvmaf to Compute VMAF Scores**  
To compare a **compressed VVC Y4M video** with its **corresponding compressed MP4 Y4M video**, use the following command:

```sh
ffmpeg -i "F:\geometry_compression_VVC_y4m\R2\R2_loot_gc_black_10_vox10.y4m" -i "F:\geometry_compression_MP4_y4m\R2\loot_black_10_vox10.y4m" -lavfi libvmaf -f null -
```

---

### **3. Explanation of the Command**
- `-i "F:\geometry_compression_VVC_y4m\R2\R2_loot_gc_black_10_vox10.y4m"`  
  - Specifies the **reference video** (original compressed VVC Y4M file).
  
- `-i "F:\geometry_compression_MP4_y4m\R2\loot_black_10_vox10.y4m"`  
  - Specifies the **distorted video** (compressed MP4 Y4M file).  

- `-lavfi libvmaf`  
  - Applies the **VMAF filter** to compare the two videos.  

- `-f null -`  
  - Discards the output video and only computes VMAF scores.  

---

## **4. Saving VMAF Scores as JSON Output**  
If you want to **save the VMAF scores** in a JSON file for later analysis, modify the command as follows:

```sh
ffmpeg -i "F:\geometry_compression_VVC_y4m\R2\R2_loot_gc_black_10_vox10.y4m" -i "F:\geometry_compression_MP4_y4m\R2\loot_black_10_vox10.y4m" -lavfi libvmaf="log_path=F:/vmaf_results/R2_loot_vmaf.json" -f null -
```
This will create a JSON file containing detailed VMAF scores.

---

## **5. How to Interpret VMAF Results**  
When you compute VMAF scores, the output will contain values like:

| Metric | Description |
|--------|------------|
| `VMAF_score` | Overall VMAF score (ranges from 0-100). Higher is better. 

- **VMAF Score Range:**  
  - **90-100** 🟢 → Excellent Quality  
  - **70-90** 🟡 → Good Quality  
  - **50-70** 🔴 → Noticeable Quality Loss  
  - **Below 50** ❌ → Poor Quality  

---

## **6. Automating VMAF Calculation for Multiple Videos**
If you have multiple files and want to **automate the process**, you can use a batch script (`.bat` file) to loop through all videos in a folder:

## **7. Troubleshooting**
If you encounter **errors**, check the following:
- Ensure **FFmpeg is installed correctly** and `libvmaf` is enabled.
- Make sure **both input videos** have the same resolution.
- If needed, use **FFmpeg to resize**:
  ```sh
  ffmpeg -i input.y4m -vf scale=1920:1080 output.y4m
  ```
- Run commands in **cmd (Command Prompt)**, not PowerShell.

---

## **8. Conclusion**
Using **FFmpeg with libvmaf**, you can efficiently compare **compressed volumetric videos** and evaluate quality loss. The JSON output allows further analysis using visualization tools.

📌 **Next Steps**  
- Automate batch processing for all datasets.  
- Compare results with **PSNR** and **SSIM** metrics.  
- Visualize VMAF scores for better insights.

---

## **9. References**
- [FFmpeg Official Website](https://ffmpeg.org/)  
- [Netflix VMAF GitHub](https://github.com/Netflix/vmaf)  
