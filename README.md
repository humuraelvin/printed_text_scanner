# Printed Text Scanner GUI - Week 13 Assignment

## Overview
A PyQt5-based graphical user interface application for optical character recognition (OCR) from images and live camera feeds. This application demonstrates AI without Machine Learning by using Tesseract OCR engine for text extraction.

## Features

### Core Functionality
- **Image Loading**: Load JPG/PNG images from disk
- **Live Camera Feed**: Real-time video capture from webcam (USB/built-in)
- **OCR Processing**: Extract text using pytesseract (Tesseract engine)
- **ROI Selection**: Interactive region-of-interest selection with mouse drag
- **Text Box Overlay**: Visual bounding boxes around detected text regions
- **Preprocessing Options**: Multiple image preprocessing modes for better OCR accuracy

### GUI Components
1. **Image Canvas** - Displays loaded images or camera feed with ROI selection capability
2. **Control Panel** - Buttons for image/camera operations and OCR functions
3. **OCR Settings** - Preprocessing mode and threshold value controls
4. **Text Display** - Text widget showing extracted text output
5. **Status Bar** - Real-time operation status feedback

### Preprocessing Modes
- **Grayscale**: Convert to grayscale with noise reduction
- **Threshold**: Binary conversion with configurable threshold
- **Adaptive Threshold**: Advanced thresholding for varying lighting conditions
- **Morphological**: Binary + morphological operations for noise removal

## System Requirements
- **Python**: 3.8 or higher
- **Operating System**: Linux, Windows, or macOS
- **Camera**: USB webcam or built-in camera (for live feed feature)
- **Tesseract**: Must be installed on your system

### Installing Tesseract OCR

#### Linux (Ubuntu/Debian)
```bash
sudo apt-get install tesseract-ocr
```

#### macOS
```bash
brew install tesseract
```

#### Windows
Download installer from: https://github.com/UB-Mannheim/tesseract/wiki
Install and add to system PATH, or set the path in the application.

## Installation

### 1. Clone or Download
```bash
cd /path/to/Printend_text_scanner
```

### 2. Install Python Dependencies
```bash
pip3 install -r requirements.txt
```

Or manually install:
```bash
pip3 install PyQt5
pip3 install opencv-python
pip3 install pytesseract
pip3 install Pillow
pip3 install numpy
```

### 3. Verify Tesseract Installation
```bash
tesseract --version
```

## Running the Application

### Basic Usage
```bash
python3 main.py
```

### From Different Directory
```bash
cd /home/humura/Documents/workings/Year\ 3/Intelligent\ Robotics/Printend_text_scanner
python3 main.py
```

## Usage Guide

### Loading and Processing Images

1. **Load Image**
   - Click "Load Image (JPG/PNG)" button
   - Select an image file from your system
   - Image appears in the canvas on the left

2. **Full Image OCR**
   - Click "OCR Full Image" button
   - Extracted text appears in the text display panel
   - Processing status shown at bottom

3. **ROI (Region of Interest) Selection**
   - Click and drag on the displayed image to draw a rectangle
   - Selected region shown with green outline
   - Click "OCR Selected ROI" to process only that area
   - Use "Clear ROI Selection" to reset

4. **Text Box Overlay**
   - Click "Show Text Box Overlay" button
   - Bounding boxes appear around detected text regions
   - Confidence percentages displayed above boxes
   - Helps visualize OCR detection accuracy

### Using Live Camera

1. **Start Camera Feed**
   - Click "Open Live Camera" button
   - Live preview displays in the canvas
   - Button changes to "Stop Camera"

2. **Capture and Process**
   - Current frame automatically shown in canvas
   - Apply OCR to current frame using "OCR Full Image"
   - Select regions for ROI processing

3. **Stop Camera**
   - Click "Stop Camera" button to disconnect

### Adjusting OCR Settings

1. **Preprocessing Mode**
   - Select from dropdown: Grayscale, Threshold, Adaptive Threshold, Morphological
   - Different modes work better for different images
   - Experiment to find best results

2. **Threshold Value**
   - Adjust value (0-255) for Threshold and Morphological modes
   - Higher values keep more text
   - Lower values remove noise

## File Structure

```
Printend_text_scanner/
├── main.py              # Main PyQt5 application
├── ocr_utils.py         # OCR and preprocessing functions
├── camera_utils.py      # Camera capture utilities
├── README.md            # This file
└── requirements.txt     # Python dependencies
```

