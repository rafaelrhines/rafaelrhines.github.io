<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Android Camera Viewer</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      background: #000;
      margin: 0;
      height: 100vh;
    }
    video {
      width: 100%;
      height: auto;
      max-height: 100vh;
    }
  </style>
</head>
<body>
  <video id="camera" autoplay playsinline></video>

  <script>
    async function startCamera() {
      try {
        const constraints = {
          video: {
            facingMode: "environment" // back camera
          },
          audio: false
        };
        const stream = await navigator.mediaDevices.getUserMedia(constraints);
        const videoElement = document.getElementById("camera");
        videoElement.srcObject = stream;
      } catch (error) {
        console.error("Error accessing camera:", error);
        alert("Camera access denied or not supported.");
      }
    }

    startCamera();
  </script>
</body>
</html>
