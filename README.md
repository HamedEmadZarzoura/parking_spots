# parking_spots

Detects which parking spots are free in a parking-lot video and shows the count on screen.

## How it works
- A mask image (mask.png) marks each parking spot. Connected components of the mask give one bounding box per spot (util.py).
- Every 30 frames, each spot is compared with the same spot in the previous sampled frame. After the first sample, only spots whose change is above 40% of the largest change are classified again.
- Each spot crop is resized to 15x15x3, flattened, and classified as empty or not empty by a model loaded from model.p.
- Spots are drawn green (empty) or red (not empty), with "Available spots: X / N" on screen. Press q to quit.

## Files
- main.py, util.py
- mask.png, mask_crop.png
- parking.mp4, parking_crop.mp4, video.mp4
- model.p

## Dependencies (from the imports)
opencv-python, numpy, matplotlib, scikit-image. The type of model stored in model.p is not shown in this repo; the code only calls its predict method.

## Run (from the code, not tested)
```
python main.py
```

Run it from the repo folder: the paths to mask.png, parking.mp4 and model.p are relative.

## Notes
- model.p is a Python pickle. Only load pickles you trust, because loading an untrusted one can run code.
- The code that trained model.p is not in this repo.
- The script uses one fixed video and one mask.
