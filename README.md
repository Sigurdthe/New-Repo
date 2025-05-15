<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PowerFit - Your Ultimate Fitness Companion</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    :root {
      --primary-color: #00ff88;
      --secondary-color: #00cc66;
      --background-color: #1a1a1a;
      --card-background: #2d2d2d;
      --text-color: #ffffff;
      --section-spacing: 4rem;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', system-ui, sans-serif;
    }

    body {
      background-color: var(--background-color);
      color: var(--text-color);
      line-height: 1.6;
    }

    /* Enhanced Navigation */
    .navbar {
      background-color: rgba(34, 34, 34, 0.95);
      padding: 1rem 5%;
      position: fixed;
      width: 100%;
      top: 0;
      z-index: 1000;
      display: flex;
      justify-content: space-between;
      align-items: center;
      backdrop-filter: blur(10px);
    }

    .auth-buttons {
    display: flex;
    gap: 1rem;
  }

  .auth-button {
    background: var(--primary-color);
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    cursor: pointer;
    transition: transform 0.2s;
  }

  .modal {
    display: none;
    position: fixed;
    z-index: 1001;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.7);
  }

  .modal-content {
    position: relative;
    background: var(--card-background);
    margin: 15% auto;
    padding: 2rem;
    width: 90%;
    max-width: 400px;
    border-radius: 10px;
  }

  .close {
      position: absolute;
      right: 20px;
      top: 10px;
      color: #aaa;
      font-size: 28px;
      font-weight: bold;
      cursor: pointer;
    }

    .close:hover {
      color: var(--text-color);
    }

    #formSwitch {
      display: flex;
      gap: 1rem;
      margin: 1rem 0;
      justify-content: center;
    }

    .switch-active {
      color: var(--primary-color);
      cursor: pointer;
      font-weight: bold;
    }

    #authForm input {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      background: #333;
      border: none;
      border-radius: 4px;
      color: white;
    }

    .logo {
      font-size: 1.5rem;
      color: var(--primary-color);
      text-decoration: none;
      font-weight: 700;
    }

    .nav-links {
      display: flex;
      gap: 2rem;
    }

    .nav-links a {
      color: var(--text-color);
      text-decoration: none;
      font-weight: 500;
      transition: color 0.3s;
      position: relative;
    }

    .nav-links a::after {
      content: '';
      position: absolute;
      bottom: -5px;
      left: 0;
      width: 0;
      height: 2px;
      background-color: var(--primary-color);
      transition: width 0.3s;
    }

    .nav-links a:hover::after {
      width: 100%;
    }

    .nav-links a.active {
      color: var(--primary-color);
    }

    .hamburger {
      display: none;
      color: var(--text-color);
      font-size: 1.5rem;
      cursor: pointer;
    }

    /* Hero Section */
    .hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      text-align: center;
      padding: 8rem 5% 4rem;
      background: linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.7)),
        url('https://images.unsplash.com/photo-1571019614242-c5c5dee9f50b') center/cover;
    }

    .hero h1 {
      font-size: 3.5rem;
      margin-bottom: 1.5rem;
      line-height: 1.2;
    }

    .hero p {
      font-size: 1.2rem;
      max-width: 600px;
      margin-bottom: 2rem;
    }

    /* Exercise Grid */
    .exercise-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 2rem;
      width: 100%;
      max-width: 1200px;
      margin: 2rem auto;
    }

    .exercise-card {
      background: var(--card-background);
      border-radius: 15px;
      overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
      cursor: pointer;
      position: relative;
    }

    .exercise-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    .exercise-card img {
      width: 100%;
      height: 250px;
      object-fit: cover;
      transition: transform 0.3s;
    }

    .exercise-card:hover img {
      transform: scale(1.05);
    }

    .exercise-info {
      padding: 1.5rem;
    }

    .exercise-info h3 {
      margin-bottom: 0.5rem;
      color: var(--primary-color);
    }

    .exercise-info p {
      color: #cccccc;
      font-size: 0.9rem;
    }

    /* CTA Button */
    .cta-button {
      display: inline-flex;
      align-items: center;
      gap: 0.5rem;
      background-color: var(--primary-color);
      color: var(--background-color);
      padding: 1rem 2rem;
      border-radius: 30px;
      text-decoration: none;
      font-weight: 600;
      transition: transform 0.3s, background-color 0.3s;
    }

    .cta-button:hover {
      transform: translateY(-2px);
      background-color: var(--secondary-color);
    }

    /* Mobile Responsive */
    @media (max-width: 768px) {
      .hamburger {
        display: block;
      }

      .nav-links {
        position: fixed;
        top: 4rem;
        right: -100%;
        flex-direction: column;
        background: var(--card-background);
        width: 100%;
        max-width: 250px;
        padding: 1rem;
        transition: right 0.3s;
      }

      .nav-links.active {
        right: 0;
      }

      .hero h1 {
        font-size: 2.5rem;
      }

      .exercise-grid {
        grid-template-columns: 1fr;
      }
    }

    /* New Features */
    .section-header {
      text-align: center;
      margin-bottom: 3rem;
    }

    .section-header h2 {
      font-size: 2.5rem;
      margin-bottom: 1rem;
    }

    .feature-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 2rem;
      padding: 2rem 5%;
    }

    .feature-card {
      background: var(--card-background);
      padding: 2rem;
      border-radius: 15px;
      text-align: center;
    }

    .feature-card i {
      font-size: 2.5rem;
      color: var(--primary-color);
      margin-bottom: 1rem;
    }

    .progress-tracker {
      background: var(--card-background);
      padding: 2rem;
      border-radius: 15px;
      margin: 2rem 5%;
    }

    .dropdown {
      position: relative;
    }

    .dropdown-content {
      display: none;
      position: absolute;
      top: 100%;
      left: 0;
      background: var(--card-background);
      min-width: 200px;
      border-radius: 8px;
      box-shadow: 0 8px 16px rgba(0,0,0,0.2);
      z-index: 1;
    }

    .dropdown:hover .dropdown-content {
      display: block;
    }

    .dropdown-content a {
      color: var(--text-color);
      padding: 12px 16px;
      text-decoration: none;
      display: block;
      transition: background 0.3s;
    }

    .dropdown-content a:hover {
      background: rgba(255,255,255,0.1);
    }
    
    
  </style>
