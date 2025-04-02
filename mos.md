# Mean Opinion Score (MOS) Evaluation

## Overview
The Mean Opinion Score (MOS) is a subjective quality assessment method used to evaluate the perceived quality of volumetric videos. In this project, MOS ratings were collected from 10 different evaluators to analyze the quality of compressed volumetric videos (both VVC and MP4 formats). The results provide an essential comparison metric alongside objective measurements such as VMAF, PSNR, and SSIM.

## Evaluation Process
### 1. Dataset and Test Videos
The dataset consists of compressed volumetric videos, categorized as:
- **Compressed VVC Videos** (Y4M format)
- **Compressed MP4 Videos** (Y4M format after conversion)
Each video represents different compression levels, allowing for a comprehensive quality assessment.

### 2. Evaluators
- A total of **10 evaluators** participated in the MOS study.
- Each evaluator rated multiple versions of the same video compressed at different levels.

### 3. Rating Scale
The evaluators used the following scale to rate video quality:
| Rating | Perceived Quality  |
|--------|------------------|
| 5      | Excellent       |
| 4      | Good           |
| 3      | Fair           |
| 2      | Poor           |
| 1      | Bad            |

### 4. Data Collection
Each evaluator provided ratings for each test video. The rating format was structured as follows:

| Video Name | Evaluator 1 | Evaluator 2 | Evaluator 3 | Evaluator 4 | Evaluator 5 | Evaluator 6 | Evaluator 7 | Evaluator 8 | Evaluator 9 | Evaluator 10 |
|------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|--------------|
| Video_1    | 5           | 4           | 3           | 2           | 1           | 5           | 5           | 4           | 3           | 2            |
| Video_2    | 5           | 5           | 4           | 3           | 3           | 4           | 4           | 3           | 2           | 1            |
| ...        | ...         | ...         | ...         | ...         | ...         | ...         | ...         | ...         | ...         | ...          |

The provided sample Excel file follows this structure for multiple videos.





