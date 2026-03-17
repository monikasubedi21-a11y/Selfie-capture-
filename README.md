<!DOCTYPE html>
<html>
<head>
  <title>Selfie Capture</title>
</head>
<body style="text-align:center; font-family:sans-serif;">
  <h2>Camera Access Required 📷</h2>
  <video id="video" width="300" autoplay></video>
  <br><br>
  <button onclick="startCapture()">Start Capturing</button>
  <div id="photos"></div>

<script>
let video = document.getElementById('video');

navigator.mediaDevices.getUserMedia({ video: true })
.then(stream => {
  video.srcObject = stream;
})
.catch(err => {
  alert("Camera permission denied!");
});

function takePhoto() {
  let canvas = document.createElement("canvas");
  canvas.width = 300;
  canvas.height = 220;
  let ctx = canvas.getContext("2d");
  ctx.drawImage(video, 0, 0, canvas.width, canvas.height);

  document.getElementById("photos").appendChild(canvas);
}

function startCapture() {
  let count = 0;
  let interval = setInterval(() => {
    takePhoto();
    count++;
    if(count == 3){
      clearInterval(interval);
      alert("3 Photos Captured ✅");
    }
  }, 2000);
}
</script>

</body>
</html>
