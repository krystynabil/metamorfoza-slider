<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8">
  <title>Metamorfoza</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
    }
    #compare {
      position: relative;
      width: 100%;
      max-width: 900px;
      margin: 0 auto;
      aspect-ratio: 16 / 9;
      overflow: hidden;
      cursor: ew-resize;
      touch-action: none;
    }
    #compare img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
      pointer-events: none;
    }
    #overlay {
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 50%;
      overflow: hidden;
      z-index: 2;
    }
    #slider {
      position: absolute;
      top: 0;
      left: calc(50% - 10px);
      width: 20px;
      height: 100%;
      background: rgba(255, 255, 255, 0.5);
      border-left: 2px solid #000;
      border-right: 2px solid #000;
      z-index: 3;
      cursor: ew-resize;
    }
  </style>
</head>
<body>
  <div id="compare">
    <img src="ban%20pojed.png" alt="Po metamorfozie">
    <div id="overlay">
      <img src="ban%20po.png" alt="Przed metamorfozą">
    </div>
    <div id="slider"></div>
  </div>

  <script>
    const compare = document.getElementById('compare');
    const overlay = document.getElementById('overlay');
    const slider = document.getElementById('slider');

    let isDragging = false;

    function updateSlider(x) {
      const rect = compare.getBoundingClientRect();
      let offsetX = x - rect.left;
      offsetX = Math.max(0, Math.min(offsetX, rect.width));
      overlay.style.width = offsetX + 'px';
      slider.style.left = (offsetX - 10) + 'px';
    }

    slider.addEventListener('mousedown', () => isDragging = true);
    window.addEventListener('mouseup', () => isDragging = false);
    window.addEventListener('mousemove', (e) => {
      if (isDragging) updateSlider(e.clientX);
    });

    slider.addEventListener('touchstart', () => isDragging = true);
    window.addEventListener('touchend', () => isDragging = false);
    window.addEventListener('touchmove', (e) => {
      if (isDragging && e.touches.length) {
        updateSlider(e.touches[0].clientX);
      }
    });
  </script>
</body>
</html>
