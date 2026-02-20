# 🏋️ Virtual Sports Coach

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18+-61dafb.svg)](https://reactjs.org/)
[![ngrok](https://img.shields.io/badge/ngrok-ready-blueviolet)](https://ngrok.com/)
[![Git LFS](https://img.shields.io/badge/Git%20LFS-enabled-orange)](https://git-lfs.github.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An intelligent, real-time virtual coach that uses computer vision and machine learning to analyze exercise form, provide instant feedback, and track workout progress. Perfect for home workouts, rehabilitation, and fitness training.
## 🎥 Demo

Check out the Virtual Sports Coach in action!

<video src="docs/demo/virtual-coach-demo.mp4" width="100%" controls></video>

## ✨ Features

- **Real-time pose detection** using MediaPipe and YOLOv8
- **Exercise form analysis** with custom ML models (LSTM, ONNX)
- **Instant audio feedback** via pyttsx3
- **Public URL access** via ngrok (share your workout session remotely)
- **Hardware integration** for Raspberry Pi (LEDs, buzzer)
- **Progress tracking** with SQLite database
- **Cross-platform** (Windows, Raspberry Pi, Linux)
- **Modern web interface** built with React/Next.js
- **WebSocket support** for real-time communication

## 📋 Table of Contents

- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [ML Models](#-ml-models)
- [🌐 Public Access with ngrok](#-public-access-with-ngrok)
- [Project Structure](#-project-structure)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [Hardware Setup](#-hardware-setup-for-raspberry-pi)
- [API Documentation](#-api-documentation)
- [Contributing](#-contributing)
- [License](#-license)

## 🚀 Prerequisites

### System Requirements
- **Python**: 3.11 or higher
- **Node.js**: 18.x or higher
- **RAM**: 8GB minimum (16GB recommended for model training)
- **Disk Space**: 2GB for models and dependencies
- **Camera**: Webcam or USB camera (for pose detection)

### Software Requirements
- **Git** with **Git LFS** (Large File Storage)
- **pip** (Python package manager)
- **npm** or **yarn** (Node.js package manager)
- **ngrok** (for public access) - [Download here](https://ngrok.com/download)

## ⚡ Quick Start

### 1. Clone the Repository with Models

First, install Git LFS from [git-lfs.github.com](https://git-lfs.github.com/), then:

```bash
# Clone the repository
git clone https://github.com/JustEv4/Virtual-Coach.git
cd Virtual-Coach

# Download the ML models (stored with Git LFS)
git lfs pull
```

### 2. Backend Setup (Python/FastAPI)

```bash
# Navigate to backend directory
cd backend

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Start the backend server
python main.py
# or
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

### 3. Frontend Setup (React/Next.js)

```bash
# Open a new terminal
cd frontend

# Install dependencies
npm install
# or
yarn install

# Start the development server
npm run dev
# or
yarn dev
```

The application will be available at:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **API Documentation**: http://localhost:8000/docs

## 🌐 Public Access with ngrok

Share your virtual coach with anyone, anywhere using ngrok tunnels.

### Why ngrok?
- **Share your workout session** with remote coaches or friends
- **Test on mobile devices** without local network setup
- **Demo your project** to clients or stakeholders
- **Access from anywhere** without port forwarding

### Setting up ngrok

#### 1. **Install ngrok**
- **Windows**: Download from [ngrok.com/download](https://ngrok.com/download)
- **Mac**: `brew install ngrok`
- **Linux**: `sudo snap install ngrok`

#### 2. **Create an ngrok account** (free)
- Sign up at [ngrok.com](https://ngrok.com)
- Get your auth token from the dashboard

#### 3. **Authenticate ngrok**
```bash
ngrok config add-authtoken YOUR_AUTH_TOKEN
```

### 🚀 Creating Public Tunnels

#### **Option A: Tunnel both frontend and backend (Recommended)**

Open two separate terminals:

**Terminal 1 - Backend tunnel:**
```bash
# Tunnel the FastAPI backend (port 8000)
ngrok http 8000
```
**Output:**
```
Forwarding https://abc123.ngrok.io -> http://localhost:8000
```

**Terminal 2 - Frontend tunnel:**
```bash
# Tunnel the Next.js frontend (port 3000)
ngrok http 3000
```
**Output:**
```
Forwarding https://xyz789.ngrok.io -> http://localhost:3000
```

#### **Option B: Single tunnel for backend only (for API access)**
```bash
ngrok http 8000
```

#### **Option C: Use the included batch script (Windows)**
```bash
# Simply run:
run_backend_public.bat
```
This script automatically:
- Starts the backend server
- Launches ngrok tunnel
- Displays the public URL
- Opens your default browser

### 📱 Accessing Your Public App

Once tunnels are running:

| Service | Local URL | Public URL (example) |
|---------|-----------|----------------------|
| Frontend | http://localhost:3000 | https://xyz789.ngrok.io |
| Backend API | http://localhost:8000 | https://abc123.ngrok.io |
| API Docs | http://localhost:8000/docs | https://abc123.ngrok.io/docs |
| WebSocket | ws://localhost:8000/ws | wss://abc123.ngrok.io/ws |

### ⚙️ Configure Frontend to Use Public Backend

Update your frontend `.env.local` file:

```env
# For local development
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_WEBSOCKET_URL=ws://localhost:8000/ws

# For public access (replace with your ngrok URL)
NEXT_PUBLIC_API_URL=https://abc123.ngrok.io
NEXT_PUBLIC_WEBSOCKET_URL=wss://abc123.ngrok.io/ws
```

### 🔒 Security Notes

- **Free ngrok** URLs are temporary and change each restart
- **Paid plans** offer:
  - Custom subdomains (e.g., `mycoach.ngrok.io`)
  - Reserved domains
  - Basic authentication
  - IP restrictions

Add basic auth to your tunnel:
```bash
ngrok http 8000 --basic-auth="username:password"
```

### 🎯 Use Cases for ngrok

| Scenario | How to Use |
|----------|------------|
| Remote coaching | Share frontend URL with your coach |
| Mobile testing | Access from phone/tablet on cellular data |
| Client demo | Send temporary URL for review |
| Team collaboration | Share backend API for integration |
| IoT/Raspberry Pi | Access Pi from anywhere without static IP |

## 🧠 ML Models

This project uses several machine learning models stored with **Git LFS**. After cloning, ensure you've run `git lfs pull` to download them.

### Model Files

| File | Size | Purpose |
|------|------|---------|
| `fitness_model.onnx` | 330 MB | Main exercise classification |
| `correctionExercices (1).onnx` | 85 MB | Exercise correction model |
| `correctionExercices (1).pt` | 85 MB | PyTorch version of correction model |
| `model_lstm_tache2.h5` | 45 MB | LSTM model for temporal analysis |
| `model_lstm_tache2.tflite` | 15 MB | TensorFlow Lite optimized version |
| `model_lstm_tache2_optimized.tflite` | 8 MB | Further optimized for edge devices |
| `pose_landmarker_full.task` | 30 MB | MediaPipe pose landmarks |
| `yolov8n-pose.pt` | 6 MB | YOLOv8 pose detection |
| `classif_model_.pkl` | 2 MB | Scikit-learn classifier |
| `scaler_tache2.pkl` | 1 MB | Feature scaler |

### Important Notes for Contributors

If you're contributing to this project:

```bash
# Install Git LFS first
git lfs install

# Clone the repo
git clone https://github.com/JustEv4/Virtual-Coach.git
cd Virtual-Coach

# Pull the LFS files
git lfs pull

# When adding new model files
git lfs track "*.onnx"
git lfs track "*.pt"
git lfs track "*.h5"
git lfs track "*.tflite"
git add .gitattributes
git add your-model-file
git commit -m "Add new model"
git push
```

## 📁 Project Structure

```
Virtual-Coach/
├── backend/                    # Python FastAPI backend
│   ├── main.py                 # Main application entry point
│   ├── requirements.txt        # Python dependencies
│   ├── venv/                   # Virtual environment (not in repo)
│   ├── models/                 # ML models (Git LFS)
│   │   ├── fitness_model.onnx
│   │   ├── correctionExercices (1).onnx
│   │   ├── model_lstm_tache2.h5
│   │   └── ...
│   ├── pose_detector.py        # Pose detection module
│   ├── exercise_engine.py      # Exercise analysis logic
│   ├── feedback.py             # Audio feedback system
│   ├── hardware_manager.py     # Hardware abstraction layer
│   ├── hardware_pi.py          # Raspberry Pi specific code
│   ├── hardware_sim.py         # Hardware simulation for dev
│   ├── database.py             # SQLite database operations
│   ├── calibration.py          # Camera calibration
│   ├── scripts/                 # Utility scripts
│   │   ├── install_deps.bat
│   │   ├── install_deps.sh
│   │   ├── run_backend.bat
│   │   ├── setup_pi.sh
│   │   └── test_hardware.sh
│   └── tests/                   # Unit tests
│       ├── test_models.py
│       ├── test_ORT.py
│       └── test_tflite.py
│
├── frontend/                   # React/Next.js frontend
│   ├── src/                    # Source code
│   ├── public/                  # Static assets
│   ├── package.json
│   ├── package-lock.json
│   └── node_modules/            # Not in repo
│
├── docs/                        # Documentation
│   ├── Architecture.md
│   ├── Architecture_RaspberryPi.md
│   ├── DEPLOYMENT_VERCEL_PI.md
│   ├── HARDWARE_CONFIG.md
│   ├── Setup_RaspberryPi.md
│   └── deployment_guide.md
│
├── .gitignore                   # Git ignore rules
├── .gitattributes               # Git LFS configuration
├── run_backend_public.bat       # Windows startup script with ngrok
├── setup_and_run_pi.sh          # Raspberry Pi setup script
└── sport_coach.bat              # Main launcher for Windows
```

## ⚙️ Configuration

### Environment Variables

Create a `.env` file in the backend directory:

```env
# Backend Configuration
HOST=0.0.0.0
PORT=8000
DEBUG=True
DATABASE_URL=sqlite:///coach.db

# Camera Settings
CAMERA_ID=0
FRAME_WIDTH=640
FRAME_HEIGHT=480
FPS=30

# Hardware (Raspberry Pi)
ENABLE_HARDWARE=False
LED_PIN=18
BUZZER_PIN=23

# Model Settings
MODEL_PATH=./models/fitness_model.onnx
CONFIDENCE_THRESHOLD=0.7
```

### Frontend Configuration

Create a `.env.local` file in the frontend directory:

```env
# For local development
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_WEBSOCKET_URL=ws://localhost:8000/ws

# For public access (replace with your ngrok URL)
# NEXT_PUBLIC_API_URL=https://abc123.ngrok.io
# NEXT_PUBLIC_WEBSOCKET_URL=wss://abc123.ngrok.io/ws
```

## 🎮 Usage

### Basic Workflow

1. **Start the backend server**
2. **(Optional) Start ngrok tunnel** for public access
3. **Open the frontend application** in your browser
4. **Allow camera access** when prompted
5. **Select an exercise** from the list
6. **Follow the on-screen instructions** and perform the exercise
7. **Receive real-time feedback** via audio and visual cues
8. **Track your progress** in the dashboard

### Available Exercises

- Squats
- Push-ups
- Lunges
- Planks
- Jumping jacks
- And more...

### Voice Commands (if enabled)

- "Start workout"
- "Next exercise"
- "Repeat instructions"
- "Stop workout"

## 🎛️ Hardware Setup (for Raspberry Pi)

### Required Components
- Raspberry Pi 4 or 5
- Camera module or USB webcam
- LEDs (optional, for visual feedback)
- Buzzer (optional, for audio feedback)
- Speaker (optional, for voice feedback)

### Installation on Raspberry Pi

```bash
# Clone the repository
git clone https://github.com/JustEv4/Virtual-Coach.git
cd Virtual-Coach

# Download models
git lfs pull

# Run the setup script
chmod +x setup_and_run_pi.sh
./setup_and_run_pi.sh
```

### Pin Configuration (if using GPIO)

| Component | GPIO Pin |
|-----------|----------|
| LED (Red) | 18 |
| LED (Green) | 19 |
| LED (Blue) | 20 |
| Buzzer | 23 |

### Access Your Pi Remotely with ngrok

```bash
# On your Raspberry Pi, expose the backend
ngrok http 8000

# Share the generated URL with anyone!
```

## 📚 API Documentation

Once the backend is running, access the interactive API documentation at:
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc
- **Via ngrok**: https://your-ngrok-url/docs

### Main Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | API status |
| `/ws` | WebSocket | Real-time video stream |
| `/exercises` | GET | List available exercises |
| `/analyze` | POST | Analyze a single frame |
| `/start_workout` | POST | Start a workout session |
| `/stop_workout` | POST | Stop current session |
| `/history` | GET | Get workout history |

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**:
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**:
   ```bash
   git commit -m 'Add amazing feature'
   ```
4. **Push to the branch**:
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Development Guidelines

- Follow PEP 8 for Python code
- Use ESLint/Prettier for JavaScript/React
- Add tests for new features
- Update documentation as needed
- Keep model files under 100MB (use Git LFS for larger files)

### Adding New Models

```bash
# Track new model types if needed
git lfs track "*.newmodel"

# Add your model
git add path/to/your-model.newmodel
git commit -m "Add new model for feature X"
git push
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [MediaPipe](https://mediapipe.dev/) for pose detection
- [YOLOv8](https://github.com/ultralytics/ultralytics) for object detection
- [FastAPI](https://fastapi.tiangolo.com/) for the backend framework
- [React](https://reactjs.org/) for the frontend library
- [TailwindCSS](https://tailwindcss.com/) for styling
- [Git LFS](https://git-lfs.github.com/) for large file storage
- [ngrok](https://ngrok.com/) for secure tunnels to localhost

## 📧 Contact

- **Project Link**: [https://github.com/JustEv4/Virtual-Coach](https://github.com/JustEv4/Virtual-Coach)
- **Issues**: [Report a bug](https://github.com/JustEv4/Virtual-Coach/issues)
- **Discussions**: [Join the conversation](https://github.com/JustEv4/Virtual-Coach/discussions)

---

**Happy Training!** 🏋️‍♂️ 
**Share your progress anywhere with ngrok!** 🌐
