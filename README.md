<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>أداة إنشاء فيديو</title>
  <style>
    body {
      font-family: Arial;
      background-color: #f9f9f9;
      text-align: center;
      padding: 30px;
    }
    h1 {
      color: #333;
    }
    input, textarea, button {
      margin: 10px;
      padding: 10px;
      width: 300px;
      font-size: 16px;
    }
    video, img {
      margin-top: 20px;
      max-width: 100%;
    }
  </style>
</head>
<body>

  <h1>🔤 إنشاء فيديو من النص</h1>
  <textarea id="textInput" placeholder="اكتب النص هنا..."></textarea><br>
  <button onclick="createTextVideo()">أنشئ فيديو من النص</button>
  <video id="textVideo" controls></video>

  <hr style="margin: 40px 0;">

  <h1>🖼️ إنشاء فيديو من صورة</h1>
  <input type="file" id="imageInput" accept="image/*"><br>
  <button onclick="createImageVideo()">أنشئ فيديو من الصورة</button>
  <video id="imageVideo" controls></video>

  <script>
    // إنشاء فيديو بسيط من النص باستخدام Web Speech API + canvas
    function createTextVideo() {
      const text = document.getElementById("textInput").value;
      if (!text) return alert("من فضلك أدخل نصًا!");

      const speech = new SpeechSynthesisUtterance(text);
      speech.lang = "ar-SA";
      speechSynthesis.speak(speech);

      const blob = new Blob([text], { type: "text/plain" });
      const url = URL.createObjectURL(blob);

      const video = document.getElementById("textVideo");
      video.src = "https://www.w3schools.com/html/mov_bbb.mp4"; // فيديو وهمي مؤقت للعرض
    }

    // إنشاء فيديو مبسط من صورة (تحريك تلقائي بسيط)
    function createImageVideo() {
      const input = document.getElementById("imageInput");
      const file = input.files[0];
      if (!file) return alert("اختر صورة أولاً!");

      const url = URL.createObjectURL(file);
      const canvas = document.createElement("canvas");
      const ctx = canvas.getContext("2d");
      const img = new Image();

      img.onload = function() {
        canvas.width = img.width;
        canvas.height = img.height;

        let frames = [];
        let frameCount = 30;

        for (let i = 0; i < frameCount; i++) {
          ctx.clearRect(0, 0, canvas.width, canvas.height);
          ctx.globalAlpha = 1 - (i / frameCount); // تأثير بسيط
          ctx.drawImage(img, 0, 0);
          frames.push(canvas.toDataURL("image/webp"));
        }

        const video = document.getElementById("imageVideo");
        video.src = "https://www.w3schools.com/html/mov_bbb.mp4"; // مؤقت حتى نستخدم مكتبة فيديو فعلية
      }

      img.src = url;
    }
  </script>
</body>
</html>

     
 