## Module Descriptions

### main.py
- **TextScannerApp**: Main QMainWindow subclass with complete GUI
- **ImageCanvas**: Custom QLabel for image display and ROI selection
- **CameraThread**: Background thread for continuous camera frame capture
- Features: Image loading, camera control, OCR operation, overlay display

### ocr_utils.py
- **preprocess_image()**: Applies various preprocessing techniques
- **extract_text_with_boxes()**: Runs pytesseract OCR
- **get_text_boxes()**: Returns bounding box coordinates
- **extract_text_from_roi()**: Processes specific ROI regions

### camera_utils.py
- **CameraCapture**: OpenCV camera wrapper class
- Methods: get_frame(), set_resolution(), set_fps(), release()
- **test_camera_availability()**: Checks if camera is accessible

## Troubleshooting

### Camera Not Detected
```bash
# Check available cameras
ls /dev/video*  # Linux
# Or test with OpenCV
python3 -c "import cv2; cap = cv2.VideoCapture(0); print('Camera works' if cap.isOpened() else 'Camera not found')"
```

### Tesseract Not Found
```bash
# Linux: Install tesseract
sudo apt-get install tesseract-ocr

# macOS: Install with brew
brew install tesseract

# Windows: Download from https://github.com/UB-Mannheim/tesseract/wiki
# Then set path in code or add to system PATH
```

### Poor OCR Results
1. Try different preprocessing modes
2. Adjust threshold value (0-255)
3. Ensure good lighting on document
4. Use Adaptive Threshold for variable lighting
5. Select high-contrast images for best results

### Permission Errors
```bash
# Make script executable (Linux/macOS)
chmod +x main.py

# Or run explicitly with Python
python3 main.py
```

## Demo Instructions

### Demo 1: Image OCR
1. Run: `python3 main.py`
2. Click "Load Image"
3. Select a text-containing image (article, document, etc.)
4. Click "OCR Full Image"
5. View extracted text in output panel

### Demo 2: ROI Processing
1. After loading image, draw rectangle by clicking and dragging
2. Click "OCR Selected ROI"
3. Only selected region text extracted
4. Compare with full image OCR results

### Demo 3: Text Overlay
1. Load an image
2. Click "Show Text Box Overlay"
3. Green boxes appear around detected text
4. Confidence scores shown above boxes

### Demo 4: Live Camera OCR
1. Ensure webcam connected
2. Click "Open Live Camera"
3. Point camera at printed text
4. Click "OCR Full Image"
5. Extracted text appears in real-time

## Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| PyQt5 | 5.15+ | GUI framework |
| opencv-python | 4.5+ | Computer vision (camera, image ops) |
| pytesseract | 0.3+ | Tesseract OCR wrapper |
| Pillow | 8.0+ | Image processing (PIL) |
| numpy | 1.19+ | Numerical operations |
| tesseract (system) | 4.0+ | OCR engine (must install separately) |

## Performance Notes
- **Camera Resolution**: Set to 640x480 for optimal performance
- **Frame Rate**: 30 FPS default
- **OCR Speed**: ~2-5 seconds per full image (depends on resolution)
- **Memory**: Uses ~200-300 MB while running

## Development Notes

### Code Quality
- Object-oriented design using PyQt5 inheritance
- Modular architecture separating concerns
- Error handling for all major operations
- Thread-safe camera capture with QThread
- Cross-platform compatibility

### Key Design Decisions
1. **Threading**: Camera capture in background thread prevents UI freezing
2. **Signal/Slot**: PyQt5 signals for thread-safe communication
3. **Preprocessing Modes**: Multiple options for different image types
4. **ROI Selection**: Click-drag interface mimics standard image editors

## Academic Context
This project demonstrates:
- **AI without ML**: Using traditional OCR (Tesseract) instead of neural networks
- **Computer Vision**: Image preprocessing and manipulation with OpenCV
- **GUI Development**: PyQt5 framework for professional applications
- **Real-time Processing**: Live camera feed handling and frame processing
- **Software Engineering**: Clean code, modularity, and error handling

## License
For academic use - Week 13 Assignment, Intelligent Robotics course

## Author
Generated for Week 13 Assignment: "AI Without ML – Printed Text Scanner GUI"

## Support
For issues or questions, check:
1. Tesseract installation and PATH configuration
2. Camera permissions (Linux: may need `usermod` to add user to video group)
3. Image format and quality
4. Python version compatibility (3.8+)
