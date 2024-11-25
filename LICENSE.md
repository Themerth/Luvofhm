<!DOCTYPE html> 
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Celebration Website</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background-color: purple;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      font-family: Arial, sans-serif;
    }

    .container {
      position: relative;
      width: 100%;
      height: 100%;
    }

    .title {
      position: absolute;
      top: 30%;
      width: 100%;
      text-align: center;
      font-size: 32px;
      color: white;
      font-family: "Brush Script MT", cursive;
      text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
      z-index: 10;
    }

    .heart {
      font-size: 100px;
      cursor: pointer;
      text-shadow: 0 0 10px red, 0 0 20px red, 0 0 30px pink;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%) scale(1.2);
      transition: transform 0.3s;
      z-index: 10;
    }

    .heart:hover {
      transform: translate(-50%, -50%) scale(1.5);
    }

    .confetti-container {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 20;
    }

    .floating-photo {
      position: absolute;
      border: 5px solid white;
      border-radius: 15px;
      max-width: 150px;
      z-index: 1;
    }
.floating-photo {
  position: absolute;
  border: 5px solid white;
  border-radius: 15px;
  max-width: 150px;
  z-index: 1;

  /* Added properties to remove black areas */
  object-fit: cover;
  width: 150px;
  height: 250px; /* Adjust height as necessary */
  overflow: hidden;
}
.floating-photo {
  position: absolute;
  border: 5px solid white;
  border-radius: 50%; /* Makes the image round */
  width: 150px; /* Ensure width and height are equal */
  height: 150px; /* Ensure width and height are equal */
  object-fit: cover; /* Ensures the image fills the circular frame without distortion */
  z-index: 1;
}

}
.floating-photo {
  position: absolute;
  border: 5px solid white;
  border-radius: 50%; /* Keeps the image round */
  width: 250px; /* Increased size */
  height: 250px; /* Ensure width and height remain equal */
  object-fit: cover; /* Ensures the image fills the circular frame without distortion */
  z-index: 1;
}


    @keyframes fall {
      0% {
        transform: translateY(0);
      }
      100% {
        transform: translateY(100vh);
      }
    }

    .confetti-container div {
      position: absolute;
      animation-timing-function: ease-in;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="title">Happy Anniversary to the Beautiful Love of Hatice & Mert</div>
    <div class="heart" id="heart">❤️</div>
    <div class="confetti-container" id="confetti-container"></div>
    <div class="photos" id="photos">
      <img src="Screenshot_20241122-101531_WhatsApp.jpg" alt="Photo 1" class="floating-photo">
      <img src="Screenshot_20241122-101611_WhatsApp.jpg" alt="Photo 2" class="floating-photo">
      <img src="Screenshot_20241122-101251_WhatsApp.jpg" alt="Photo 3" class="floating-photo">
      <img src="Screenshot_20241122-101320_WhatsApp.jpg" alt="Photo 4" class="floating-photo">
      <img src="Screenshot_20241122-101352_WhatsApp.jpg" alt="Photo 5" class="floating-photo">
      <img src="Screenshot_20241122-101438_WhatsApp.jpg" alt="Photo 6" class="floating-photo">
      <img src="Screenshot_20241122-101713_WhatsApp.jpg" alt="Photo 7" class="floating-photo">
      <img src="Screenshot_20241122-133423_Gallery.jpg" alt="Photo 8" class="floating-photo">
      <img src="Screenshot_20241122-133859_Gallery.jpg" alt="Photo 9" class="floating-photo">
      <img src="Screenshot_20241122-133848_Gallery.jpg" alt="Photo 10" class="floating-photo">
    </div>
  </div>
 <script>
    // Confetti function
    function createConfetti() {
      const confettiContainer = document.getElementById('confetti-container');
      for (let i = 0; i < 200; i++) {
        const confetti = document.createElement('div');
        confetti.style.position = 'absolute';
        confetti.style.width = `${Math.random() * 10 + 5}px`;
        confetti.style.height = `${Math.random() * 10 + 5}px`;
        confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 100%, 50%)`;
        confetti.style.top = `-${Math.random() * 20}px`;
        confetti.style.left = `${Math.random() * window.innerWidth}px`;
        confetti.style.opacity = Math.random();
        confetti.style.animation = `fall ${Math.random() * 3 + 2}s linear infinite`;
        confetti.style.borderRadius = '50%';
        confettiContainer.appendChild(confetti);
      }
    }
    createConfetti();

    // Floating photo animation
    const photos = document.querySelectorAll('.floating-photo');
    const container = document.querySelector('.container');
    const containerWidth = container.offsetWidth;
    const containerHeight = container.offsetHeight;

    const images = Array.from(photos).map(photo => {
      const rect = photo.getBoundingClientRect();
      return {
        element: photo,
        x: Math.random() * (containerWidth - rect.width),
        y: Math.random() * (containerHeight - rect.height),
        dx: (Math.random() < 0.5 ? -1 : 1) * (Math.random() * 2 + 1), // Random horizontal speed
        dy: (Math.random() < 0.5 ? -1 : 1) * (Math.random() * 2 + 1), // Random vertical speed
        width: rect.width,
        height: rect.height,
      };
    });

    function moveImages() {
      images.forEach(image => {
        // Move the image
        image.x += image.dx;
        image.y += image.dy;

        // Screen boundary collision detection
        if (image.x <= 0 || image.x + image.width >= containerWidth) {
          image.dx = -image.dx;
          image.x = Math.max(0, Math.min(image.x, containerWidth - image.width)); // Prevent overflow
        }
        if (image.y <= 0 || image.y + image.height >= containerHeight) {
          image.dy = -image.dy;
          image.y = Math.max(0, Math.min(image.y, containerHeight - image.height)); // Prevent overflow
        }

        // Update position
        image.element.style.left = `${image.x}px`;
        image.element.style.top = `${image.y}px`;
      });

      requestAnimationFrame(moveImages);
    }

    // Initialize positions
    images.forEach(image => {
      image.element.style.left = `${image.x}px`;
      image.element.style.top = `${image.y}px`;
    });

    moveImages();

    const heart = document.getElementById('heart');
    const confettiContainer = document.getElementById('confetti-container');
    let songPlayed = false; // Track if the song has already been played

    // Create an audio object for the song
    const backgroundMusic = new Audio('This I Love.mp3');
    backgroundMusic.loop = true; // Enable looping

    function createSmallHearts() {
      for (let i = 0; i < 30; i++) {
        const smallHeart = document.createElement('div');
        smallHeart.textContent = '❤️';
        smallHeart.style.position = 'absolute';
        smallHeart.style.fontSize = '20px';
        smallHeart.style.top = '0';
        smallHeart.style.left = `${Math.random() * 100}%`;
        smallHeart.style.animation = `fall ${Math.random() * 3 + 2}s ease-in infinite`;
        smallHeart.style.opacity = `${Math.random()}`;
        confettiContainer.appendChild(smallHeart);

        setTimeout(() => smallHeart.remove(), 5000); // Remove after animation
      }
    }

    heart.addEventListener('click', () => {
      createConfetti();
      createSmallHearts();

      if (!songPlayed) {
        backgroundMusic.play(); // Play the song
        songPlayed = true; // Set the flag to true
      }
    });
  </script>
