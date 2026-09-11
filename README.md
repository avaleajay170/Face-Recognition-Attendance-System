<div align="center">

# 🎭 FaceAttend
### Face Recognition Based Attendance System

<p>
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/OpenCV-Computer%20Vision-red?style=for-the-badge&logo=opencv&logoColor=white">
  <img src="https://img.shields.io/badge/Flask-Web%20Framework-black?style=for-the-badge&logo=flask&logoColor=white">
  <img src="https://img.shields.io/badge/HTML5-Frontend-orange?style=for-the-badge&logo=html5&logoColor=white">
  <img src="https://img.shields.io/badge/CSS3-Styling-blue?style=for-the-badge&logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/JavaScript-Interactive-yellow?style=for-the-badge&logo=javascript&logoColor=black">
</p>

<p>
  <img src="https://img.shields.io/github/stars/avaleajay170/Face-Recognition-Attendance-System?style=flat-square">
  <img src="https://img.shields.io/github/forks/avaleajay170/Face-Recognition-Attendance-System?style=flat-square">
  <img src="https://img.shields.io/github/license/avaleajay170/Face-Recognition-Attendance-System?style=flat-square">
</p>

<p>
  <b>🚀 Automate attendance using Computer Vision & Face Recognition</b>
</p>

</div>

---

## ✨ About The Project

**FaceAttend** is a web-based **Face Recognition Attendance System** designed to automate the process of recording attendance.

Instead of manually marking attendance, the system uses a camera to detect and recognize registered faces. Once a person is successfully recognized, their attendance is recorded automatically along with relevant information such as their name, roll number, and timestamp.

The project combines **Computer Vision, Face Recognition, Python, OpenCV, and Flask** to provide a simple and interactive attendance management solution.

---

## 🎯 Why FaceAttend?

Traditional attendance systems can be:

- ⏳ Time-consuming
- 📝 Manual
- ❌ Prone to human errors
- 🔄 Difficult to maintain for large groups
- 📊 Inefficient for repeated attendance tracking

FaceAttend provides an automated alternative where attendance can be recorded through facial recognition.

---

# 🚀 Key Features

<table>
<tr>
<td width="50%">

### 👤 Face Recognition
Automatically detects and recognizes registered faces using computer vision.

</td>
<td width="50%">

### 📸 Camera Based Attendance
Uses a camera to capture faces and process them in real time.

</td>
</tr>

<tr>
<td>

### 🕒 Automatic Timestamp
Records the time when attendance is marked.

</td>
<td>

### 📊 Attendance Dashboard
Displays attendance records through an interactive web interface.

</td>
</tr>

<tr>
<td>

### ➕ Add New Users
Allows new users to be registered into the system.

</td>
<td>

### 💾 Attendance Storage
Attendance information is maintained using CSV-based records.

</td>
</tr>

<tr>
<td>

### 🌐 Flask Web Application
Provides a browser-based interface for interacting with the system.

</td>
<td>

### 🎨 Modern UI
Responsive dark-themed interface with animated visual elements.

</td>
</tr>
</table>

---

# 🧠 How The System Works

```mermaid
flowchart TD

    A[👤 User] --> B[📷 Camera]

    B --> C[🔍 Face Detection]

    C --> D[🧠 Face Recognition]

    D --> E{Face Recognized?}

    E -->|Yes| F[👤 Identify User]

    E -->|No| G[❌ Unknown Face]

    F --> H[📝 Record Attendance]

    H --> I[🕒 Add Timestamp]

    I --> J[💾 Store Attendance]

    J --> K[🌐 Flask Dashboard]

    G --> K