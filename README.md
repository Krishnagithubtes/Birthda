import os
import shutil

# Set up file names and directories
project_dir = 'birthday_page'
image_dir = os.path.join(project_dir, 'images')
image_source = 'her-photo.jpg'  # <-- Make sure this file exists in the same folder as the script
image_target = os.path.join(image_dir, 'her-photo.jpg')

# Create necessary directories
os.makedirs(image_dir, exist_ok=True)

# HTML content
html_content = '''<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Happy Birthday!</title>
  <link rel="stylesheet" href="style.css">
  <meta property="og:title" content="🎂 Happy Birthday!" />
  <meta property="og:description" content="Click to see your surprise!" />
  <meta property="og:image" content="images/her-photo.jpg" />
  <meta property="og:url" content="#" />
</head>
<body>
  <div class="container">
    <div class="photo-frame">
      <img src="images/her-photo.jpg" alt="Her Photo">
    </div>
    <h1 class="greeting">🎉 Happy Birthday! 🎂</h1>
    <p class="message">Wishing you all the joy and love in the world on your special day.</p>
  </div>
  <div id="balloons-container"></div>
  <script src="script.js"></script>
</body>
</html>
'''

# CSS content
css_content = '''body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(to top right, #ffd6e8, #ffe6f2);
  overflow: hidden;
}
.container {
  text-align: center;
  margin-top: 60px;
  animation: fadeIn 2s ease-in-out;
}
.photo-frame {
  width: 200px;
  height: 200px;
  margin: 0 auto;
  border: 6px solid #fff;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  animation: bounce 2s infinite alternate;
}
.photo-frame img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.greeting {
  color: #ff1493;
  font-size: 3rem;
  margin: 20px 0 10px;
}
.message {
  font-size: 1.3rem;
  color: #555;
}
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-30px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes bounce {
  0% { transform: translateY(0); }
  100% { transform: translateY(-10px); }
}
#balloons-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}
.balloon {
  position: absolute;
  bottom: -100px;
  width: 40px;
  height: 60px;
  background-color: red;
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
  animation: float 8s linear infinite;
}
@keyframes float {
  0% {
    transform: translateY(0) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(-110vh) rotate(360deg);
    opacity: 0;
  }
}
'''

# JS content
js_content = '''const balloonColors = ['#ff69b4', '#ffa07a', '#87cefa', '#98fb98', '#dda0dd'];

function createBalloon() {
  const balloon = document.createElement('div');
  balloon.className = 'balloon';
  balloon.style.left = Math.random() * 100 + 'vw';
  balloon.style.backgroundColor = balloonColors[Math.floor(Math.random() * balloonColors.length)];
  balloon.style.animationDuration = (6 + Math.random() * 5) + 's';
  document.getElementById('balloons-container').appendChild(balloon);
  setTimeout(() => { balloon.remove(); }, 10000);
}
setInterval(createBalloon, 500);
'''

# Save all files
with open(os.path.join(project_dir, 'index.html'), 'w', encoding='utf-8') as f:
    f.write(html_content)

with open(os.path.join(project_dir, 'style.css'), 'w', encoding='utf-8') as f:
    f.write(css_content)

with open(os.path.join(project_dir, 'script.js'), 'w', encoding='utf-8') as f:
    f.write(js_content)

# Copy her photo
if os.path.isfile(image_source):
    shutil.copy(image_source, image_target)
    print(f"[✔] Copied image: {image_source} → {image_target}")
else:
    print(f"[!] WARNING: Image file not found at {image_source}. Please add it manually to /images/ folder.")

# Zip the whole project
shutil.make_archive(project_dir, 'zip', project_dir)
print(f"[✔] Birthday webpage created in ./{project_dir}")
print(f"[✔] ZIP file ready: {project_dir}.zip")
print("\n✅ You can now upload it to Netlify, GitHub Pages, or any static host.")
