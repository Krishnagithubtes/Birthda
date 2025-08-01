<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Happy Birthday!</title>
  <link rel="stylesheet" href="style.css">
	body {
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
  
  /* Balloons */
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
  

</head>
<body>
  <div class="container">
    <div class="photo-frame">
      <img src="images/her-photo.jpg" alt="Her Photo">
    </div>
    <h1 class="greeting">🎉 Happy Birthday! 🎂</h1>
    <p class="message">Wishing you all the joy and love in the world on your special day.</p>
  </div>

  <!-- Balloons Container -->
  <div id="balloons-container"></div>

  <script src="script.js"></script>
</body>
</html>
