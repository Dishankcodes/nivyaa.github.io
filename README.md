<html>   
<head>
  <style>
:root {
  --primary-color: #ff00ff;
  --secondary-color: #00ffff;
  --text-color: #fff;
}

body {
  margin: 0;
  padding: 0;
  background-color: #000;
  background: url('https://images.unsplash.com/photo-1503264116251-35a269479413?auto=format&fit=crop&w=1950&q=80') no-repeat center center fixed;
  background-size: cover;
      
  color: var(--text-color);
  font-family: "Poppins", sans-serif;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
  transition: background-color 2s ease;
}

body.sad-theme {
  background-color: #1a1a2e;
}

.sad-theme .wishes {
  color: #a5a5a5;
}

.sad-theme .star {
  animation: slowTwinkle 4s infinite;
}

@keyframes slowTwinkle {
  0%,
  100% {
    opacity: 0.1;
  }

  50% {
    opacity: 0.3;
  }
}

.stars {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.star {
  position: absolute;
  background: #fff;
  border-radius: 50%;
  animation: twinkle var(--duration) infinite;
}

@keyframes twinkle {
  0%,
  100% {
    opacity: 0.2;
  }

  50% {
    opacity: 1;
  }
}

.start-btn,
.choice-btn {
  padding: 15px 30px;
  font-size: 20px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(255, 255, 255, 0.5);
  border-radius: 10px;
  color: white;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 2;
}

.start-btn {
  animation: glow 2s infinite;
}

.choice-btn {
  margin: 10px;
  font-size: 18px;
  opacity: 0;
}

.start-btn:hover,
.choice-btn:hover {
  background: rgba(255, 255, 255, 0.2);
  border-color: rgba(255, 255, 255, 0.8);
  box-shadow: 0 0 20px rgba(255, 255, 255, 0.3);
  transform: translateY(-2px);
}

@keyframes glow {
  0% {
    box-shadow: 0 0 20px rgba(255, 0, 255, 0.5);
  }

  50% {
    box-shadow: 0 0 40px rgba(255, 0, 255, 0.8);
  }

  100% {
    box-shadow: 0 0 20px rgba(255, 0, 255, 0.5);
  }
}

.hidden {
  display: none;
}

.wishes {
  text-align: center;
  font-size: 24px;
  margin: 20px;
  opacity: 0;
  font-family: "Dancing Script", cursive;
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
}

.emoji {
  position: absolute;
  font-size: 30px;
  pointer-events: none;
  z-index: 1;
}

.neon-text {
  text-shadow: 0 0 10px var(--primary-color), 0 0 20px var(--primary-color),
    0 0 30px var(--primary-color);
}

.message-container {
  max-width: 90%;
  width: 800px;
  text-align: center;
  padding: 30px;
  position: relative;
  z-index: 1;
}

@keyframes floatUp {
  0% {
    transform: translateY(0) translateX(0);
    opacity: 0;
  }

  10% {
    opacity: 1;
  }

  90% {
    opacity: 1;
  }

  100% {
    transform: translateY(-100vh) translateX(var(--random-x));
    opacity: 0;
  }
}

.mute-btn {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 2px solid rgba(255, 255, 255, 0.5);
  color: white;
  font-size: 24px;
  cursor: pointer;
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.mute-btn:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(1.1);
}

    </style>
</head>
<body id="body" onclick="fullScreen()">
  <div class="stars"></div>
  <button class="start-btn" id="startBtn">Click to Start ✨</button>
  <div id="wishesContainer" class="hidden">
    <div id="wishes" class="wishes"></div>
    <div id="choices" class="hidden">
      <button class="choice-btn" onclick="makeChoice('')">Aunty</button>
      <button class="choice-btn" onclick="makeChoice('bestfriend')">Best Friend</button>
    </div>
  </div>

  <audio id="bgMusic" src="https://hindi.djpunjab.app/load/MLNyCd86wmLEJPdPIiSd8Q==/Badhai%20Ho%20Badhai%20Janm%20Din%20Ki.mp3" loop></audio>
   <audio id="bestFriendMusic" src="https://hindi.djpunjab.app/load/cPnz7r4F4iEtdhKQGvl6Jw==/Yaara%20Teri%20Yaari%20Happy.mp3" loop></audio>

  <button id="muteButton" class="mute-btn">🔊</button>
<script>
    const wishes = [
  "Happiestt 19th Birthdayy Nivyaaaaaa... 🌟",
  "On your special day... ✨",
  "You are as rare and beautiful as the stars ✨",
  "This day is special because you were born on it! 🎂",
  "From your smile to your soul, you glow!💕",
  "Happy Birthday! 😚💕🌸🎂",
  
];

const bestFriendMessages = [
  "Yaara teri yaari ko maine toh khuda mana 🌟",
  "Teri dosti ne mujhe jeena sikhaya hai ✨",
  "Tere jaisa yaar kaha, kaha aisa yarana 💖",
  "Dosti ki hai, nibhani to padegi💕",
  "Koi dhundta hai kisi ko,😚",
  "Koi kisi ka sahara hai 🌟",
  "You're not just my friend Nivyaaaa,",
  "You're my favorite person to annoy! 😋",
  "Let's be Best Friends Forever! 🤗"
];

function createStars() {
  const starsContainer = document.createElement("div");
  starsContainer.className = "stars";
  for (let i = 0; i < 200; i++) {
    const star = document.createElement("div");
    star.className = "star";
    star.style.width = `${Math.random() * 3}px`;
    star.style.height = star.style.width;
    star.style.left = `${Math.random() * 100}%`;
    star.style.top = `${Math.random() * 100}%`;
    star.style.setProperty("--duration", `${Math.random() * 3 + 1}s`);
    starsContainer.appendChild(star);
  }
  document.body.appendChild(starsContainer);
}

function createEmoji() {
  const emojis = ["💖", "🌸", "✨", "🌼", "🎂", "🎈","🌻"];
  const emoji = document.createElement("div");
  emoji.className = "emoji";
  emoji.textContent = emojis[Math.floor(Math.random() * emojis.length)];
  emoji.style.left = Math.random() * window.innerWidth + "px";
  emoji.style.top = "-50px";
  document.body.appendChild(emoji);
  const animation = emoji.animate(
    [
      {
        transform: "translateY(0) rotate(0deg)"
      },
      {
        transform: `translateY(${window.innerHeight + 50}px) rotate(${
          Math.random() * 360
        }deg)`
      }
    ],
    {
      duration: 3000,
      easing: "linear"
    }
  );
  animation.onfinish = () => emoji.remove();
}

function stopAllMusic() {
  const audios = ["bgMusic", "GirlfriendMusic"];
  audios.forEach((id) => {
    const audio = document.getElementById(id);
    if (audio) {
      audio.pause();
      audio.currentTime = 0;
    }
  });
}

function playAudio(audioId) {
  const audio = document.getElementById(audioId);
  if (audio) {
    audio.volume = 0.5;
    audio.play().catch((err) => console.log("Audio play failed:", err));
  }
}
let emojiInterval;
async function typeWriter(text) {
  const wishesElement = document.getElementById("wishes");
  wishesElement.style.opacity = 1;
  wishesElement.innerHTML = "";
  wishesElement.className = "wishes neon-text";
  for (let char of text) {
    wishesElement.innerHTML += char;
    await new Promise((resolve) => setTimeout(resolve, 100));
  }
  await new Promise((resolve) => setTimeout(resolve, 1000));
}
let isMuted = false;
const muteButton = document.getElementById("muteButton");
muteButton.addEventListener("click", () => {
  const audios = ["bgMusic", "sisterMusic", "bestFriendMusic"];
  isMuted = !isMuted;
  audios.forEach((id) => {
    const audio = document.getElementById(id);
    if (audio) {
      audio.muted = isMuted;
    }
  });
  // Update button text
  muteButton.textContent = isMuted ? "🔇" : "🔊";
});
async function makeChoice(choice) {
  clearInterval(emojiInterval);
  const wishesElement = document.getElementById("wishes");
  document.getElementById("choices").style.display = "none";
  stopAllMusic();
  if (choice === "Aunty") {
    document.body.classList.add("sad-theme");
    const sisterAudio = document.getElementById("sisterMusic");
    sisterAudio.muted = isMuted;
    try {
      const playPromise = sisterAudio.play();
      if (playPromise !== undefined) {
        playPromise.catch((error) => {
          console.log("Audio play failed:", error);
        });
      }
    } catch (err) {
      console.log("Audio play failed:", err);
    }
    for (let message of sisterChat) {
      await typeWriter(message);
    }
    document.getElementById("choices").innerHTML = `
                    <button class="choice-btn" onclick="makeChoice('bestfriend')">Best Friend</button>
                `;
    document.getElementById("choices").style.display = "block";
    document.querySelector(".choice-btn").style.opacity = 1;
  } else {
    document.body.classList.remove("sad-theme");
    const bestFriendAudio = document.getElementById("bestFriendMusic");
    bestFriendAudio.muted = isMuted;
    try {
      const playPromise = bestFriendAudio.play();
      if (playPromise !== undefined) {
        playPromise.catch((error) => {
          console.log("Audio play failed:", error);
        });
      }
    } catch (err) {
      console.log("Audio play failed:", err);
    }
    emojiInterval = setInterval(createEmoji, 300);
    for (let message of bestFriendMessages) {
      await typeWriter(message);
    }
    setTimeout(() => {
      setTimeout(() => {
        window.open(
          "https://www.instagram.com/direct/t/harshpreet_singh_honey",
          "_blank"
        );
        wishesElement.innerHTML =
          "Check your Whtsapp Nivyudiii, !📱✨<br>💖I am there💖";
      }, 1000);
    }, 2000);
  }
}
document.getElementById("startBtn").addEventListener("click", async () => {
  document.getElementById("startBtn").style.display = "none";
  document.getElementById("wishesContainer").classList.remove("hidden");
  const bgAudio = document.getElementById("bgMusic");
  bgAudio.muted = isMuted;
  try {
    const playPromise = bgAudio.play();
    if (playPromise !== undefined) {
      playPromise.catch((error) => {
        console.log("Audio play failed:", error);
      });
    }
  } catch (err) {
    console.log("Audio play failed:", err);
  }
  emojiInterval = setInterval(createEmoji, 300);
  for (let wish of wishes) {
    await typeWriter(wish);
  }
  document.getElementById("choices").classList.remove("hidden");
  document.querySelectorAll(".choice-btn").forEach((btn) => {
    btn.style.opacity = 1;
  });
});
document.addEventListener("click", async function initAudio() {
  const audios = ["bgMusic", "sisterMusic", "bestFriendMusic"];
  for (let id of audios) {
    const audio = document.getElementById(id);
    try {
      await audio.play();
      audio.pause();
      audio.currentTime = 0;
    } catch (err) {
      console.log("Audio initialization failed:", err);
    }
  }
  document.removeEventListener("click", initAudio);
});

createStars();
let honey = document.getElementById("body");
function fullScreen() {
  honey.requestFullscreen();
}

  </script>
  </html>
