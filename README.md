### DOWNLOAD our Model weight
Our pre-tained model weight can be download [HERE](https://drive.google.com/file/d/1_mrzOAAGsn2DAI7T1igJ9pYKabV278lb/view?usp=sharing).
Please put it in `models/`

### Example Google Colab code
https://colab.research.google.com/drive/1TszsO2RmbS8Q6nK4x56MWaHMenCwBMsQ?usp=sharing

### File Structure
Dataset description: https://hackmd.io/Nf8Rh1NrSrqNUzmO0sQKZw 
Remember to set the data root directory in utils.py.

        TrackNetV2_Dataset
            ├─ train
            |    ├── match1/
            |    │     ├── ball_trajectory/
            |    │     │     ├── 1_01_00_ball.csv
            |    │     │     ├── 1_02_00_ball.csv
            |    │     │     ├── …
            |    │     │     └── *_**_**_ball.csv
            |    │     ├── frame/
            |    │     │     ├── 1_01_00/
            |    │     │     │     ├── 0.png
            |    │     │     │     ├── 1.png
            |    │     │     │     ├── …
            |    │     │     │     └── *.png
            |    │     │     ├── 1_02_00/
            |    │     │     │     ├── 0.png
            |    │     │     │     ├── 1.png
            |    │     │     │     ├── …
            |    │     │     │     └── *.png
            |    │     │     ├── …
            |    │     │     └── *_**_**/
            |    │     │
            |    │     └── rally_video/
            |    │           ├── 1_01_00.mp4
            |    │           ├── 1_02_00.mp4
            |    │           ├── …
            |    │           └── *_**_**.mp4
            |    ├── match2/
            |    │ ⋮
            |    ├── match15/
            |    ├── match24/
            |    ├── match25/
            |    └── match26/
            |
            └─ test
                 ├── match1/
                 ├── match2/
                 └── match3/

### Generate frames from videos

`python3 preprocess.py`

### Train TrackNet
Train TrackNet from scratch
`python3 train.py --num_frame 3 --epochs 30 --batch_size 10 --learning_rate 0.001 --save_dir exp`

Resume training
`python3 train.py --epochs 30 --save_dir exp --resume_training`

### Evaluate TrackNet
Step 1: evaluate TrackNet on train and test set
`python3 evaluation.py --batch_size 20 --model_file models/model_best.pt --save_dir models/eval`

Step 2: gather the evaluation results (optional)
`python3 evaluation.py --batch_size 20 --model_file models/model_best.pt --save_dir models/eval --analyze`

### Show predicted video with label (for evaluation)
`python3 show_rally.py --frame_dir TrackNetV2_Dataset/test/match1/frame/1_05_02 --model_file models/model_best.pt --batch_size 20 --output_mode both --save_dir models/eval`

### Prediction
`python3 predict.py --video_file test.mp4 --model_file models/model_best.pt --save_dir prediction`

### Show trajectory
`python3 show_trajectory.py --video_file test.mp4 --csv_file prediction/test_ball.csv --save_dir prediction`
