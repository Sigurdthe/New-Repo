<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PowerFit - Coach Profile</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
  <style>
    /* Optimize CSS by removing duplicates and using more efficient selectors */
    :root {
      --primary-color: #00ff88;
      --secondary-color: #00cc66;
      --background-color: #1a1a1a;
      --card-background: #2d2d2d;
      --text-color: #ffffff;
      --section-spacing: 4rem;
      --transition-speed: 0.3s;
    }

    /* Base styles */
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

    /* Optimize animations */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Use CSS containment for better performance */
    .program-grid {
      contain: content;
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      padding: 2rem 5%;
    }

    .program-card {
      contain: layout style paint;
      background: var(--card-background);
      border-radius: 15px;
      overflow: hidden;
      transition: transform var(--transition-speed);
      will-change: transform;
    }

    .program-card:hover {
      transform: translateY(-5px);
    }

    .program-card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
      transition: transform var(--transition-speed);
    }

    .program-card:hover img {
      transform: scale(1.05);
    }

    /* Optimize filter buttons */
    .filter-buttons {
      display: flex;
      gap: 1rem;
      justify-content: center;
      margin: 2rem 0;
      flex-wrap: wrap;
    }

    .filter-btn {
      background: var(--card-background);
      border: none;
      padding: 0.5rem 1.5rem;
      border-radius: 20px;
      color: var(--text-color);
      cursor: pointer;
      transition: background-color var(--transition-speed);
    }

    .filter-btn:hover,
    .filter-btn.active {
      background: var(--primary-color);
      color: var(--background-color);
    }

    /* Use hardware acceleration for animations */
    .program-info {
      padding: 1.5rem;
      transform: translateZ(0);
    }

    .program-title {
      color: var(--primary-color);
      margin-bottom: 0.5rem;
    }

    .program-description {
      color: #cccccc;
      font-size: 0.9rem;
      margin-bottom: 1rem;
    }

    .program-meta {
      display: flex;
      gap: 1rem;
      color: var(--primary-color);
      font-size: 0.9rem;
    }

    /* Optimize navigation */
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
      transform: translateZ(0);
    }

    /* Use CSS containment for better performance */
    .nav-links {
      contain: content;
      display: flex;
      gap: 2rem;
      list-style: none;
    }

    .nav-links a {
      color: var(--text-color);
      text-decoration: none;
      font-weight: 500;
      transition: color var(--transition-speed);
    }

    .nav-links a:hover {
      color: var(--primary-color);
    }

    /* Dropdown styles */
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
      background: var(--primary-color);
      color: var(--background-color);
    }

    /* Optimize mobile menu */
    @media (max-width: 768px) {
      .nav-links {
        position: fixed;
        top: 4rem;
        right: -100%;
        flex-direction: column;
        background: var(--card-background);
        width: 100%;
        max-width: 250px;
        padding: 1rem;
        transition: right var(--transition-speed);
      }

      .nav-links.active {
        right: 0;
      }

      .program-grid {
        grid-template-columns: 1fr;
      }
    }

    /* Coach Profile Section */
    .coach-profile {
      display: grid;
      grid-template-columns: 1fr 2fr;
      gap: 2rem;
      padding: 8rem 5% 4rem;
    }

    .profile-image {
      width: 100%;
      border-radius: 15px;
      overflow: hidden;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    .profile-image img {
      width: 100%;
      height: auto;
      display: block;
    }

    .profile-info {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .profile-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .profile-name {
      font-size: 2.5rem;
      color: var(--primary-color);
    }

    .profile-rating {
      display: flex;
      gap: 0.5rem;
      color: #ffd700;
    }

    .profile-tags {
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
    }

    .profile-tag {
      background: rgba(0, 255, 136, 0.1);
      color: var(--primary-color);
      padding: 0.25rem 0.75rem;
      border-radius: 20px;
      font-size: 0.8rem;
    }

    .profile-bio {
      font-size: 1.1rem;
      line-height: 1.8;
      color: #cccccc;
    }

    .profile-stats {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1rem;
      margin-top: 1rem;
    }

    .stat-item {
      background: var(--card-background);
      padding: 1rem;
      border-radius: 10px;
      text-align: center;
    }

    .stat-value {
      font-size: 1.5rem;
      color: var(--primary-color);
      font-weight: 700;
    }

    .stat-label {
      font-size: 0.9rem;
      color: #cccccc;
    }

    /* Programs Section */
    .programs-section {
      padding: 4rem 5%;
    }

    .section-title {
      font-size: 2rem;
      color: var(--primary-color);
      margin-bottom: 2rem;
      text-align: center;
    }

    /* Testimonials Section */
    .testimonials-section {
      padding: 4rem 5%;
      background: var(--card-background);
    }

    .testimonial-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 2rem;
      margin-top: 2rem;
    }

    .testimonial-card {
      background: var(--background-color);
      padding: 1.5rem;
      border-radius: 15px;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }

    .testimonial-header {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .testimonial-avatar {
      width: 50px;
      height: 50px;
      border-radius: 50%;
      overflow: hidden;
    }

    .testimonial-avatar img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }

    .testimonial-info h4 {
      color: var(--primary-color);
    }

    .testimonial-info p {
      font-size: 0.9rem;
      color: #cccccc;
    }

    .testimonial-content {
      font-style: italic;
      color: #cccccc;
    }

    .testimonial-rating {
      color: #ffd700;
    }

    /* Achievements Section */
    .achievements-section {
      padding: 4rem 5%;
    }

    .achievements-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 2rem;
      margin-top: 2rem;
    }

    .achievement-card {
      background: var(--card-background);
      padding: 1.5rem;
      border-radius: 15px;
      text-align: center;
      transition: transform var(--transition-speed);
    }

    .achievement-card:hover {
      transform: translateY(-5px);
    }

    .achievement-icon {
      font-size: 2.5rem;
      color: var(--primary-color);
      margin-bottom: 1rem;
    }

    .achievement-title {
      color: var(--primary-color);
      margin-bottom: 0.5rem;
    }

    .achievement-description {
      font-size: 0.9rem;
      color: #cccccc;
    }

    /* Booking Section */
    .booking-section {
      padding: 4rem 5%;
      background: var(--card-background);
    }

    .booking-options {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 2rem;
      margin-top: 2rem;
    }

    .booking-card {
      background: var(--background-color);
      padding: 1.5rem;
      border-radius: 15px;
      text-align: center;
      transition: transform var(--transition-speed);
    }

    .booking-card:hover {
      transform: translateY(-5px);
    }

    .booking-title {
      color: var(--primary-color);
      margin-bottom: 1rem;
    }

    .booking-price {
      font-size: 2rem;
      color: var(--text-color);
      margin-bottom: 1rem;
    }

    .booking-features {
      list-style: none;
      margin-bottom: 1.5rem;
    }

    .booking-features li {
      margin-bottom: 0.5rem;
      color: #cccccc;
    }

    .booking-features li i {
      color: var(--primary-color);
      margin-right: 0.5rem;
    }

    .book-btn {
      background: var(--primary-color);
      color: var(--background-color);
      border: none;
      padding: 0.75rem 1.5rem;
      border-radius: 20px;
      font-weight: 600;
      cursor: pointer;
      transition: background-color var(--transition-speed);
    }

    .book-btn:hover {
      background: var(--secondary-color);
    }

    /* Calendar Section */
    .calendar-section {
      padding: 4rem 5%;
    }

    .calendar-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1rem;
      margin-top: 2rem;
    }

    .time-slot {
      background: var(--card-background);
      padding: 1rem;
      border-radius: 10px;
      text-align: center;
      cursor: pointer;
      transition: background-color var(--transition-speed);
    }

    .time-slot:hover {
      background: var(--primary-color);
      color: var(--background-color);
    }

    .time-slot.booked {
      background: #333;
      cursor: not-allowed;
      opacity: 0.7;
    }

    /* Auth System */
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

    .hamburger {
      display: none;
      color: var(--text-color);
      font-size: 1.5rem;
      cursor: pointer;
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

    /* Responsive Design */
    @media (max-width: 768px) {
      .coach-profile {
        grid-template-columns: 1fr;
      }

      .profile-image {
        max-width: 400px;
        margin: 0 auto;
      }

      .profile-stats {
        grid-template-columns: 1fr;
      }

      .booking-options {
        grid-template-columns: 1fr;
      }

      .calendar-grid {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    
  </style>
</head>
<body>
  <header>
    <nav class="navbar">
      <a href="index.html" class="logo">
        <span style="display: inline-block; animation: pulse 2s infinite">PowerFit</span>
      </a>
      <ul class="nav-links">
        <li><a href="index.html" class="active">Home</a></li>
        <li class="dropdown">
          <a style="cursor: pointer;">Exercises ▾</a>
          <div class="dropdown-content">
            <a href="gym.html">Gym Workouts</a>
            <a href="calisthenics.html">Calisthenics</a>
          </div>
        </li>
        <li><a href="Coaches.html">For Coaches</a></li>
        <li><a href="Programs.html">Programs</a></li>
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
    <!-- Coach Profile Section -->
    <section class="coach-profile">
      <div class="profile-image">
        <img src="https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Coach Profile">
      </div>
      <div class="profile-info">
        <div class="profile-header">
          <h1 class="profile-name">Alex Johnson</h1>
          <div class="profile-rating">
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star-half-alt"></i>
            <span>(4.5)</span>
          </div>
        </div>
        <div class="profile-tags">
          <span class="profile-tag">Strength Training</span>
          <span class="profile-tag">Weight Loss</span>
          <span class="profile-tag">Muscle Gain</span>
          <span class="profile-tag">Sports Performance</span>
        </div>
        <p class="profile-bio">
          Certified personal trainer with over 8 years of experience helping clients achieve their fitness goals. 
          Specializing in strength training, weight loss, and sports performance. My approach combines science-based 
          training methods with personalized nutrition guidance to deliver sustainable results.
        </p>
        <div class="profile-stats">
          <div class="stat-item">
            <div class="stat-value">250+</div>
            <div class="stat-label">Clients</div>
          </div>
          <div class="stat-item">
            <div class="stat-value">8</div>
            <div class="stat-label">Years Experience</div>
          </div>
          <div class="stat-item">
            <div class="stat-value">12</div>
            <div class="stat-label">Certifications</div>
          </div>
        </div>
      </div>
    </section>

    <!-- Programs Section -->
    <section class="programs-section">
      <h2 class="section-title">Training Programs</h2>
      <div class="filter-buttons">
        <button class="filter-btn active" data-category="all">All Programs</button>
        <button class="filter-btn" data-category="strength">Strength</button>
        <button class="filter-btn" data-category="weight-loss">Weight Loss</button>
        <button class="filter-btn" data-category="muscle-gain">Muscle Gain</button>
        <button class="filter-btn" data-category="sports">Sports</button>
      </div>
      <div class="program-grid">
        <div class="program-card" data-category="strength">
          <img src="https://images.unsplash.com/photo-1583454110551-21f2fa2afe61?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Strength Program">
          <div class="program-info">
            <h3 class="program-title">Power Builder</h3>
            <p class="program-description">Build raw strength and power with this comprehensive program designed for intermediate to advanced lifters.</p>
            <div class="program-meta">
              <span><i class="fas fa-clock"></i> 12 Weeks</span>
              <span><i class="fas fa-dumbbell"></i> Advanced</span>
            </div>
          </div>
        </div>
        <div class="program-card" data-category="weight-loss">
          <img src="https://images.unsplash.com/photo-1517836357463-d25dfeac3438?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Weight Loss Program">
          <div class="program-info">
            <h3 class="program-title">Fat Burner</h3>
            <p class="program-description">Shed unwanted fat while preserving muscle mass with this high-intensity interval training program.</p>
            <div class="program-meta">
              <span><i class="fas fa-clock"></i> 8 Weeks</span>
              <span><i class="fas fa-dumbbell"></i> Intermediate</span>
            </div>
          </div>
        </div>
        <div class="program-card" data-category="muscle-gain">
          <img src="https://images.unsplash.com/photo-1581009146145-b5ef050c2e1e?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Muscle Gain Program">
          <div class="program-info">
            <h3 class="program-title">Mass Builder</h3>
            <p class="program-description">Pack on lean muscle mass with this hypertrophy-focused program designed for all experience levels.</p>
            <div class="program-meta">
              <span><i class="fas fa-clock"></i> 10 Weeks</span>
              <span><i class="fas fa-dumbbell"></i> All Levels</span>
            </div>
          </div>
        </div>
        <div class="program-card" data-category="sports">
          <img src="https://images.unsplash.com/photo-1461896836934-ffe607ba8211?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Sports Performance Program">
          <div class="program-info">
            <h3 class="program-title">Athletic Performance</h3>
            <p class="program-description">Enhance your athletic abilities with this program focused on speed, agility, and explosive power.</p>
            <div class="program-meta">
              <span><i class="fas fa-clock"></i> 6 Weeks</span>
              <span><i class="fas fa-dumbbell"></i> Intermediate</span>
            </div>
          </div>
        </div>
        <div class="program-card" data-category="strength">
          <img src="https://images.unsplash.com/photo-1581009146145-b5ef050c2e1e?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Beginner Strength Program">
          <div class="program-info">
            <h3 class="program-title">Foundation Strength</h3>
            <p class="program-description">Build a solid strength foundation with this beginner-friendly program focusing on proper form and technique.</p>
            <div class="program-meta">
              <span><i class="fas fa-clock"></i> 8 Weeks</span>
              <span><i class="fas fa-dumbbell"></i> Beginner</span>
            </div>
          </div>
        </div>
        <div class="program-card" data-category="weight-loss">
          <img src="https://images.unsplash.com/photo-1517836357463-d25dfeac3438?ixlib=rb-1.2.1&auto=format&fit=crop&w=800&q=80" alt="Advanced Weight Loss Program">
          <div class="program-info">
            <h3 class="program-title">Extreme Transformation</h3>
            <p class="program-description">Accelerate your weight loss journey with this intense program combining strength training and cardio.</p>
            <div class="program-meta">
              <span><i class="fas fa-clock"></i> 12 Weeks</span>
              <span><i class="fas fa-dumbbell"></i> Advanced</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials Section -->
    <section class="testimonials-section">
      <h2 class="section-title">Client Testimonials</h2>
      <div class="testimonial-grid">
        <div class="testimonial-card">
          <div class="testimonial-header">
            <div class="testimonial-avatar">
              <img src="https://randomuser.me/api/portraits/men/32.jpg" alt="Client">
            </div>
            <div class="testimonial-info">
              <h4>Michael T.</h4>
              <p>Lost 30 lbs in 3 months</p>
            </div>
          </div>
          <p class="testimonial-content">
            "Alex's Fat Burner program completely transformed my body. His attention to form and nutrition guidance was invaluable. I've never felt better!"
          </p>
          <div class="testimonial-rating">
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
          </div>
        </div>
        <div class="testimonial-card">
          <div class="testimonial-header">
            <div class="testimonial-avatar">
              <img src="https://randomuser.me/api/portraits/women/44.jpg" alt="Client">
      </div>
            <div class="testimonial-info">
              <h4>Sarah L.</h4>
              <p>Gained 15 lbs of muscle</p>
      </div>
        </div>
          <p class="testimonial-content">
            "The Mass Builder program delivered exactly what I needed. Alex's expertise in nutrition and progressive overload helped me achieve my muscle gain goals."
          </p>
          <div class="testimonial-rating">
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star-half-alt"></i>
          </div>
        </div>
        <div class="testimonial-card">
          <div class="testimonial-header">
            <div class="testimonial-avatar">
              <img src="https://randomuser.me/api/portraits/men/67.jpg" alt="Client">
            </div>
            <div class="testimonial-info">
              <h4>David R.</h4>
              <p>Improved athletic performance</p>
            </div>
          </div>
          <p class="testimonial-content">
            "As a competitive athlete, I needed a program that would enhance my performance. Alex's Athletic Performance program did exactly that. My speed and agility have improved significantly."
          </p>
          <div class="testimonial-rating">
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
            <i class="fas fa-star"></i>
          </div>
        </div>
      </div>
    </section>

    <!-- Achievements Section -->
    <section class="achievements-section">
      <h2 class="section-title">Certifications & Achievements</h2>
      <div class="achievements-grid">
        <div class="achievement-card">
          <div class="achievement-icon">
          <i class="fas fa-medal"></i>
        </div>
          <h3 class="achievement-title">NASM Certified</h3>
          <p class="achievement-description">National Academy of Sports Medicine Certified Personal Trainer</p>
        </div>
        <div class="achievement-card">
          <div class="achievement-icon">
          <i class="fas fa-award"></i>
        </div>
          <h3 class="achievement-title">CrossFit L2</h3>
          <p class="achievement-description">CrossFit Level 2 Trainer with specialization in Olympic lifting</p>
        </div>
        <div class="achievement-card">
          <div class="achievement-icon">
            <i class="fas fa-certificate"></i>
          </div>
          <h3 class="achievement-title">Nutrition Specialist</h3>
          <p class="achievement-description">Precision Nutrition Certified Coach</p>
        </div>
        <div class="achievement-card">
          <div class="achievement-icon">
            <i class="fas fa-trophy"></i>
          </div>
          <h3 class="achievement-title">Best Trainer 2022</h3>
          <p class="achievement-description">Recognized as the top personal trainer in the region</p>
        </div>
      </div>
    </section>

    <!-- Booking Section -->
    <section class="booking-section">
      <h2 class="section-title">Training Packages</h2>
      <div class="booking-options">
        <div class="booking-card">
          <h3 class="booking-title">Starter Package</h3>
          <div class="booking-price">$99<span>/month</span></div>
          <ul class="booking-features">
            <li><i class="fas fa-check"></i> 1 Program Selection</li>
            <li><i class="fas fa-check"></i> Weekly Progress Check-ins</li>
            <li><i class="fas fa-check"></i> Basic Nutrition Guidelines</li>
            <li><i class="fas fa-check"></i> Email Support</li>
          </ul>
          <button class="book-btn">Select Package</button>
        </div>
        <div class="booking-card">
          <h3 class="booking-title">Premium Package</h3>
          <div class="booking-price">$199<span>/month</span></div>
          <ul class="booking-features">
            <li><i class="fas fa-check"></i> 2 Program Selections</li>
            <li><i class="fas fa-check"></i> Bi-weekly Video Calls</li>
            <li><i class="fas fa-check"></i> Customized Meal Plans</li>
            <li><i class="fas fa-check"></i> Priority Support</li>
            <li><i class="fas fa-check"></i> Form Analysis</li>
          </ul>
          <button class="book-btn">Select Package</button>
        </div>
        <div class="booking-card">
          <h3 class="booking-title">Elite Package</h3>
          <div class="booking-price">$299<span>/month</span></div>
          <ul class="booking-features">
            <li><i class="fas fa-check"></i> Unlimited Programs</li>
            <li><i class="fas fa-check"></i> Weekly 1-on-1 Sessions</li>
            <li><i class="fas fa-check"></i> Personalized Nutrition Coaching</li>
            <li><i class="fas fa-check"></i> 24/7 Support</li>
            <li><i class="fas fa-check"></i> Progress Tracking App</li>
            <li><i class="fas fa-check"></i> Supplement Guidance</li>
          </ul>
          <button class="book-btn">Select Package</button>
        </div>
      </div>
    </section>

    <!-- Calendar Section -->
    <section class="calendar-section">
      <h2 class="section-title">Available Time Slots</h2>
      <div class="calendar-grid">
        <div class="time-slot">
          <div>Monday</div>
          <div>9:00 AM - 10:00 AM</div>
      </div>
        <div class="time-slot">
          <div>Monday</div>
          <div>2:00 PM - 3:00 PM</div>
        </div>
        <div class="time-slot booked">
          <div>Tuesday</div>
          <div>10:00 AM - 11:00 AM</div>
        </div>
        <div class="time-slot">
          <div>Tuesday</div>
          <div>4:00 PM - 5:00 PM</div>
        </div>
        <div class="time-slot">
          <div>Wednesday</div>
          <div>11:00 AM - 12:00 PM</div>
        </div>
        <div class="time-slot booked">
          <div>Wednesday</div>
          <div>3:00 PM - 4:00 PM</div>
        </div>
        <div class="time-slot">
          <div>Thursday</div>
          <div>9:00 AM - 10:00 AM</div>
        </div>
        <div class="time-slot">
          <div>Thursday</div>
          <div>2:00 PM - 3:00 PM</div>
        </div>
        <div class="time-slot booked">
          <div>Friday</div>
          <div>10:00 AM - 11:00 AM</div>
        </div>
        <div class="time-slot">
          <div>Friday</div>
          <div>4:00 PM - 5:00 PM</div>
        </div>
      </div>
    </section>
  </main>

  <script>
    // Optimize performance by caching DOM elements
    document.addEventListener('DOMContentLoaded', () => {
      const filterBtns = document.querySelectorAll('.filter-btn');
      const programCards = document.querySelectorAll('.program-card');
      const hamburger = document.querySelector('.hamburger');
      const navLinks = document.querySelector('.nav-links');
      const modal = document.getElementById('authModal');
      const loginBtn = document.getElementById('loginBtn');
      const signupBtn = document.getElementById('signupBtn');
      const closeBtn = document.querySelector('.close');
      const formSwitch = document.querySelectorAll('#formSwitch span');
      const authForm = document.getElementById('authForm');

      // Initialize all programs as visible
      programCards.forEach(card => {
        card.style.display = 'block';
      });

      // Optimized filtering function
      const filterPrograms = (category) => {
        programCards.forEach(card => {
          if (category === 'all') {
            card.style.display = 'block';
          } else {
            const cardCategory = card.getAttribute('data-category');
            card.style.display = cardCategory === category ? 'block' : 'none';
          }
        });
      };

      // Event delegation for filter buttons
      document.querySelector('.filter-buttons').addEventListener('click', (e) => {
        if (e.target.classList.contains('filter-btn')) {
          // Remove active class from all buttons
          filterBtns.forEach(btn => btn.classList.remove('active'));
          // Add active class to clicked button
          e.target.classList.add('active');
          // Get category from data attribute
          const category = e.target.getAttribute('data-category');
          filterPrograms(category);
        }
      });

      // Optimized hamburger menu
      hamburger.addEventListener('click', () => {
        navLinks.classList.toggle('active');
      });

      // Close mobile menu on click outside
      document.addEventListener('click', (e) => {
        if (!hamburger.contains(e.target) && !navLinks.contains(e.target)) {
          navLinks.classList.remove('active');
        }
      });

      // Optimized modal handling
      const showModal = (isLogin) => {
        modal.style.display = 'block';
        formSwitch[isLogin ? 1 : 0].classList.add('switch-active');
        formSwitch[isLogin ? 0 : 1].classList.remove('switch-active');
      };

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

      // Optimized form switch
      formSwitch.forEach(span => {
        span.addEventListener('click', () => {
          formSwitch.forEach(s => s.classList.remove('switch-active'));
          span.classList.add('switch-active');
        });
      });

      // Auth form submission
      authForm.addEventListener('submit', (e) => {
        e.preventDefault();
        const isLogin = document.querySelector('#formSwitch .switch-active').textContent === 'Login';
        handleAuth(isLogin);
        modal.style.display = 'none';
      });

      // Lazy loading for images
      const lazyImages = document.querySelectorAll('img[data-src]');
      const imageObserver = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
          if (entry.isIntersecting) {
            const img = entry.target;
            img.src = img.dataset.src;
            img.removeAttribute('data-src');
            observer.unobserve(img);
          }
        });
      });

      lazyImages.forEach(img => imageObserver.observe(img));
    });

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
  </script>
</body>
</html> # New-Repo
N/A
