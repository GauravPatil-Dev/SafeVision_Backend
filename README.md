
# Real-Time Violence and Safety Violation Detection System

This project is a real-time video analysis tool designed to detect violent incidents and safety violations using advanced computer vision models. It leverages **YOLOv5** for safety gear detection and **LSTM-CNN** models for violence detection. Built with **Flask** and **Flask-SocketIO** for live streaming and frame processing, this system provides an interface for administrators to monitor, analyze, and review detected incidents with frame-level insights.

## Features

- **Real-Time Video Streaming**: Streams video from a live camera feed and processes frames in real-time.
- **Violence Detection**: Detects violent incidents using an LSTM model trained on video sequences.
- **Safety Gear Detection**: Uses YOLOv5 to detect safety gear violations, such as missing helmets or reflective vests.
- **Incident Logging and Frame Storage**: Stores frames for detected incidents with a configurable cooldown period to prevent redundant alerts.
- **Admin Dashboard**: Allows administrators to review and view frames associated with violent incidents and safety violations.
- **Notification System**: Sends real-time alerts when a violent incident or safety violation is detected.

---

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Project Structure](#project-structure)
- [Endpoints](#endpoints)
- [Cooldown Mechanism](#cooldown-mechanism)
- [Sample Output](#sample-output)
- [Future Enhancements](#future-enhancements)

---

## Installation

### Prerequisites

- **Python 3.7+**
- **Virtual Environment** (recommended)
- Required libraries: OpenCV, Flask, Flask-SocketIO, PyTorch, Keras, and dependencies for YOLOv5.

### Clone the Repository

```bash
git clone https://github.com/username/RealTimeViolenceSafetyDetection.git
cd RealTimeViolenceSafetyDetection
```

### Set Up the Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

### YOLOv5 Setup

Ensure YOLOv5 is set up with the correct model weights in the specified path.

```python
yolo_model = torch.hub.load("/path/to/yolov5", "custom", path="path/to/yolov5/runs/train/exp/weights/best.pt", source="local")
```

### Start the Application

```bash
flask run
```

---

## Usage

1. **Upload Video for Analysis**:
   - Use the web interface to upload a video file.
   - The system will process the uploaded video and generate alerts for any detected violence or safety violations.
   
2. **Live Stream**:
   - Start live streaming through the admin dashboard to monitor safety gear compliance and detect violent incidents in real-time.
   
3. **View Incident Logs**:
   - The admin dashboard displays a list of past incidents with links to view associated frames.

---

## Configuration

### Cooldown Periods

Configure cooldown periods in `config.py`:

```python
# Cooldown periods to suppress redundant alerts (in seconds)
COOLDOWN_VIOLENCE = 60  # 1 minute
COOLDOWN_SAFETY_VIOLATION = 60  # 1 minute
```

### Frame Storage Paths

Specify paths for storing incident frames:

```python
# Paths to save frames
VIOLENCE_FRAME_PATH = '/path/to/violence_frames'
SAFETY_VIOLATION_FRAME_PATH = '/path/to/violation_frames'
```

### YOLO Model

Update the path to the YOLO model weights in `yolo_processing()` function.

```python
yolo_model = torch.hub.load("path/to/yolov5", "custom", path="path/to/weights/best.pt", source="local")
```

---

## Project Structure

```bash
RealTimeViolenceSafetyDetection/
│
├── main.py                   # Main application file
├── extractor.py             # Model feature extraction logic
├── requirements.txt         # Python dependencies
├── static/                  # Static files
│   ├── sample_videos/       # Uploaded videos
│   ├── yolo_frames/         # YOLO processed frames
│   ├── violence_frames/     # Violence incident frames
│   └── violation_frames/    # Safety violation frames
├── templates/               # HTML templates
│   ├── home.html            # Home page
│   ├── analyze.html         # Analysis results page
│   └── incidents.html       # Incident listing page
├── README.md                # Project readme
└── config.py                # Configuration file for settings
```

---

## Endpoints

| Endpoint                | Method | Description                            |
|-------------------------|--------|----------------------------------------|
| `/`                     | GET    | Home page                              |
| `/analyze`              | POST   | Analyze uploaded video                 |
| `/live`                 | POST   | Start live streaming                   |
| `/incidents`            | GET    | View past incidents                    |
| `/incidents/violence/<timestamp>` | GET | View violence incident frames  |
| `/incidents/violation/<timestamp>`| GET | View safety violation frames    |

---

## Cooldown Mechanism

To prevent redundant alerts and frame storage, the application uses a cooldown mechanism. Each type of incident (violence and safety violation) has a specified cooldown period. Once an alert is triggered, additional alerts for the same incident type are suppressed until the cooldown period elapses.

---

## Sample Output

### Violent Incident Detection

1. Alerts are generated and frames are stored in `static/violence_frames`.
2. The admin dashboard lists incidents, allowing detailed review of stored frames.

### Safety Gear Violation Detection

1. Alerts are generated for each type of violation (e.g., missing helmet).
2. Frames associated with safety violations are saved in `static/violation_frames`.

---

## Future Enhancements

- **Enhanced Admin Interface**: Implement filters and search capabilities for incident logs.
- **Cloud Storage Integration**: Offload frame storage to cloud storage solutions.
- **Customizable Cooldown Mechanisms**: Allow dynamic adjustment of cooldown periods.
- **Additional Notifications**: Add SMS or email notifications for real-time incident alerts.

---

## Troubleshooting

1. **Model Path Errors**:
   - Ensure that the YOLOv5 model path is correctly specified and accessible.

2. **Storage Limitations**:
   - Monitor disk usage to ensure sufficient space for storing frames. Implement storage rotation or archiving if needed.

3. **Performance Optimization**:
   - Adjust frame storage frequency and cooldowns based on system performance and requirements.

---

## Contributors

- **[Gaurav Patil]** - Developer
- **[Manish Reddy]** - Developer
- **[Pratima Yadav]** - Developer
- **[Shubham Das]** - Developer

---

This project aims to enhance workplace safety and security by providing real-time monitoring for violence and safety compliance. Contributions are welcome, and feel free to report any issues or request new features.