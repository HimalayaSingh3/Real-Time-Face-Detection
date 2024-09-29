# Face Detection Using JavaScript

## Overview

This project implements face detection in web applications using JavaScript. Leveraging modern libraries and APIs, it provides a simple yet effective way to identify faces in images or video streams. This README will guide you through the setup, usage, and customization of the face detection functionality.

## Features

- Real-time face detection from webcam feed
- Image upload support for static images
- Customizable detection parameters
- Lightweight and efficient performance

## Technologies Used

- **JavaScript**: Core programming language for implementation.
- **HTML5**: For structuring the web application.
- **CSS**: For styling the application.
- **TensorFlow.js**: For machine learning capabilities.
- **Face-api.js**: A JavaScript library that simplifies face detection.

## Getting Started

### Prerequisites

Make sure you have the following installed:

- A modern web browser (Chrome, Firefox, etc.)
- Node.js (for local development)

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/HimalayaSingh3/Face-Detection-js.git
   cd face-detection-js
   ```

2. **Install Dependencies**:
   If using a package manager, run:
   ```bash
   npm install
   ```

3. **Open `index.html`**:
   Open the `index.html` file in your preferred web browser to see the application in action.

### Usage

1. **Real-time Detection**:
   - Allow access to your webcam when prompted.
   - The application will start detecting faces in real-time.

2. **Image Upload**:
   - Click on the "Upload Image" button to select an image from your device.
   - The application will process the image and display detected faces.

### Customization

You can customize various aspects of the face detection process:

- **Detection Model**: Change the model used for face detection by modifying the model path in the script.
- **Detection Parameters**: Adjust parameters such as score threshold and input size for better accuracy.

### Example Code Snippet

Here’s a basic example of how to set up face detection:

```javascript
const video = document.getElementById('videoElement');
const canvas = document.getElementById('canvas');
const context = canvas.getContext('2d');

async function setupCamera() {
    const stream = await navigator.mediaDevices.getUserMedia({
        video: true,
    });
    video.srcObject = stream;
    return new Promise((resolve) => {
        video.onloadedmetadata = () => {
            resolve(video);
        };
    });
}

async function detectFaces() {
    const net = await faceapi.nets.tinyFaceDetector.loadFromUri('/models');
    await faceapi.nets.faceLandmark68Net.loadFromUri('/models');
    await faceapi.nets.faceRecognitionNet.loadFromUri('/models');

    const options = new faceapi.TinyFaceDetectorOptions();
    
    setInterval(async () => {
        const detections = await faceapi.detectAllFaces(video, options).withFaceLandmarks().withFaceDescriptors();
        context.drawImage(video, 0, 0);
        faceapi.draw.drawDetections(canvas, detections);
    }, 100);
}

setupCamera().then(detectFaces);
```

## Contributing

Contributions are welcome! If you have suggestions or improvements, please fork the repository and submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [TensorFlow.js](https://www.tensorflow.org/js)
- [face-api.js](https://github.com/justadudewhohacks/face-api.js)

---
