# Weebb
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Let me take you out?</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      gap: 3rem;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 25%, #f093fb 50%, #4facfe 75%, #00f2fe 100%);
      background-size: 400% 400%;
      animation: gradientShift 8s ease infinite;
      padding: 2rem;
    }

    @keyframes gradientShift {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    h1 {
      font-size: 56px;
      font-weight: 800;
      margin: 0;
      color: white;
      text-shadow: 0 6px 20px rgba(0,0,0,0.3);
    }

    .button-container {
      display: flex;
      gap: 3rem;
      align-items: center;
      justify-content: center;
      position: relative;
      z-index: 1;
    }

    button {
      border: none;
      border-radius: 50px;
      cursor: pointer;
      transition: all 0.2s ease;
      white-space: nowrap;
      font-weight: 700;
      font-size: 22px;
    }

    #yesBtn {
      padding: 20px 60px;
      font-size: 28px;
      border: 4px solid white;
      background: #ff2d55;
      color: white;
      box-shadow: 0 10px 30px rgba(255, 45, 85, 0.5);
      letter-spacing: 1px;
    }

    #yesBtn:hover {
      box-shadow: 0 15px 40px rgba(255, 45, 85, 0.7);
    }

    #noBtn {
      padding: 18px 50px;
      font-size: 22px;
      border: 3px solid white;
      background: #b19cd9;
      color: white;
      box-shadow: 0 6px 20px rgba(177, 156, 217, 0.4);
      text-shadow: 0 1px 3px rgba(0,0,0,0.2);
      position: fixed;
      z-index: 100;
      right: 30px;
      bottom: 30px;
    }

    #result {
      text-align: center;
      min-height: 50px;
      font-size: 24px;
      font-weight: 700;
      color: white;
      text-shadow: 0 3px 10px rgba(0,0,0,0.3);
    }
  </style>
</head>
<body>
  <h1>Let me take you out?</h1>
  
  <div class="button-container">
    <button id="yesBtn">❤️ YES ❤️</button>
    <button id="noBtn">No</button>
  </div>
  
  <div id="result"></div>

  <script>
    const yesBtn = document.getElementById('yesBtn');
    const noBtn = document.getElementById('noBtn');
    const result = document.getElementById('result');

    const formUrl = 'https://forms.office.com/Pages/ResponsePage.aspx?id=DQSIkWdsW0yxEjajBLZtrQAAAAAAAAAAAAa__RCgiR5UMTJUNVVWNjRLNkxBNTdVRERZTFBRVTJGVS4u';

    let yesScale = 1;
    let yesClicks = 0;

    function moveNoButton() {
      const noBtnWidth = noBtn.offsetWidth;
      const noBtnHeight = noBtn.offsetHeight;
      const yesBtnRect = yesBtn.getBoundingClientRect();
      
      let randomX, randomY;
      let overlap = true;
      let attempts = 0;
      
      while (overlap && attempts < 50) {
        randomX = Math.random() * (window.innerWidth - noBtnWidth);
        randomY = Math.random() * (window.innerHeight - noBtnHeight);
        
        const noRect = {
          left: randomX,
          top: randomY,
          right: randomX + noBtnWidth,
          bottom: randomY + noBtnHeight
        };
        
        overlap = !(noRect.right < yesBtnRect.left - 30 || 
                   noRect.left > yesBtnRect.right + 30 || 
                   noRect.bottom < yesBtnRect.top - 30 || 
                   noRect.top > yesBtnRect.bottom + 30);
        
        attempts++;
      }
      
      noBtn.style.left = randomX + 'px';
      noBtn.style.top = randomY + 'px';
      noBtn.style.right = 'auto';
      noBtn.style.bottom = 'auto';
    }

    setTimeout(function() {
      moveNoButton();
    }, 100);

    yesBtn.addEventListener('click', function() {
      yesClicks++;
      yesScale += 0.3;
      yesBtn.style.transform = `scale(${yesScale})`;
      yesBtn.style.padding = `${20 * yesScale}px ${60 * yesScale}px`;
      yesBtn.style.fontSize = `${28 * yesScale}px`;
      
      if (yesClicks === 1) {
        result.textContent = '✨ Best choice! Opening form... ✨';
      } else if (yesClicks === 2) {
        result.textContent = '🎉 Even better the second time! 🎉';
      } else if (yesClicks === 3) {
        result.textContent = '💕 You\'re committed! 💕';
      } else {
        result.textContent = '💫 This is true love! 💫';
      }
      
      window.open(formUrl, '_blank');
    });

    yesBtn.addEventListener('mouseover', function() {
      yesBtn.style.transform = `scale(${yesScale + 0.1})`;
      yesBtn.style.boxShadow = '0 15px 40px rgba(255, 45, 85, 0.7)';
    });

    yesBtn.addEventListener('mouseout', function() {
      yesBtn.style.transform = `scale(${yesScale})`;
      yesBtn.style.boxShadow = '0 10px 30px rgba(255, 45, 85, 0.5)';
    });

    noBtn.addEventListener('mouseover', function() {
      moveNoButton();
    });

    noBtn.addEventListener('click', function(e) {
      e.preventDefault();
      moveNoButton();
    });

    noBtn.addEventListener('mouseenter', function() {
      moveNoButton();
    });
  </script>
</body>
</html>
