# VMAF (Video Multi-Method Assessment Fusion) 

## What is VMAF?
VMAF (Video Multi-Method Assessment Fusion) is a video quality metric developed by Netflix. It combines multiple quality assessment algorithms using machine learning to provide a score that correlates well with human perception of video quality. It is widely used to compare compressed video quality against a reference to evaluate compression efficiency.

## Comparing Videos Using VMAF
To compare a reference video with a distorted (compressed) video using VMAF, use the following command:

```sh
vmaf --reference "/mnt/f/redandblack_grey_11_vox10.y4m" --distorted "/mnt/f/R5_redandblack_11_grey_vox10.y4m" --output "/mnt/f/R5_redandblack_11_grey_vox10.json" --json
```

### Explanation of Command:
- `--reference` → Specifies the original high-quality video file (e.g., `redandblack_grey_11_vox10.y4m`).
- `--distorted` → Specifies the compressed version of the video (e.g., `R5_redandblack_11_grey_vox10.y4m`).
- `--output` → The output file where VMAF scores will be stored (e.g., `R5_redandblack_11_grey_vox10.json`).
- `--json` → Ensures the output is saved in JSON format.

## Setting Up VMAF on GitHub
To document and share your VMAF comparison process on GitHub, follow these steps:

## How to Interpret VMAF Results
The JSON output file contains VMAF scores for different frames. The key values to look at include:
- `VMAF_score`: The overall quality score (0-100). Higher is better.

Example JSON snippet:
```json
"vmaf": {
      "min": 46.386961,
      "max": 73.834192,
      "mean": 60.450197,
      "harmonic_mean": 59.993917
    }
```

### How to Explain VMAF Scores
- A **VMAF score of 100** means the distorted video is visually identical to the reference.
- **Above 80** is considered very good quality.
- **60-80** is acceptable but may show some compression artifacts.
- **Below 50** indicates noticeable degradation.

## Conclusion
By using VMAF, you can objectively evaluate video compression quality and optimize encoding settings for better perceptual quality. Documenting your results on GitHub ensures transparency and reproducibility for future work.

