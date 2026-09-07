# HandFrame AI

An interactive computer vision project that creates a floating artistic frame controlled by hand gestures, transforming your image into multiple AI-generated artistic styles in real-time.

## Overview

HandFrame AI combines real-time hand tracking, gesture recognition, and AI-powered image generation to create an immersive artistic experience. By forming an L-shape with your hands, you create a floating "pane of glass" that captures your image and applies artistic styles - from classic oil paintings to cyberpunk neon aesthetics.

### Key Features

- **Real-time Hand Tracking**: Uses MediaPipe for robust hand landmark detection
- **Gesture-Controlled Interface**: Form an L-frame with both hands to activate the floating panel
- **Pinch to Capture**: Quick pinch cycles styles, hold pinch triggers AI generation
- **16+ Artistic Styles**: Thermal, Anime, Cyberpunk, Van Gogh, Watercolor, and more
- **Live Filter Mode**: Instant OpenCV-based stylization for real-time feedback
- **AI Generation**: Asynchronous FLUX.2 model inference via fal.ai for high-quality results
- **Perspective-Aware Rendering**: The floating panel naturally tilts, scales, and rotates with your hands
- **Smooth Landmark Filtering**: One-Euro filter eliminates jitter for stable tracking

---

## Tech Stack

| Technology | Purpose |
|------------|---------|
| **Python** | Core programming language |
| **OpenCV** | Image processing, video capture, stylization |
| **MediaPipe** | Hand landmark detection |
| **NumPy** | Numerical operations |
| **fal-client** | FLUX.2 AI model inference |
| **Pillow** | Image handling |

---

## Project Structure

```
HandFrame-AI/
├── app.py              # Main application entry point
├── hand_tracker.py     # Hand tracking & gesture recognition
├── perspective.py      # Perspective transforms & image warping
├── inference.py        # AI inference engine (FLUX.2 + OpenCV fallback)
├── styles.py           # Artistic style definitions
├── smoothing.py        # One-Euro landmark smoothing filter
├── ui_overlay.py       # HUD, spinner, and overlay rendering
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```

---

## Installation

### Prerequisites

- Python 3.9 or higher
- Webcam
- (Optional) fal.ai API key for AI generation

### Setup

```bash
# Clone the repository
git clone https://github.com/tubakhxn/HandFrame-AI.git
cd HandFrame-AI

# Install dependencies
pip install -r requirements.txt
```

### Download Hand Landmarker Model

The project requires MediaPipe's hand landmarker model:

```bash
# Download the model to the project directory
curl -L -o hand_landmarker.task \
  "https://storage.googleapis.com/mediapipe-models/hand_landmarker/hand_landmarker/float16/1/hand_landmarker.task"
```

---

## Usage

### Basic Run

```bash
python app.py
```

### With AI Generation

```bash
python app.py --fal_key YOUR_FAL_API_KEY
```

### Command Line Options

| Argument | Description | Default |
|----------|-------------|---------|
| `--camera` | Webcam index | 0 |
| `--width` | Capture width | 1280 |
| `--height` | Capture height | 720 |
| `--fal_key` | fal.ai API key | None |
| `--strength` | AI style strength | 0.65 |
| `--steps` | AI inference steps | 8 |
| `--capture_size` | Resolution sent to AI model | 512 |
| `--live_size` | Resolution for live filtering | 320 |
| `--hold_threshold` | Seconds to trigger AI generation | 0.6 |
| `--cycle_cooldown` | Minimum seconds between style cycles | 0.35 |
| `--mirror` | Mirror webcam view | True |

---

## Controls

| Gesture | Action |
|---------|--------|
| **L-frame with both hands** | Open the floating panel |
| **Quick pinch (right hand)** | Cycle to next style |
| **Hold pinch (right hand)** | Trigger AI generation |
| **`[` key** | Previous style |
| **`]` key** | Next style |
| **`R` key** | Reset to live mode |
| **`Q` key** | Quit application |

---

## Artistic Styles

The project includes 17 pre-defined styles:

1. Thermal / Heatmap
2. Anime
3. Classic Oil Painting
4. Pop Art
5. Psychedelic Swirl
6. Watercolor Sketch
7. Cyberpunk Neon
8. Van Gogh
9. Graffiti
10. Pencil Sketch
11. Pixel Art
12. Comic Book
13. Low Poly
14. Stained Glass
15. Charcoal
16. Vaporwave
17. Studio Ghibli Sky

---

## Architecture

### Hand Tracking Pipeline
1. MediaPipe processes each video frame
2. Landmarks are smoothed using One-Euro filter
3. Gesture recognition detects L-frame and pinch

### Rendering Pipeline
1. Quadrilateral from hand positions defines the floating panel
2. Perspective transform warps source image into the panel
3. Alpha blending composites the panel onto the live feed
4. Optional border enhances the "pane of glass" effect

### Inference Modes
- **Live Filter**: OpenCV-based stylization runs every frame for instant feedback
- **AI Generation**: Asynchronous FLUX.2 inference via fal.ai produces high-quality results

---

## Performance Tips

- **Live filter mode** runs at full frame rate using optimized OpenCV operations
- **AI generation** runs asynchronously - the UI remains responsive while generating
- **Reduced resolution** for live filtering (`--live_size 160`) improves performance on slower hardware
- **Face-aware stylization** in some styles keeps faces natural while stylizing backgrounds

---

## Troubleshooting

### Webcam Not Found
```bash
# Check available cameras
python -c "import cv2; print([i for i in range(10) if cv2.VideoCapture(i).isOpened()])"

# Try a different camera index
python app.py --camera 1
```

### Model File Missing
```bash
# Download the hand landmarker model
curl -L -o hand_landmarker.task \
  "https://storage.googleapis.com/mediapipe-models/hand_landmarker/hand_landmarker/float16/1/hand_landmarker.task"
```

### AI Generation Not Working
- Ensure `fal-client` is installed: `pip install fal-client`
- Get a free API key at [fal.ai/dashboard/keys](https://fal.ai/dashboard/keys)
- Pass it via `--fal_key YOUR_KEY` or set `FAL_KEY` environment variable

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

Distributed under the MIT License. See `LICENSE` for more information.

---

## Acknowledgments

- [MediaPipe](https://developers.google.com/mediapipe) for hand tracking
- [fal.ai](https://fal.ai) for FLUX.2 model hosting
- [OpenCV](https://opencv.org/) for computer vision capabilities

---

## Contact

Tuba Khan - [@tubakhxn](https://github.com/tubakhxn)

Project Link: [https://github.com/tubakhxn/HandFrame-AI](https://github.com/tubakhxn/HandFrame-AI)

---

*If you found this project useful, consider starring the repository! ⭐*
