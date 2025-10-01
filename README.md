<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Anaglyph Camera Split</title>
  <style>
    body {
      margin: 0;
      background: black;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
    }
    .container {
      display: flex;
      gap: 20px; /* spacing between red & cyan copies */
    }
    video {
      width: 48vw;  /* each video ~half screen */
      height: auto;
      object-fit: cover;
    }
    .red {
      filter: grayscale(100%) brightness(100%) sepia(100%) hue-rotate(-50deg) saturate(800%);
    }
    .cyan {
      filter: grayscale(100%) brightness(100%) sepia(100%) hue-rotate(180deg) saturate(800%);
    }
  </style>
</head>
<body>
  <div class="container">
    <video id="camRed" autoplay playsinline muted class="red"></video>
    <video id="camCyan" autoplay playsinline muted class="cyan"></video>
  </div>

  <script>
    async function startCamera() {
      try {
        const constraints = {
          video: { facingMode: "environment" },
          audio: false
        };
        const stream = await navigator.mediaDevices.getUserMedia(constraints);

        document.getElementById("camRed").srcObject = stream;
        document.getElementById("camCyan").srcObject = stream;
      } catch (err) {
        console.error("Camera error:", err);
        alert("Camera access denied or unsupported.");
      }
    }

    startCamera();
  </script>
</body>
</html>