</head>
<body>
  <header>
    <nav class="navbar">
      <a href="index.html" class="logo">PowerFit</a>
      <ul class="nav-links">
        <li><a href="index.html" class="active">Home</a></li>
        <li class="dropdown">
          <a href="exercices.html">Exercises ▾</a>
          <div class="dropdown-content">
            <a href="gym.html">Gym Workouts</a>
            <a href="calisthenics.html">Calisthenics</a>
            <a href="cardio.html">Cardio</a>
            <a href="flexibility.html">Flexibility</a>
          </div>
        </li>
        <li><a href="conseils.html">Programs</a></li>
        <li><a href="contact.html">Contact</a></li>
      </ul>
      <div class="auth-buttons">
        <button id="loginBtn" class="auth-button">Login</button>
        <button id="signupBtn" class="auth-button">Sign Up</button>
      </div>
      
      <div id="authModal" class="modal">
        <div class="modal-content">
          <span class="close">&times;</span>
          <form id="authForm">
            <h2>Welcome to PowerFit</h2>
            <div id="formSwitch">
              <span class="switch-active">Sign Up</span>
              <span>Login</span>
            </div>
            <input type="email" id="email" placeholder="Email" required>
            <input type="password" id="password" placeholder="Password" required>
            <button type="submit" class="cta-button">Get Started</button>
          </form>
        </div>
      </div>
      <i class="hamburger fas fa-bars"></i>
    </nav>
  </header>

  <main>
    <section class="hero">
      <h1>Transform Your Body, <br>Boost Your Confidence</h1>
      <p>Your personalized fitness journey starts here</p>
      
      <div class="exercise-grid">
        <a href="gym.html" style="text-decoration: none;" class="exercise-card">
          <img src="https://www.fastandup.in/nutrition-world/wp-content/uploads/2023/05/Workouts-for-Men.jpg" alt="Gym Workouts">
          <div class="exercise-info">
            <h3>Gym Workouts</h3>
            <p>Full-body training with professional equipment</p>
          </div>
        </a>

        <a href="calisthenics.html" style="text-decoration: none;" class="exercise-card">
          <img src="https://gravity.fitness/cdn/shop/articles/Calisthenics_Exercises_Every-Body_should_master_from_beginner_to_advanced.jpg?v=1711239686&width=2048" alt="Calisthenics">
          <div class="exercise-info">
            <h3>Calisthenics</h3>
            <p>Bodyweight mastery and functional training</p>
          </div>
        </a>
      </div>
    </section>

    <!-- New Features Section -->
    <section class="features">
      <div class="section-header">
        <h2>Why Choose PowerFit?</h2>
      </div>
      <div class="feature-grid">
        <div class="feature-card">
          <i class="fas fa-dumbbell"></i>
          <h3>Personalized Programs</h3>
          <p>Custom workout plans tailored to your goals</p>
        </div>
        <div class="feature-card">
          <i class="fas fa-apple-alt"></i>
          <h3>Nutrition Guides</h3>
          <p>Optimize your diet for maximum results</p>
        </div>
        <div class="feature-card">
          <i class="fas fa-chart-line"></i>
          <h3>Progress Tracking</h3>
          <p>Monitor your improvements over time</p>
        </div>
      </div>
    </section>

    <!-- Progress Tracker Section -->
    <div class="progress-tracker">
      <h3>Your Weekly Progress</h3>
      <div class="progress-bar">
        <!-- Add progress bar implementation -->
      </div>
    </div>
  </main>

  <script>
    // Auth System
    const users = JSON.parse(localStorage.getItem('users')) || [];
  
    function handleAuth(isLogin) {
      const email = document.getElementById('email').value;
      const password = document.getElementById('password').value;
      
      if(isLogin) {
        const user = users.find(u => u.email === email && u.password === password);
        if(user) {
          localStorage.setItem('currentUser', JSON.stringify(user));
          alert('Login successful!');
        } else {
          alert('Invalid credentials!');
        }
      } else {
        const newUser = { email, password, programs: [] };
        users.push(newUser);
        localStorage.setItem('users', JSON.stringify(users));
        localStorage.setItem('currentUser', JSON.stringify(newUser));
        alert('Registration successful!');
      }
    }
    document.addEventListener('DOMContentLoaded', function () {
      const hamburger = document.querySelector('.hamburger');
      const navLinks = document.querySelector('.nav-links');

      // Hamburger menu toggle
      hamburger.addEventListener('click', () => {
        navLinks.classList.toggle('active');
      });

      // Smooth scroll
      document.querySelectorAll('a[href^="#"]').forEach(anchor => {
        anchor.addEventListener('click', function (e) {
          e.preventDefault();
          document.querySelector(this.getAttribute('href')).scrollIntoView({
            behavior: 'smooth'
          });
        });
      });

      // Close mobile menu on click outside
      document.addEventListener('click', (e) => {
        if (!hamburger.contains(e.target) && !navLinks.contains(e.target)) {
          navLinks.classList.remove('active');
        }
      });
    });
    // Modal handling
    const modal = document.getElementById('authModal');
    const loginBtn = document.getElementById('loginBtn');
    const signupBtn = document.getElementById('signupBtn');
    const closeBtn = document.querySelector('.close');
    const formSwitch = document.querySelectorAll('#formSwitch span');

    // Show modal
    function showModal(isLogin) {
      modal.style.display = 'block';
      document.getElementById('formSwitch').children[isLogin ? 1 : 0].classList.add('switch-active');
      document.getElementById('formSwitch').children[isLogin ? 0 : 1].classList.remove('switch-active');
    }

    // Event listeners
    loginBtn.addEventListener('click', () => showModal(true));
    signupBtn.addEventListener('click', () => showModal(false));
    
    closeBtn.addEventListener('click', () => {
      modal.style.display = 'none';
    });

    window.addEventListener('click', (e) => {
      if (e.target === modal) {
        modal.style.display = 'none';
      }
    });

    // Form switch
    formSwitch.forEach(span => {
      span.addEventListener('click', () => {
        formSwitch.forEach(s => s.classList.remove('switch-active'));
        span.classList.add('switch-active');
      });
    });

    // Auth form submission
    document.getElementById('authForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const isLogin = document.querySelector('#formSwitch .switch-active').textContent === 'Login';
      handleAuth(isLogin);
      modal.style.display = 'none';
    });
  </script>
</body>
</html>