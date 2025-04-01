# Vehicle Detection and Speed Estimation using YOLOv8 and Supervision

This project uses YOLOv8 and Supervision library to detect vehicles in a video, track them, and estimate their speed within a defined region of interest (ROI).

## Prerequisites

- Python 3.x
- Required libraries:
  ```bash
  pip install opencv-python numpy ultralytics supervision
  ```

## Configuration

### File Paths
```python
SOURCE_VIDEO_PATH = "/content/video1.mp4"  # Input video path
TARGET_VIDEO_PATH = "/content/vehicles-result1.mp4"  # Output video path
```

### Detection Parameters
```python
CONFIDENCE_THRESHOLD = 0.3  # Minimum confidence score for detections
IOU_THRESHOLD = 0.5        # Intersection over Union threshold for NMS
MODEL_NAME = "yolov8x.pt"  # YOLO model to use
MODEL_RESOLUTION = 1280    # Model inference resolution
```

### Region of Interest (ROI)
Defined as a polygon with source coordinates:
```python
SOURCE = np.array([
    [740, 570],   # Point A
    [1120, 570],  # Point B
    [1750, 1080], # Point C
    [0, 1080]     # Point D
])
```

### Target Perspective
Transformed coordinates for speed calculation:
```python
TARGET_WIDTH = 25   # Width in meters
TARGET_HEIGHT = 70  # Height in meters
```

## Functionality

### View Transformation
The `ViewTransformer` class handles perspective transformation:
- Converts points from source ROI to target coordinate system
- Used for accurate distance and speed calculations

### Main Components
1. **Object Detection**: Uses YOLOv8 for vehicle detection
2. **Tracking**: Implements ByteTrack for object tracking
3. **Visualization**: 
   - Bounding boxes
   - Tracking traces
   - Speed labels
4. **Speed Calculation**:
   - Tracks vehicle position over frames
   - Calculates distance traveled
   - Estimates speed in km/h

### Processing Pipeline
1. Reads video frames
2. Detects vehicles within ROI
3. Applies Non-Maximum Suppression
4. Tracks vehicles across frames
5. Calculates speed based on transformed coordinates
6. Annotates frames with:
   - Bounding boxes
   - Tracker IDs
   - Speed estimates
7. Writes processed frames to output video

## Usage
1. Set the correct video paths
2. Adjust ROI coordinates if needed
3. Modify detection parameters as required
4. Run the script

## Output
- Processed video with vehicle detections and speed estimates
- Vehicles are labeled with tracker ID and speed in km/h
- Only vehicles within the defined ROI are processed

## Notes
- Speed calculation assumes a flat plane and known real-world dimensions
- Accuracy depends on:
  - Correct ROI calibration
  - Frame rate consistency
  - Video quality
- Class ID 0 is filtered out (typically person class)

## References
This project is inspired by and builds upon the work:

- Shaqib, S. M., Rupak, A. U. H., Alo, A. P., Khan, S. S., Ramit, S. S., & Rahman, M. S. (2024). *Vehicle Speed Detection System Utilizing YOLOv8: Enhancing Road Safety and Traffic Management for Metropolitan Areas*. arXiv:2406.07710v1 [cs.CV]. Department of CSE, Daffodil International University, Dhaka, Bangladesh.
  - Available at: [https://arxiv.org/abs/2406.07710](https://arxiv.org/abs/2406.07710)
  - Authors' contacts:
    - SM Shaqib: shaqib15-4614@diu.edu.bd
    - Afraz Ul Haque Rupak: afra15-13252@diu.edu.bd
    - Alaya Parvin Alo: alo15-4283@diu.edu.bd
    - Sadman Sadik Khan: sadman15-13696@diu.edu.bd
    - Shahriar Sultan Ramit: shahriar15-4248@diu.edu.bd
    - Md. Sadekur Rahman: sadekur.cse@daffodilvarsity.edu.bd
