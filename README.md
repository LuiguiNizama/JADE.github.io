# JADE.github.io
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Para Mi Papita ❤️‍🩹 - Flores Amarillas</title>
  <!-- Bootstrap 5 CSS -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
  <!-- FontAwesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  
  <style>
    :root {
      --primary-yellow: #ffda08;
      --glow-yellow: #fff066;
      --stem-green: #2b9348;
      --bg-dark: #0a0f24;
    }

    body {
      background: radial-gradient(circle at center, #1a237e, #0a0f24);
      min-height: 100vh;
      color: #fff;
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      overflow-x: hidden;
      position: relative;
    }

    /* Fondo animado interactivo */
    #canvas-bg {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 1;
      pointer-events: none;
    }

    .main-container {
      position: relative;
      z-index: 10;
    }

    /* Carta / Notita Responsiva */
    .note-card {
      background: linear-gradient(145deg, #fffdf0, #fef3c7);
      color: #333;
      border: 3px solid #f59e0b;
      border-radius: 20px;
      box-shadow: 0 10px 25px rgba(245, 158, 11, 0.3);
      cursor: pointer;
      transition: all 0.3s ease-in-out;
      width: 100%;
    }

    .note-card:hover {
      transform: translateY(-5px) scale(1.02);
      box-shadow: 0 15px 35px rgba(245, 158, 11, 0.5);
    }

    .heart-beat {
      display: inline-block;
      color: #dc2626;
      animation: pulse 1.2s infinite ease-in-out;
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.25); }
    }

    /* Jardín de Flores Adaptaflo */
    .garden {
      min-height: 300px;
      max-height: 420px;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: flex-end;
      flex-wrap: nowrap;
      overflow: visible;
      padding-bottom: 10px;
    }

    .flower-wrapper {
      position: relative;
      bottom: 0;
      cursor: pointer;
      transition: transform 0.3s ease;
      transform-origin: bottom center;
      flex: 0 1 auto;
    }

    .flower-wrapper:hover {
      transform: scale(1.08) rotate(2deg);
    }

    /* Ajuste responsivo para el tamaño de las flores */
    .flower-wrapper svg {
      width: 100%;
      height: auto;
      max-height: 360px;
    }

    /* Estilos adaptativos en pantalla móvil */
    @media (max-width: 576px) {
      .display-5 {
        font-size: 1.8rem;
      }
      
      .note-card h2 {
        font-size: 1.25rem !important;
      }

      .garden {
        min-height: 240px;
      }

      .flower-wrapper svg {
        max-height: 230px;
      }

      .btn-custom {
        width: 100%;
        padding: 10px 18px;
        font-size: 0.95rem;
      }
    }

    /* Botones de acción */
    .btn-custom {
      background: linear-gradient(135deg, #f59e0b, #d97706);
      border: none;
      color: white;
      font-weight: 600;
      border-radius: 50px;
      padding: 12px 28px;
      box-shadow: 0 5px 15px rgba(245, 158, 11, 0.4);
      transition: all 0.3s ease;
    }

    .btn-custom:hover {
      background: linear-gradient(135deg, #fbbf24, #f59e0b);
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(245, 158, 11, 0.6);
      color: white;
    }

    /* Ventana Modal Responsiva */
    .modal-content {
      background: linear-gradient(135deg, #fffbeb, #fef3c7);
      border: 3px solid #f59e0b;
      border-radius: 20px;
      color: #1f2937;
    }
  </style>
</head>
<body>

  <!-- Partículas de Fondo -->
  <canvas id="canvas-bg"></canvas>

  <div class="container main-container py-4 py-md-5 text-center">
    <!-- Encabezado -->
    <header class="mb-3 mb-md-4">
      <span class="badge bg-warning text-dark fs-6 px-3 py-2 rounded-pill mb-2">
        <i class="fa-solid fa-sparkles me-1"></i> MI PAPITA
      </span>
      <h1 class="fw-bold display-5 text-warning">CON TODO MI AMOR</h1>
      <p class="text-light opacity-75 small fs-md-6">Mi vida toca las flores o la pantalla para q veas la magia ✨</p>
    </header>
        <!-- Notita Interactiva -->
    <div class="row justify-content-center mb-4 px-2">
      <div class="col-12 col-sm-10 col-md-8 col-lg-6">
        <div class="note-card p-3 p-md-4" data-bs-toggle="modal" data-bs-target="#noteModal">
          <div class="d-flex align-items-center justify-content-center gap-2">
            <i class="fa-solid fa-envelope-open-text fs-3 text-warning"></i>
            <h2 class="m-0 fw-bold fs-3 text-dark">
              TE AMO MI PAPITA <span class="heart-beat">❤️‍🩹</span>
            </h2>
          </div>
          <small class="text-muted d-block mt-2 fs-7"><i class="fa-solid fa-hand-pointer"></i> PRESIONA AQUI BEBE</small>
        </div>
      </div>
    </div>

    <!-- Ramo de Flores SVG -->
    <div class="garden mb-4 px-1" id="flowerGarden">
      <!-- Flor Lateral Izquierda -->
      <div class="flower-wrapper" onclick="burstSparks(event)">
        <svg viewBox="0 0 120 320" width="100" height="280">
          <path d="M60,320 Q50,200 60,100" stroke="#2b9348" stroke-width="8" fill="none" stroke-linecap="round"/>
          <path d="M58,220 Q20,200 30,170 Q55,190 58,220" fill="#2b9348"/>
          <g transform="translate(60, 100)">
            <g class="petals">
              <ellipse cx="0" cy="-35" rx="12" ry="30" fill="#ffda08"/>
              <ellipse cx="0" cy="35" rx="12" ry="30" fill="#ffda08"/>
              <ellipse cx="-35" cy="0" rx="30" ry="12" fill="#ffda08"/>
              <ellipse cx="35" cy="0" rx="30" ry="12" fill="#ffda08"/>
              <ellipse cx="-25" cy="-25" rx="12" ry="30" fill="#ffea00" transform="rotate(-45)"/>
              <ellipse cx="25" cy="25" rx="12" ry="30" fill="#ffea00" transform="rotate(-45)"/>
              <ellipse cx="-25" cy="25" rx="12" ry="30" fill="#ffea00" transform="rotate(45)"/>
              <ellipse cx="25" cy="-25" rx="12" ry="30" fill="#ffea00" transform="rotate(45)"/>
            </g>
            <circle cx="0" cy="0" r="22" fill="#78350f"/>
            <circle cx="0" cy="0" r="18" fill="#92400e" stroke="#b45309" stroke-width="2"/>
          </g>
        </svg>
      </div>

      <!-- Flor Central Principal -->
      <div class="flower-wrapper" onclick="burstSparks(event)">
        <svg viewBox="0 0 150 360" width="130" height="340">
          <path d="M75,360 Q85,220 75,90" stroke="#2b9348" stroke-width="10" fill="none" stroke-linecap="round"/>
          <path d="M77,240 Q120,220 100,180 Q80,210 77,240" fill="#2b9348"/>
          <path d="M73,270 Q30,250 50,210 Q70,240 73,270" fill="#2b9348"/>
          <g transform="translate(75, 90)">
            <g class="petals">
              <ellipse cx="0" cy="-45" rx="15" ry="38" fill="#ffc107"/>
              <ellipse cx="0" cy="45" rx="15" ry="38" fill="#ffc107"/>
              <ellipse cx="-45" cy="0" rx="38" ry="15" fill="#ffc107"/>
              <ellipse cx="45" cy="0" rx="38" ry="15" fill="#ffc107"/>
              <ellipse cx="-32" cy="-32" rx="15" ry="38" fill="#ffda08" transform="rotate(-45)"/>
              <ellipse cx="32" cy="32" rx="15" ry="38" fill="#ffda08" transform="rotate(-45)"/>
              <ellipse cx="-32" cy="32" rx="15" ry="38" fill="#ffda08" transform="rotate(45)"/>
              <ellipse cx="32" cy="-32" rx="15" ry="38" fill="#ffda08" transform="rotate(45)"/>
            </g>
            <circle cx="0" cy="0" r="28" fill="#451a03"/>
            <circle cx="0" cy="0" r="22" fill="#78350f" stroke="#d97706" stroke-width="3"/>
          </g>
        </svg>
      </div>

      <!-- Flor Lateral Derecha -->
      <div class="flower-wrapper" onclick="burstSparks(event)">
        <svg viewBox="0 0 120 300" width="100" height="260">
          <path d="M60,300 Q70,180 60,90" stroke="#2b9348" stroke-width="8" fill="none" stroke-linecap="round"/>
          <path d="M62,190 Q100,170 90,140 Q70,160 62,190" fill="#2b9348"/>
          <g transform="translate(60, 90)">
            <g class="petals">
              <ellipse cx="0" cy="-35" rx="12" ry="30" fill="#ffda08"/>
              <ellipse cx="0" cy="35" rx="12" ry="30" fill="#ffda08"/>
              <ellipse cx="-35" cy="0" rx="30" ry="12" fill="#ffda08"/>
              <ellipse cx="35" cy="0" rx="30" ry="12" fill="#ffda08"/>
              <ellipse cx="-25" cy="-25" rx="12" ry="30" fill="#ffea00" transform="rotate(-45)"/>
              <ellipse cx="25" cy="25" rx="12" ry="30" fill="#ffea00" transform="rotate(-45)"/>
              <ellipse cx="-25" cy="25" rx="12" ry="30" fill="#ffea00" transform="rotate(45)"/>
              <ellipse cx="25" cy="-25" rx="12" ry="30" fill="#ffea00" transform="rotate(45)"/>
            </g>
            <circle cx="0" cy="0" r="22" fill="#78350f"/>
            <circle cx="0" cy="0" r="18" fill="#92400e" stroke="#b45309" stroke-width="2"/>
          </g>
        </svg>
      </div>
    </div>

    <!-- Botones de Acción Adaptables -->
    <div class="d-flex flex-column flex-sm-row justify-content-center align-items-center gap-3 max-w-sm mx-auto">
      <button class="btn btn-custom w-100 w-sm-auto" onclick="triggerHearts()">
        <i class="fa-solid fa-heart me-2"></i>  VER CORAZONCITOS
      </button>
      <button class="btn btn-custom w-100 w-sm-auto" onclick="addExtraFlower()">
        <i class="fa-solid fa-seedling me-2"></i> VER FLORCITAS
      </button>
    </div>
  </div>

  <!-- Modal / Mensaje Emergente -->
  <div class="modal fade" id="noteModal" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog modal-dialog-centered modal-sm-down">
      <div class="modal-content text-center p-3 p-md-4">
        <div class="modal-header border-0 pb-0">
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <i class="fa-solid fa-heart-circle-bolt display-4 text-danger mb-3 heart-beat"></i>
          <h3 class="fw-bold text-dark mb-3 fs-4 fs-md-3">¡Para Ti, Mi Papita! ❤️‍🩹</h3>
          <p class="fs-6 text-secondary">
            Estas flores amarillas son para ti, para iluminar tu día tal como tú iluminas el mío. 
            Gracias por estar a mi lado y mi amor que aun que haya dias dificiles yo siempre 
            te elejire por que te amo con el alma , yo jamas podria seguir sin ti mi papita te amo
            como no tienes idea yo te amare hasta mi ultimo aliento.
            
          </p>
          <div class="p-3 bg-warning-subtle rounded-4 mt-3">
            <h5 class="fw-bold text-warning-emphasis m-0">TE AMO CON TODO MI CORAZÓN</h5>
          </div>
        </div>
        <div class="modal-footer border-0 justify-content-center pt-0">
          <button type="button" class="btn btn-warning px-4 rounded-pill fw-bold" data-bs-dismiss="modal">
            ¡Te Amo Más! 🥰
          </button>
        </div>
      </div>
    </div>
  </div>

  <!-- Bootstrap JS Bundle -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

  <!-- Lógica JavaScript para Canvas y Animaciones -->
  <script>
    const canvas = document.getElementById('canvas-bg');
    const ctx = canvas.getContext('2d');

    let particles = [];
    let width = canvas.width = window.innerWidth;
    let height = canvas.height = window.innerHeight;

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    });

    class Particle {
      constructor(x, y, type = 'glow') {
        this.x = x || Math.random() * width;
        this.y = y || Math.random() * height;
        this.type = type;
        this.size = type === 'heart' ? Math.random() * 12 + 8 : Math.random() * 3 + 1.5;
        this.speedX = Math.random() * 2 - 1;
        this.speedY = type === 'heart' ? -(Math.random() * 2.5 + 1) : Math.random() * -0.8 - 0.3;
        this.color = type === 'heart' ? '#ef4444' : '#fef08a';
        this.opacity = 1;
        this.life = type === 'heart' ? 90 : Math.random() * 180 + 80;
      }

      update() {
        this.x += this.speedX;
        this.y += this.speedY;
        this.life--;
        if (this.type === 'heart') {
          this.opacity = this.life / 90;
        }
      }

      draw() {
        ctx.save();
        ctx.globalAlpha = this.opacity;
        if (this.type === 'heart') {
          ctx.fillStyle = this.color;
          ctx.font = `${this.size}px Arial`;
          ctx.fillText('❤️', this.x, this.y);
        } else {
          ctx.fillStyle = this.color;
          ctx.beginPath();
          ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
          ctx.fill();
        }
        ctx.restore();
      }
    }

    function initParticles() {
      const density = window.innerWidth < 576 ? 20 : 40;
      for (let i = 0; i < density; i++) {
        particles.push(new Particle());
      }
    }

    function animate() {
      ctx.clearRect(0, 0, width, height);
      
      const maxParticles = window.innerWidth < 576 ? 30 : 50;
      if (particles.length < maxParticles && Math.random() < 0.25) {
        particles.push(new Particle(Math.random() * width, height + 10));
      }

      particles.forEach((p, index) => {
        p.update();
        p.draw();
        if (p.life <= 0 || p.y < -20) {
          particles.splice(index, 1);
        }
      });

      requestAnimationFrame(animate);
    }

    initParticles();
    animate();

    // Eventos táctiles y de clic adaptados
    window.addEventListener('click', (e) => {
      if (e.target.tagName !== 'BUTTON' && !e.target.closest('.note-card') && !e.target.closest('.modal')) {
        for (let i = 0; i < 6; i++) {
          particles.push(new Particle(e.clientX, e.clientY, 'glow'));
        }
      }
    });

    function triggerHearts() {
      const count = window.innerWidth < 576 ? 18 : 30;
      for (let i = 0; i < count; i++) {
        setTimeout(() => {
          particles.push(new Particle(Math.random() * width, height + 10, 'heart'));
        }, i * 70);
      }
    }

    function burstSparks(e) {
      e.stopPropagation();
      const rect = e.currentTarget.getBoundingClientRect();
      const x = rect.left + rect.width / 2;
      const y = rect.top + rect.height / 3;
      
      for (let i = 0; i < 10; i++) {
        particles.push(new Particle(x, y, 'heart'));
      }
    }

    function addExtraFlower() {
      const garden = document.getElementById('flowerGarden');
      if (garden.children.length >= 5) return; // Límite para no sobrecargar pantallas pequeñas

      const newFlower = document.createElement('div');
      newFlower.className = 'flower-wrapper';
      newFlower.onclick = burstSparks;
      newFlower.innerHTML = `
        <svg viewBox="0 0 110 280" width="90" height="240">
          <path d="M55,280 Q45,160 55,80" stroke="#2b9348" stroke-width="7" fill="none" stroke-linecap="round"/>
          <g transform="translate(55, 80)">
            <g class="petals">
              <ellipse cx="0" cy="-30" rx="10" ry="25" fill="#facc15"/>
              <ellipse cx="0" cy="30" rx="10" ry="25" fill="#facc15"/>
              <ellipse cx="-30" cy="0" rx="25" ry="10" fill="#facc15"/>
              <ellipse cx="30" cy="0" rx="25" ry="10" fill="#facc15"/>
            </g>
            <circle cx="0" cy="0" r="18" fill="#78350f"/>
          </g>
        </svg>
      `;
      garden.appendChild(newFlower);
    }
  </script>
</body>
</html>
