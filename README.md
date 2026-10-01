# 🤖 Face Recognition Attendance System

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/Flask-Web%20Application-000000?style=for-the-badge&logo=flask&logoColor=white">
  <img src="https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white">
  <img src="https://img.shields.io/badge/scikit--learn-KNN-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white">
  <img src="https://img.shields.io/badge/Pandas-Data%20Processing-150458?style=for-the-badge&logo=pandas&logoColor=white">
  <img src="https://img.shields.io/badge/Joblib-Model%20Persistence-2E7D32?style=for-the-badge">
</p>

<p align="center">
  <strong>A webcam-based attendance application that detects faces in real time, identifies registered users with a trained K-Nearest Neighbors classifier, and records attendance automatically in daily CSV files.</strong>
</p>

<p align="center">
  <a href="https://github.com/avaleajay170/Face-Recognition-Attendance-System">📂 Repository</a>
  •
  <a href="#-features">Features</a>
  •
  <a href="#-system-workflow">Workflow</a>
  •
  <a href="#-installation">Installation</a>
  •
  <a href="#-project-structure">Project Structure</a>
</p>

---

## 📖 Table of Contents

<details>
<summary>Click to expand</summary>

- [📌 Overview](#-overview)
- [🎯 Problem Statement](#-problem-statement)
- [💡 Objectives](#-objectives)
- [✨ Features](#-features)
- [🧠 How Face Recognition Works](#-how-face-recognition-works)
- [🔄 System Workflow](#-system-workflow)
- [🧩 Detection & Recognition Pipeline](#-detection--recognition-pipeline)
- [👤 User Registration](#-user-registration)
- [✅ Attendance Marking](#-attendance-marking)
- [📊 Attendance Records](#-attendance-records)
- [🛠️ Technology Stack](#️-technology-stack)
- [🏗️ System Architecture](#️-system-architecture)
- [📂 Project Structure](#-project-structure)
- [⚙️ Installation](#️-installation)
- [▶️ Running the Application](#️-running-the-application)
- [🗃️ Model & Data Storage](#️-model--data-storage)
- [🧪 Testing](#-testing)
- [⚠️ Limitations & Security Considerations](#️-limitations--security-considerations)
- [🚀 Future Scope](#-future-scope)
- [🤝 Contributing](#-contributing)
- [👨‍💻 Developer](#-developer)
- [📄 License](#-license)

</details>

---

# 📌 Overview

The **Face Recognition Attendance System** is a Python-based web application that combines **Flask, OpenCV, and scikit-learn** to automate attendance using a webcam.

Instead of manually entering attendance, the application:

1. Captures video from the webcam.
2. Detects faces in the camera feed.
3. Resizes the detected face.
4. Uses a trained KNN classifier to identify the registered user.
5. Adds the recognized user to the current day's attendance file.
6. Prevents duplicate attendance entries for the same roll number on that day.

The project provides two main operations:

- **Start Face Recognition** — identify users and record attendance.
- **Register New User** — capture a set of face images and retrain the recognition model.

---

# 🎯 Problem Statement

Manual attendance systems can be:

- Time consuming
- Repetitive
- Prone to data-entry mistakes
- Difficult to manage for larger groups
- Dependent on manual identification

This project explores a computer-vision-based approach where a webcam is used to identify registered users and record attendance automatically.

---

# 💡 Objectives

The application is designed to:

- Automate attendance using facial recognition
- Detect faces through a webcam
- Maintain a registered face dataset
- Train a machine-learning classifier for identification
- Record name, roll number, and time
- Avoid duplicate attendance records
- Provide a simple browser-based interface
- Allow new users to be registered without manually editing the model

---

# ✨ Features

## 🎥 Real-Time Face Detection

The system uses OpenCV's Haar Cascade classifier:

```
haarcascade_frontalface_default.xml
```

The webcam stream is continuously analyzed for faces.

---

## 🧠 Face Recognition with KNN

The recognition model is created with:

```python
KNeighborsClassifier(n_neighbors=5)
```

Captured face images are resized to:

```
50 × 50
```

and flattened into feature vectors before being passed to the classifier.

---

## 👤 New User Registration

The application includes a registration workflow that:

- Accepts a new username
- Creates a dedicated folder for the user
- Opens the webcam
- Detects the user's face
- Captures **30 face images**
- Stores the captured images
- Retrains the KNN model
- Saves the updated model using Joblib

This allows the recognition database to grow directly from the application.

---

## ✅ Automatic Attendance

When a known face is recognized, the system extracts the registered username and roll number and records:

```
Name
Roll
Time
```

The current date determines the attendance CSV file.

Example:

```
Attendance/Attendance-09_11_26.csv
```

---

## 🚫 Duplicate Prevention

Before writing a new attendance record, the system checks whether the recognized user's roll number already exists in the current day's CSV file.

Conceptually:

```
Recognized User
      ↓
Read Today's CSV
      ↓
Roll Number Already Present?
      ├── Yes → Do Not Add Again
      └── No  → Add Attendance
```

---

## 📊 Live Attendance Dashboard

The web interface displays:

- Today's attendance
- Name
- Roll number
- Time
- Total registered users

The dashboard also provides a button to start the face-recognition process.

---

## 🎨 Interactive UI

The current interface includes:

- Dark modern dashboard
- Responsive layout
- Animated visual background
- Face-recognition themed design
- Live attendance table
- User-registration panel
- Registered-user statistics
- Responsive mobile styling

---

# 🧠 How Face Recognition Works

This project uses a two-stage computer-vision pipeline.

## Stage 1 — Face Detection

OpenCV's Haar Cascade detects possible faces inside the webcam frame.

```
Camera Frame
     ↓
Convert to Grayscale
     ↓
Haar Cascade
     ↓
Face Bounding Box
```

The implementation uses:

```python
cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

followed by:

```python
face_detector.detectMultiScale(
    gray,
    1.2,
    5,
    minSize=(20, 20)
)
```

---

## Stage 2 — User Identification

Once a face is detected:

```
Detected Face
     ↓
Resize to 50 × 50
     ↓
Flatten
     ↓
KNN Classifier
     ↓
Predicted User
```

The trained classifier is loaded from:

```
static/face_recognition_model.pkl
```

---

# 🔄 System Workflow

```
                   ┌────────────────────┐
                   │      Web App       │
                   └─────────┬──────────┘
                             │
                 ┌───────────┴───────────┐
                 ▼                       ▼
          Start Recognition        Add New User
                 │                       │
                 ▼                       ▼
          Open Webcam               Open Webcam
                 │                       │
                 ▼                       ▼
          Detect Face               Capture Images
                 │                       │
                 ▼                       ▼
          Resize Face              Store Face Data
                 │                       │
                 ▼                       ▼
        KNN Classification          Train KNN
                 │                       │
                 ▼                       ▼
          Identify User          Save Model (.pkl)
                 │
                 ▼
       Check Today's Attendance
                 │
          ┌──────┴──────┐
          │             │
       Already        New User
       Present            │
          │               ▼
          │         Write Attendance
          │               │
          └───────┬───────┘
                  ▼
           Display Dashboard
```

---

# 🧩 Detection & Recognition Pipeline

The implementation follows this sequence:

```
1. Capture webcam frame
2. Convert frame to grayscale
3. Detect face regions
4. Select the detected face
5. Resize the face to 50 × 50
6. Flatten the image into a feature vector
7. Load the saved KNN model
8. Predict the user's label
9. Extract name and roll number
10. Check today's CSV
11. Add attendance when not already present
```

---

# 👤 User Registration

The registration endpoint accepts a username from the dashboard.

Example:

```
Name entered
     ↓
Create static/faces/<name>_<id>/
     ↓
Open webcam
     ↓
Detect face
     ↓
Capture 30 images
     ↓
Save images
     ↓
Retrain KNN
     ↓
Save face_recognition_model.pkl
```

The current implementation captures one face image every five webcam iterations until 30 images have been stored.

---

# ✅ Attendance Marking

The attendance process is handled by the `/start` route.

When the webcam recognizes a registered face, the system generates:

```python
username = name.split('_')[0]
userid = name.split('_')[1]
```

and records the current time.

Attendance is written to:

```
Attendance/Attendance-MM_DD_YY.csv
```

with the columns:

```
Name,Roll,Time
```

Example:

| Name | Roll | Time |
|---|---:|---|
| Ajay | 2 | 10:32:18 |
| Aditya | 3 | 10:35:42 |

---

# 📊 Attendance Records

Attendance files are stored inside:

```
Attendance/
```

The repository contains multiple dated CSV examples.

The application creates a new daily CSV when the corresponding file does not yet exist.

Daily records are loaded with Pandas and shown on the dashboard.

---

# 🛠️ Technology Stack

## Backend

- Python
- Flask

## Computer Vision

- OpenCV
- Haar Cascade Classifier

## Machine Learning

- scikit-learn
- K-Nearest Neighbors (KNN)

## Data Processing

- Pandas
- NumPy

## Model Persistence

- Joblib

## Frontend

- HTML5
- CSS3
- Jinja templates
- Material Icons

---

# 🏗️ System Architecture

```
                    Browser
                       │
                       ▼
                ┌─────────────┐
                │    Flask    │
                │  Web Layer  │
                └──────┬──────┘
                       │
           ┌───────────┴───────────┐
           ▼                       ▼
      Dashboard              Recognition
                                  │
                                  ▼
                            OpenCV Webcam
                                  │
                                  ▼
                         Haar Face Detector
                                  │
                                  ▼
                          Face Preprocessing
                            (50 × 50)
                                  │
                                  ▼
                         KNN Classification
                                  │
                                  ▼
                       Recognized User Label
                                  │
                    ┌─────────────┴─────────────┐
                    ▼                           ▼
               CSV Attendance             Dashboard Table
```

---

# 📂 Project Structure

```
Face-Recognition-Attendance-System/
│
├── app.py
├── README.md
├── background.png
├── Interface.png
├── haarcascade_frontalface_default.xml
│
├── Attendance/
│   ├── Attendance-03_13_25.csv
│   ├── Attendance-07_10_24.csv
│   ├── Attendance-08_07_24.csv
│   └── ...
│
└── static/
    │
    ├── face_recognition_model.pkl
    │
    └── faces/
        ├── Aditya_3/
        ├── Ajay_2/
        ├── Virat_1/
        └── ...
```

---

# 🗃️ Model & Data Storage

## Face Dataset

Each registered user gets a directory under:

```
static/faces/
```

The directory naming convention is:

```
<username>_<user_id>
```

Example:

```
static/faces/Ajay_2/
static/faces/Aditya_3/
static/faces/Virat_1/
```

---

## Training Data

Each user directory contains captured face images.

The training pipeline:

```
Face Image
   ↓
Resize 50 × 50
   ↓
Flatten
   ↓
Feature Matrix
   +
User Labels
   ↓
KNN Training
```

The trained model is stored using Joblib:

```
static/face_recognition_model.pkl
```

---

# ⚙️ Installation

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/avaleajay170/Face-Recognition-Attendance-System.git
cd Face-Recognition-Attendance-System
```

---

## 2️⃣ Create a Virtual Environment

### Windows

```bash
python -m venv venv
venv\\Scripts\\activate
```

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3️⃣ Install Dependencies

Install the Python packages used by the application:

```bash
pip install flask opencv-python numpy pandas scikit-learn joblib
```

> The current GitHub tree does not show a root-level `requirements.txt`, so the command above reflects the libraries imported by `app.py`.

---

# ▶️ Running the Application

Start Flask:

```bash
python app.py
```

Then open:

```
http://127.0.0.1:5000
```

or:

```
http://localhost:5000
```

---

# 🎥 Running Face Recognition

From the dashboard:

```
Start Face Recognition
        ↓
Webcam Opens
        ↓
Face Detected
        ↓
User Identified
        ↓
Attendance Recorded
```

Press **ESC** in the OpenCV window to stop the recognition loop.

---

# ➕ Registering a New User

From the dashboard:

```
Add New User
     ↓
Enter Name
     ↓
Register New User
     ↓
Camera Opens
     ↓
30 Face Images Captured
     ↓
Model Retrained
```

After registration, the new user becomes part of the KNN training dataset.

---

# 🧪 Testing

Recommended test cases include:

| Test Case | Expected Result |
|---|---|
| Registered user appears on camera | User is identified |
| Same user appears again | Duplicate attendance is prevented |
| New user is registered | Face samples are stored |
| Model retraining completes | Updated `.pkl` model is created |
| No face is visible | No attendance is added |
| Attendance file does not exist | Daily CSV is created |
| ESC is pressed | Recognition window closes |

---

# ⚠️ Limitations & Security Considerations

This implementation is a practical academic/project prototype and has several limitations.

### Lighting & Camera Conditions

Face detection and classification can be affected by:

- Poor lighting
- Camera quality
- Face angle
- Occlusion
- Significant appearance changes

### Recognition Model

The current implementation uses a KNN classifier over flattened 50 × 50 pixel images. This is relatively simple compared with modern face-embedding or deep-learning approaches.

### Multiple Faces

The current recognition loop selects the first detected face rather than managing a full multi-person recognition pipeline.

### User ID Generation

New user IDs are generated from the number of user folders. Removing folders or changing the dataset structure could therefore affect ID allocation.

### Local Webcam Dependency

The recognition process expects access to a webcam on the machine running the application.

### Privacy

Face images are biometric-related data and should be handled carefully. In a production system, access control, secure storage, retention rules, and user consent should be considered.

### Production Security

The development application should not be exposed directly to the public internet without appropriate:

- Authentication
- HTTPS
- Access control
- Input validation
- Secure deployment configuration
- Logging and monitoring

---

# 🚀 Future Scope

## 🧠 Deep Face Embeddings

Replace raw-image KNN with modern facial embeddings using approaches such as:

- FaceNet
- ArcFace
- DeepFace-based pipelines

This can provide a stronger representation than flattened pixel values.

---

## 👥 Multi-Face Recognition

Support recognition of multiple students simultaneously:

```
Camera Frame
      ↓
Detect All Faces
      ↓
Recognize Each Face
      ↓
Validate Attendance
      ↓
Record Multiple Users
```

---

## 📍 Geolocation Integration

Combine face recognition with physical-location validation.

```
Face Verification
       +
Geolocation
       +
Time Window
       ↓
Attendance Decision
```

---

## 🔐 Liveness Detection

Add anti-spoofing measures to reduce the risk of attendance being marked using:

- Printed photographs
- Screens
- Replay attacks

---

## ☁️ Database Integration

Move from daily CSV files to a database such as:

- MySQL
- PostgreSQL
- MongoDB

This would make searching, reporting, and multi-user management easier.

---

## 📊 Advanced Analytics

Add:

- Attendance percentage
- Student-wise summaries
- Monthly reports
- Subject-wise analysis
- Trend charts
- Export to Excel/PDF

---

## 🌐 Production Deployment

The Flask application can be redesigned for deployment using:

```
Frontend
   ↓
Backend API
   ↓
Recognition Service
   ↓
Database
   ↓
Cloud Storage
```

---

# 🧠 Key Concepts Demonstrated

This project demonstrates practical use of:

- Computer Vision
- Face Detection
- Face Recognition
- Machine Learning Classification
- KNN
- OpenCV
- Flask
- Webcam Processing
- Dataset Management
- Model Serialization
- Pandas
- CSV-based data storage
- Real-time application design

---

# 📈 Project Snapshot

| Component | Implementation |
|---|---|
| Web Framework | Flask |
| Face Detection | Haar Cascade |
| Recognition | KNN |
| Training Images | 30 per registration |
| Face Size | 50 × 50 |
| Model Storage | Joblib `.pkl` |
| Attendance Storage | Daily CSV |
| Computer Vision | OpenCV |
| Data Processing | Pandas / NumPy |
| Camera | Local Webcam |
| UI | HTML / CSS / Jinja |

---

# 🤝 Contributing

Contributions are welcome.

```bash
git checkout -b feature/your-feature
```

Make your changes, then:

```bash
git add .
git commit -m "Add your feature"
git push origin feature/your-feature
```

Then open a Pull Request.

---

# 👨‍💻 Developer

<div align="center">

### Ajay Avale

Information Technology Student & Software Developer

<a href="https://github.com/avaleajay170">
  <img src="https://img.shields.io/badge/GitHub-avaleajay170-181717?style=for-the-badge&logo=github&logoColor=white">
</a>

</div>

---

# 📄 License

A license is not currently specified in the repository.

For public open-source distribution, consider adding a license such as the MIT License in a `LICENSE` file.

---

# ⭐ Support

If you find the project useful, consider giving the repository a ⭐ on GitHub.

<p align="center">

<strong>Face Detection → Recognition → Attendance</strong>

<br><br>

Built with Python, OpenCV, Flask & scikit-learn 🚀

</p>
