# Food_Delivery-AI_agent
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Zwiggy Cloud Kitchen</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700;800;900&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg: #0d0d0d;
      --card: #1a1a1a;
      --card2: #222;
      --accent: #ff6b00;
      --accent2: #ff9a3c;
      --text: #f0f0f0;
      --muted: #888;
      --border: #2a2a2a;
      --green: #22c55e;
    }
    html { scroll-behavior: smooth; }
    body { font-family: 'Poppins', sans-serif; background: var(--bg); color: var(--text); overflow-x: hidden; }

    /* NAV */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 100;
      background: rgba(13,13,13,0.92); backdrop-filter: blur(12px);
      border-bottom: 1px solid var(--border);
      display: flex; align-items: center; justify-content: space-between;
      padding: 0 5vw; height: 64px;
    }
    .logo { font-size: 1.5rem; font-weight: 800; color: var(--accent); letter-spacing: -0.5px; }
    .logo span { color: var(--text); }
    nav ul { list-style: none; display: flex; gap: 2rem; }
    nav ul a { color: var(--muted); text-decoration: none; font-size: 0.9rem; font-weight: 500; transition: color 0.2s; }
    nav ul a:hover { color: var(--accent); }
    .nav-cta {
      background: var(--accent); color: #fff; border: none; padding: 0.5rem 1.4rem;
      border-radius: 50px; font-weight: 600; font-size: 0.9rem; cursor: pointer;
      transition: background 0.2s, transform 0.15s;
    }
    .nav-cta:hover { background: var(--accent2); transform: scale(1.04); }

    /* HERO */
    .hero {
      min-height: 100vh; display: flex; flex-direction: column;
      align-items: center; justify-content: center; text-align: center;
      padding: 80px 5vw 60px;
      background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(255,107,0,0.13) 0%, transparent 70%);
      position: relative; overflow: hidden; z-index: 1;
    }
    .hero::before {
      content: '';
      position: absolute; inset: 0;
      background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ff6b00' fill-opacity='0.04'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
    }
    .badge {
      background: rgba(255,107,0,0.15); border: 1px solid rgba(255,107,0,0.3);
      color: var(--accent2); padding: 0.4rem 1.1rem; border-radius: 50px;
      font-size: 0.8rem; font-weight: 600; letter-spacing: 1px; text-transform: uppercase;
      margin-bottom: 1.5rem; display: inline-block;
    }
    .hero h1 {
      font-size: clamp(2.8rem, 7vw, 5.5rem); font-weight: 900; line-height: 1.05;
      margin-bottom: 1.2rem; letter-spacing: -2px;
    }
    .hero h1 .highlight { color: var(--accent); }
    .hero p {
      font-size: clamp(1rem, 2vw, 1.2rem); color: var(--muted); max-width: 560px;
      line-height: 1.7; margin: 0 auto 2.5rem;
    }
    .hero-btns { display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center; }
    .btn-primary {
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      color: #fff; border: none; padding: 0.85rem 2.2rem; border-radius: 50px;
      font-size: 1rem; font-weight: 700; cursor: pointer;
      box-shadow: 0 4px 24px rgba(255,107,0,0.35); transition: transform 0.2s, box-shadow 0.2s;
    }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 32px rgba(255,107,0,0.5); }
    .btn-secondary {
      background: transparent; color: var(--text); border: 1px solid var(--border);
      padding: 0.85rem 2.2rem; border-radius: 50px; font-size: 1rem;
      font-weight: 600; cursor: pointer; transition: border-color 0.2s, color 0.2s;
    }
    .btn-secondary:hover { border-color: var(--accent); color: var(--accent); }

    /* PROMISE STRIP */
    .promise-strip {
      position: relative; z-index: 1; background: var(--card); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
      padding: 2rem 5vw; display: flex; justify-content: center; gap: 3rem; flex-wrap: wrap;
    }
    .promise-item { display: flex; align-items: center; gap: 0.8rem; }
    .promise-icon { font-size: 2rem; }
    .promise-item h4 { font-size: 1rem; font-weight: 700; color: var(--text); }
    .promise-item p { font-size: 0.78rem; color: var(--muted); }

    /* MENU */
    #menu { padding: 6rem 5vw; position: relative; z-index: 1; }
    .section-label { color: var(--accent); font-size: 0.8rem; font-weight: 700; letter-spacing: 2px; text-transform: uppercase; margin-bottom: 0.5rem; }
    .section-title { font-size: clamp(1.8rem, 4vw, 2.8rem); font-weight: 800; letter-spacing: -0.5px; margin-bottom: 0.5rem; }
    .section-sub { color: var(--muted); font-size: 0.95rem; margin-bottom: 2.5rem; }

    .category-tabs { display: flex; gap: 0.6rem; flex-wrap: wrap; margin-bottom: 2rem; }
    .tab {
      background: var(--card); border: 1px solid var(--border); color: var(--muted);
      padding: 0.5rem 1.2rem; border-radius: 50px; font-size: 0.85rem; font-weight: 600;
      cursor: pointer; transition: all 0.2s;
    }
    .tab.active, .tab:hover { background: var(--accent); border-color: var(--accent); color: #fff; }

    .menu-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 1.2rem; }
    .menu-card {
      background: var(--card); border: 1px solid var(--border); border-radius: 16px;
      padding: 1.2rem; display: flex; flex-direction: column; gap: 0.6rem;
      transition: border-color 0.2s, transform 0.2s; position: relative;
    }
    .menu-card:hover { border-color: var(--accent); transform: translateY(-3px); }
    .menu-card .cat-tag {
      font-size: 0.7rem; font-weight: 600; color: var(--accent2);
      background: rgba(255,107,0,0.1); padding: 0.2rem 0.6rem; border-radius: 50px;
      width: fit-content;
    }
    .menu-card h3 { font-size: 0.95rem; font-weight: 700; }
    .menu-card .price { font-size: 1.1rem; font-weight: 800; color: var(--accent); }
    .add-btn {
      background: var(--accent); color: #fff; border: none; width: 32px; height: 32px;
      border-radius: 50%; font-size: 1.2rem; cursor: pointer; font-weight: 700;
      transition: background 0.2s, transform 0.15s; display: flex; align-items: center; justify-content: center;
    }
    .add-btn:hover { background: var(--accent2); transform: scale(1.1); }
    .menu-card-row { display: flex; align-items: center; justify-content: space-between; }
    .qty-control { display: none; align-items: center; gap: 0.4rem; }
    .qty-control.visible { display: flex; }
    .qty-btn {
      background: var(--card2); border: 1px solid var(--border); color: var(--text);
      width: 28px; height: 28px; border-radius: 50%; font-size: 1rem; font-weight: 700;
      cursor: pointer; display: flex; align-items: center; justify-content: center;
      transition: background 0.2s;
    }
    .qty-btn:hover { background: var(--accent); border-color: var(--accent); }
    .qty-num { font-size: 0.95rem; font-weight: 700; min-width: 18px; text-align: center; }

    /* CART SIDEBAR */
    #cart-overlay {
      position: fixed; inset: 0; background: rgba(0,0,0,0.6); z-index: 200;
      opacity: 0; pointer-events: none; transition: opacity 0.3s;
    }
    #cart-overlay.open { opacity: 1; pointer-events: all; }
    #cart-sidebar {
      position: fixed; top: 0; right: -420px; bottom: 0; width: min(420px, 100vw);
      background: var(--card); border-left: 1px solid var(--border);
      z-index: 201; transition: right 0.35s cubic-bezier(0.4,0,0.2,1);
      display: flex; flex-direction: column;
    }
    #cart-sidebar.open { right: 0; }
    .cart-header {
      padding: 1.2rem 1.5rem; border-bottom: 1px solid var(--border);
      display: flex; align-items: center; justify-content: space-between;
    }
    .cart-header h2 { font-size: 1.1rem; font-weight: 700; }
    .cart-close {
      background: var(--card2); border: 1px solid var(--border); color: var(--text);
      width: 34px; height: 34px; border-radius: 50%; font-size: 1.1rem; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
    }
    .cart-body { flex: 1; overflow-y: auto; padding: 1rem 1.5rem; }
    .cart-empty { color: var(--muted); text-align: center; margin-top: 3rem; font-size: 0.9rem; }
    .cart-item {
      display: flex; align-items: center; justify-content: space-between;
      padding: 0.8rem 0; border-bottom: 1px solid var(--border); gap: 0.5rem;
    }
    .cart-item-name { font-size: 0.88rem; font-weight: 600; flex: 1; }
    .cart-item-price { font-size: 0.88rem; color: var(--accent); font-weight: 700; min-width: 60px; text-align: right; }
    .cart-item-qty { display: flex; align-items: center; gap: 0.3rem; }
    .cart-footer { padding: 1rem 1.5rem; border-top: 1px solid var(--border); }
    .cart-total { display: flex; justify-content: space-between; font-weight: 800; font-size: 1rem; margin-bottom: 1rem; }
    .cart-total span:last-child { color: var(--accent); }
    .place-order-btn {
      width: 100%; background: linear-gradient(135deg, var(--accent), var(--accent2));
      color: #fff; border: none; padding: 0.9rem; border-radius: 12px;
      font-size: 1rem; font-weight: 700; cursor: pointer;
      transition: opacity 0.2s, transform 0.15s;
    }
    .place-order-btn:hover { opacity: 0.9; transform: scale(1.01); }
    .place-order-btn:disabled { opacity: 0.4; cursor: not-allowed; transform: none; }

    /* CART FAB */
    #cart-fab {
      position: fixed; bottom: 2rem; right: 5.5rem; z-index: 150;
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      color: #fff; border: none; padding: 0.8rem 1.5rem; border-radius: 50px;
      font-size: 0.95rem; font-weight: 700; cursor: pointer;
      box-shadow: 0 4px 24px rgba(255,107,0,0.4); display: flex; align-items: center; gap: 0.6rem;
      transition: transform 0.2s, box-shadow 0.2s; display: none;
    }
    #cart-fab.show { display: flex; }
    #cart-fab:hover { transform: scale(1.05); box-shadow: 0 8px 32px rgba(255,107,0,0.5); }
    #cart-count {
      background: #fff; color: var(--accent); width: 22px; height: 22px;
      border-radius: 50%; font-size: 0.75rem; font-weight: 800;
      display: flex; align-items: center; justify-content: center;
    }

    /* ORDER MODAL */
    #order-modal {
      position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 300;
      display: none; align-items: center; justify-content: center; padding: 1rem;
    }
    #order-modal.open { display: flex; }
    .modal-box {
      background: var(--card); border: 1px solid var(--border); border-radius: 20px;
      padding: 2rem; max-width: 420px; width: 100%; text-align: center;
    }
    .modal-box .tick { font-size: 3.5rem; margin-bottom: 1rem; }
    .modal-box h2 { font-size: 1.4rem; font-weight: 800; margin-bottom: 0.5rem; }
    .modal-box p { color: var(--muted); font-size: 0.9rem; line-height: 1.6; }
    .modal-box .timer {
      font-size: 2rem; font-weight: 900; color: var(--accent);
      margin: 1rem 0; font-variant-numeric: tabular-nums;
    }
    .modal-close {
      background: var(--accent); color: #fff; border: none; padding: 0.7rem 2rem;
      border-radius: 50px; font-weight: 700; cursor: pointer; margin-top: 1.5rem;
      font-size: 0.95rem; transition: background 0.2s;
    }
    .modal-close:hover { background: var(--accent2); }

    /* TESTIMONIALS */
    #testimonials { padding: 6rem 5vw; background: var(--card); border-top: 1px solid var(--border); position: relative; z-index: 1; }
    .testimonial-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 1.5rem; margin-top: 2.5rem; }
    .testimonial-card {
      background: var(--bg); border: 1px solid var(--border); border-radius: 16px;
      padding: 1.5rem; transition: border-color 0.2s;
    }
    .testimonial-card:hover { border-color: var(--accent); }
    .stars { color: #fbbf24; font-size: 1rem; margin-bottom: 0.8rem; }
    .testimonial-text { color: #ccc; font-size: 0.9rem; line-height: 1.7; margin-bottom: 1rem; font-style: italic; }
    .reviewer { display: flex; align-items: center; gap: 0.8rem; }
    .avatar {
      width: 40px; height: 40px; border-radius: 50%;
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      display: flex; align-items: center; justify-content: center;
      font-weight: 800; font-size: 1rem; color: #fff;
    }
    .reviewer-info h4 { font-size: 0.88rem; font-weight: 700; }
    .reviewer-info p { font-size: 0.75rem; color: var(--muted); }

    /* FOOTER */
    footer {
      position: relative; z-index: 1; background: #0a0a0a; border-top: 1px solid var(--border);
      padding: 3rem 5vw; display: flex; justify-content: space-between;
      align-items: center; flex-wrap: wrap; gap: 1rem;
    }
    .footer-logo { font-size: 1.3rem; font-weight: 800; color: var(--accent); }
    .footer-logo span { color: var(--text); }
    footer p { color: var(--muted); font-size: 0.82rem; }



    /* FLOATING FOOD ANIMATIONS */
    .food-float-container {
      position: fixed; inset: 0; pointer-events: none; z-index: 0; overflow: hidden;
    }
    .food-emoji {
      position: absolute; font-size: 2rem; opacity: 0;
      animation: floatUp linear infinite;
      filter: drop-shadow(0 2px 8px rgba(255,107,0,0.18));
      user-select: none;
    }
    @keyframes floatUp {
      0%   { opacity: 0; transform: translateY(0) rotate(0deg) scale(0.7); }
      8%   { opacity: 0.55; }
      85%  { opacity: 0.35; }
      100% { opacity: 0; transform: translateY(-100vh) rotate(360deg) scale(1.1); }
    }
    @keyframes floatDrift {
      0%   { opacity: 0; transform: translateY(0) translateX(0) rotate(0deg) scale(0.8); }
      10%  { opacity: 0.5; }
      50%  { transform: translateY(-50vh) translateX(40px) rotate(180deg) scale(1); }
      90%  { opacity: 0.3; }
      100% { opacity: 0; transform: translateY(-100vh) translateX(-20px) rotate(360deg) scale(0.9); }
    }
    .food-emoji.drift { animation-name: floatDrift; }

    /* Hero particle glow orbs */
    .glow-orb {
      position: absolute; border-radius: 50%; pointer-events: none;
      filter: blur(80px); opacity: 0.07; animation: orbPulse ease-in-out infinite;
    }
    @keyframes orbPulse {
      0%, 100% { transform: scale(1); opacity: 0.07; }
      50%       { transform: scale(1.3); opacity: 0.13; }
    }

    /* Sizzle lines behind hero text */
    .sizzle-line {
      position: absolute; height: 2px; border-radius: 2px;
      background: linear-gradient(90deg, transparent, rgba(255,107,0,0.4), transparent);
      animation: sizzle linear infinite; pointer-events: none;
    }
    @keyframes sizzle {
      0%   { transform: translateX(-100%) scaleX(0.5); opacity: 0; }
      20%  { opacity: 1; }
      80%  { opacity: 0.6; }
      100% { transform: translateX(100vw) scaleX(1.2); opacity: 0; }
    }


    /* RESPONSIVE */
    @media (max-width: 600px) {
      nav ul { display: none; }
      .promise-strip { gap: 1.5rem; }
      footer { text-align: center; justify-content: center; }
    }
  </style>

  <!-- n8n AI Chat Assistant -->
  <link href="https://cdn.jsdelivr.net/npm/@n8n/chat/dist/style.css" rel="stylesheet" />
  <style>
    :root {
      --chat--color-primary: #ff5722;
      --chat--color-primary-shade-50: #e64a19;
      --chat--color-primary-shade-100: #d84315;
      --chat--color-secondary: #ff9800;
      --chat--color-secondary-shade-50: #f57c00;
      --chat--color-white: #ffffff;
      --chat--color-light: #fff8f5;
      --chat--color-dark: #1a1a2e;
      --chat--border-radius: 14px;
      --chat--window--width: 380px;
      --chat--window--height: 580px;
      --chat--toggle--size: 60px;
      --chat--toggle--background: #ff5722;
      --chat--toggle--hover--background: #e64a19;
      --chat--toggle--active--background: #d84315;
      --chat--toggle--color: #ffffff;
      --chat--header--background: #1a1a2e;
      --chat--header--color: #ffffff;
      --chat--message--bot--background: #fff8f5;
      --chat--message--bot--color: #1a1a2e;
      --chat--message--user--background: #ff5722;
      --chat--message--user--color: #ffffff;
    }
  </style>
  <script type="module">
    import { createChat } from 'https://cdn.jsdelivr.net/npm/@n8n/chat/dist/chat.bundle.es.js';
    createChat({
      webhookUrl: 'https://shivanshu-ai.app.n8n.cloud/webhook/ec51fb7d-e9b0-4e68-881a-078da3778ad9/chat',
      mode: 'window',
      showWelcomeScreen: false,
      defaultLanguage: 'en',
      initialMessages: [
        'Hey there! 🍔 Welcome to Zwiggy!',
        'Ask me about our menu, ongoing offers, or track your order. How can I help you today?'
      ],
      i18n: {
        en: {
          title: '🍕 Zwiggy AI Assistant',
          subtitle: 'Here to help 24/7 — menu, offers & more!',
          footer: '',
          getStarted: 'Start Chatting 🚀',
          inputPlaceholder: 'Ask about menu, offers, orders...',
        },
      },
    });
  </script>
</head>
<body>

<!-- FLOATING FOOD BACKGROUND -->
<div class="food-float-container" id="foodBg">
  <!-- Glow orbs -->
  <div class="glow-orb" style="width:500px;height:500px;background:#ff6b00;top:-100px;left:-100px;animation-duration:8s;"></div>
  <div class="glow-orb" style="width:400px;height:400px;background:#ff9a3c;bottom:10%;right:-80px;animation-duration:11s;animation-delay:3s;"></div>
  <div class="glow-orb" style="width:300px;height:300px;background:#ff6b00;top:40%;left:30%;animation-duration:14s;animation-delay:6s;"></div>
  <!-- Sizzle lines -->
  <div class="sizzle-line" style="top:18%;width:300px;animation-duration:6s;animation-delay:0s;"></div>
  <div class="sizzle-line" style="top:35%;width:200px;animation-duration:9s;animation-delay:2s;"></div>
  <div class="sizzle-line" style="top:62%;width:400px;animation-duration:7s;animation-delay:4s;"></div>
  <div class="sizzle-line" style="top:80%;width:250px;animation-duration:8s;animation-delay:1s;"></div>
</div>

<!-- NAV -->
<nav>
  <div class="logo">Zwiggy<span> Cloud Kitchen</span></div>
  <ul>
    <li><a href="#menu">Menu</a></li>
    <li><a href="#testimonials">Reviews</a></li>
  </ul>
  <button class="nav-cta" onclick="openCart()">🛒 Order Now</button>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="badge">⚡ Lightning Fast Delivery</div>
  <h1>Freshly Made.<br><span class="highlight">Delivered in 30 Min.</span></h1>
  <p>Hot, delicious food crafted with love — from our cloud kitchen straight to your doorstep. Guaranteed in 30 minutes or your next order is on us.</p>
  <div class="hero-btns">
    <button class="btn-primary" onclick="document.getElementById('menu').scrollIntoView({behavior:'smooth'})">🍔 Explore Menu</button>
    <button class="btn-secondary" onclick="openCart()">View Cart</button>
  </div>
</section>

<!-- PROMISE STRIP -->
<div class="promise-strip">
  <div class="promise-item">
    <div class="promise-icon">⏱️</div>
    <div><h4>30-Min Delivery</h4><p>Guaranteed or next order free</p></div>
  </div>
  <div class="promise-item">
    <div class="promise-icon">🌱</div>
    <div><h4>100% Vegetarian</h4><p>Fresh, wholesome ingredients</p></div>
  </div>
  <div class="promise-item">
    <div class="promise-icon">🏠</div>
    <div><h4>Cloud Kitchen</h4><p>Hygienic, dedicated kitchen</p></div>
  </div>
  <div class="promise-item">
    <div class="promise-icon">💸</div>
    <div><h4>Pocket Friendly</h4><p>Great food, small prices</p></div>
  </div>
</div>

<!-- MENU SECTION -->
<section id="menu">
  <div class="section-label">Our Menu</div>
  <div class="section-title">What's Cooking Today 🔥</div>
  <div class="section-sub">Tap any item to add it to your cart</div>

  <div class="category-tabs">
    <button class="tab active" onclick="filterMenu('all', this)">All</button>
    <button class="tab" onclick="filterMenu('sandwich', this)">🥪 Sandwiches</button>
    <button class="tab" onclick="filterMenu('burger', this)">🍔 Burgers</button>
    <button class="tab" onclick="filterMenu('fries', this)">🍟 Fries</button>
    <button class="tab" onclick="filterMenu('snacks', this)">🍿 Snacks</button>
    <button class="tab" onclick="filterMenu('maggi', this)">🍜 Maggi</button>
    <button class="tab" onclick="filterMenu('drinks', this)">🥤 Drinks</button>
  </div>

  <div class="menu-grid" id="menuGrid"></div>
</section>

<!-- TESTIMONIALS -->
<section id="testimonials">
  <div class="section-label">Customer Love</div>
  <div class="section-title">What Our Foodies Say ❤️</div>
  <div class="section-sub">Real reviews from real customers</div>
  <div class="testimonial-grid">
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <p class="testimonial-text">"Ordered the Paneer Tikka Sandwich at 10 PM and it arrived in exactly 27 minutes — still hot! The flavours were absolutely incredible. My new go-to midnight snack."</p>
      <div class="reviewer"><div class="avatar">P</div><div class="reviewer-info"><h4>Priya Sharma</h4><p>Agra, UP</p></div></div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <p class="testimonial-text">"Cheese Loaded Fries were out of this world! Crispy fries with that gooey cheese — I finished the whole box in 5 minutes. Zwiggy never disappoints. Ordering again tonight!"</p>
      <div class="reviewer"><div class="avatar">R</div><div class="reviewer-info"><h4>Rahul Verma</h4><p>Mathura, UP</p></div></div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <p class="testimonial-text">"The Paneer Momos are something else — soft, juicy, and perfectly spiced. And at ₹110 for 6 pcs, it's a steal! I've tried a lot of cloud kitchens but Zwiggy tops them all."</p>
      <div class="reviewer"><div class="avatar">A</div><div class="reviewer-info"><h4>Anjali Singh</h4><p>Agra, UP</p></div></div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★☆</div>
      <p class="testimonial-text">"Masala Maggi and Cold Coffee combo is my late-night study ritual now. The maggi is spiced just right — not too much, not too little. The 30-min promise is 100% real."</p>
      <div class="reviewer"><div class="avatar">K</div><div class="reviewer-info"><h4>Kartik Joshi</h4><p>Aligarh, UP</p></div></div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <p class="testimonial-text">"Best burger in town, hands down! The Paneer Burger was juicy, well-assembled, and arrived in a neat box. Prices are super affordable. Will definitely recommend to all my friends!"</p>
      <div class="reviewer"><div class="avatar">S</div><div class="reviewer-info"><h4>Sneha Gupta</h4><p>Firozabad, UP</p></div></div>
    </div>
    <div class="testimonial-card">
      <div class="stars">★★★★★</div>
      <p class="testimonial-text">"Chilli Potato was absolutely fire 🔥 The perfect combination of spicy and tangy. Ordered 3 times this week already. The packaging was great and everything arrived fresh and warm!"</p>
      <div class="reviewer"><div class="avatar">V</div><div class="reviewer-info"><h4>Varun Malhotra</h4><p>Agra, UP</p></div></div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div>
    <div class="footer-logo">Zwiggy<span> Cloud Kitchen</span></div>
    <p style="margin-top:0.4rem">Hot food. Fast delivery. Happy you.</p>
  </div>
  <p>© 2026 Zwiggy Cloud Kitchen. All rights reserved.</p>
</footer>

<!-- CART SIDEBAR -->
<div id="cart-overlay" onclick="closeCart()"></div>
<div id="cart-sidebar">
  <div class="cart-header">
    <h2>🛒 Your Order</h2>
    <button class="cart-close" onclick="closeCart()">✕</button>
  </div>
  <div class="cart-body" id="cartBody">
    <p class="cart-empty">Your cart is empty.<br>Add some delicious items! 😋</p>
  </div>
  <div class="cart-footer">
    <div class="cart-total"><span>Total</span><span id="cartTotal">₹0</span></div>
    <button class="place-order-btn" id="placeOrderBtn" onclick="placeOrder()" disabled>Place Order →</button>
  </div>
</div>

<!-- CART FAB -->
<button id="cart-fab" onclick="openCart()">
  🛒 Cart <div id="cart-count">0</div>
</button>

<!-- ORDER MODAL -->
<div id="order-modal">
  <div class="modal-box">
    <div class="tick">🎉</div>
    <h2>Order Placed Successfully!</h2>
    <p>Your food is being prepared with love. Estimated delivery time:</p>
    <div class="timer" id="countdown">30:00</div>
    <p>Sit back and relax. Your delicious meal is on its way! 🛵</p>
    <button class="modal-close" onclick="closeModal()">Awesome, Thanks!</button>
  </div>
</div>

<script>
const menuItems = [
  { id:1, name:"Veg Grilled Sandwich", price:70, cat:"sandwich" },
  { id:2, name:"Cheese Grilled Sandwich", price:90, cat:"sandwich" },
  { id:3, name:"Veg Cheese Corn Sandwich", price:110, cat:"sandwich" },
  { id:4, name:"Paneer Tikka Sandwich", price:130, cat:"sandwich" },
  { id:5, name:"Veg Classic Burger", price:60, cat:"burger" },
  { id:6, name:"Aloo Tikki Burger", price:70, cat:"burger" },
  { id:7, name:"Cheese Burger", price:90, cat:"burger" },
  { id:8, name:"Paneer Burger", price:120, cat:"burger" },
  { id:9, name:"Salted French Fries", price:60, cat:"fries" },
  { id:10, name:"Peri Peri Fries", price:80, cat:"fries" },
  { id:11, name:"Cheese Loaded Fries", price:110, cat:"fries" },
  { id:12, name:"Veg Nuggets (6 pcs)", price:100, cat:"snacks" },
  { id:13, name:"Veg Momos (6 pcs)", price:80, cat:"snacks" },
  { id:14, name:"Paneer Momos (6 pcs)", price:110, cat:"snacks" },
  { id:15, name:"Spring Rolls (4 pcs)", price:90, cat:"snacks" },
  { id:16, name:"Chilli Potato", price:120, cat:"snacks" },
  { id:17, name:"Masala Maggi", price:60, cat:"maggi" },
  { id:18, name:"Butter Maggi", price:80, cat:"maggi" },
  { id:19, name:"Cheese Maggi", price:100, cat:"maggi" },
  { id:20, name:"Corn Chaat", price:70, cat:"snacks" },
  { id:21, name:"Cold Coffee", price:80, cat:"drinks" },
  { id:22, name:"Lemon Soda", price:40, cat:"drinks" },
  { id:23, name:"Masala Chai", price:20, cat:"drinks" }
];

const catLabels = { sandwich:"🥪 Sandwich", burger:"🍔 Burger", fries:"🍟 Fries", snacks:"🍿 Snacks", maggi:"🍜 Maggi", drinks:"🥤 Drinks" };
let cart = {};
let currentFilter = 'all';

function renderMenu(filter) {
  const grid = document.getElementById('menuGrid');
  const filtered = filter === 'all' ? menuItems : menuItems.filter(i => i.cat === filter);
  grid.innerHTML = filtered.map(item => `
    <div class="menu-card" data-id="${item.id}">
      <span class="cat-tag">${catLabels[item.cat]}</span>
      <h3>${item.name}</h3>
      <div class="menu-card-row">
        <span class="price">₹${item.price}</span>
        <button class="add-btn" id="add-${item.id}" onclick="addItem(${item.id})">+</button>
        <div class="qty-control" id="qty-${item.id}">
          <button class="qty-btn" onclick="removeItem(${item.id})">−</button>
          <span class="qty-num" id="qnum-${item.id}">0</span>
          <button class="qty-btn" onclick="addItem(${item.id})">+</button>
        </div>
      </div>
    </div>
  `).join('');
  updateMenuQtys();
}

function filterMenu(cat, btn) {
  currentFilter = cat;
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  btn.classList.add('active');
  renderMenu(cat);
}

function addItem(id) {
  cart[id] = (cart[id] || 0) + 1;
  updateUI(id);
}

function removeItem(id) {
  if (cart[id] > 0) cart[id]--;
  if (cart[id] === 0) delete cart[id];
  updateUI(id);
}

function updateUI(id) {
  const addBtn = document.getElementById('add-' + id);
  const qtyCtrl = document.getElementById('qty-' + id);
  const qnum = document.getElementById('qnum-' + id);
  if (addBtn && qtyCtrl && qnum) {
    const qty = cart[id] || 0;
    if (qty > 0) {
      addBtn.style.display = 'none';
      qtyCtrl.classList.add('visible');
      qnum.textContent = qty;
    } else {
      addBtn.style.display = 'flex';
      qtyCtrl.classList.remove('visible');
    }
  }
  updateCart();
}

function updateMenuQtys() {
  menuItems.forEach(item => {
    const addBtn = document.getElementById('add-' + item.id);
    const qtyCtrl = document.getElementById('qty-' + item.id);
    const qnum = document.getElementById('qnum-' + item.id);
    if (addBtn && qtyCtrl && qnum) {
      const qty = cart[item.id] || 0;
      if (qty > 0) { addBtn.style.display = 'none'; qtyCtrl.classList.add('visible'); qnum.textContent = qty; }
      else { addBtn.style.display = 'flex'; qtyCtrl.classList.remove('visible'); }
    }
  });
}

function updateCart() {
  const body = document.getElementById('cartBody');
  const totalEl = document.getElementById('cartTotal');
  const placeBtn = document.getElementById('placeOrderBtn');
  const fab = document.getElementById('cart-fab');
  const countEl = document.getElementById('cart-count');
  const keys = Object.keys(cart);
  let total = 0, totalQty = 0;
  if (keys.length === 0) {
    body.innerHTML = '<p class="cart-empty">Your cart is empty.<br>Add some delicious items! 😋</p>';
    totalEl.textContent = '₹0';
    placeBtn.disabled = true;
    fab.classList.remove('show');
    return;
  }
  body.innerHTML = keys.map(id => {
    const item = menuItems.find(i => i.id == id);
    const sub = item.price * cart[id];
    total += sub; totalQty += cart[id];
    return `<div class="cart-item">
      <span class="cart-item-name">${item.name}</span>
      <div class="cart-item-qty">
        <button class="qty-btn" onclick="removeItem(${id})">−</button>
        <span class="qty-num">${cart[id]}</span>
        <button class="qty-btn" onclick="addItem(${id})">+</button>
      </div>
      <span class="cart-item-price">₹${sub}</span>
    </div>`;
  }).join('');
  totalEl.textContent = '₹' + total;
  placeBtn.disabled = false;
  fab.classList.add('show');
  countEl.textContent = totalQty;
}

function openCart() {
  document.getElementById('cart-overlay').classList.add('open');
  document.getElementById('cart-sidebar').classList.add('open');
}
function closeCart() {
  document.getElementById('cart-overlay').classList.remove('open');
  document.getElementById('cart-sidebar').classList.remove('open');
}

let countdownInterval;
function placeOrder() {
  closeCart();
  document.getElementById('order-modal').classList.add('open');
  cart = {};
  updateCart();
  renderMenu(currentFilter);
  let secs = 30 * 60;
  document.getElementById('countdown').textContent = '30:00';
  clearInterval(countdownInterval);
  countdownInterval = setInterval(() => {
    secs--;
    const m = String(Math.floor(secs / 60)).padStart(2, '0');
    const s = String(secs % 60).padStart(2, '0');
    document.getElementById('countdown').textContent = m + ':' + s;
    if (secs <= 0) clearInterval(countdownInterval);
  }, 1000);
}
function closeModal() {
  document.getElementById('order-modal').classList.remove('open');
  clearInterval(countdownInterval);
}

renderMenu('all');
</script>


<script>
// Floating food emojis
(function() {
  const emojis = ['🍔','🍟','🥪','🧆','🍕','🌮','🥙','🍜','☕','🧃','🌯','🥗','🫔','🧇','🥞','🍱','🥘','🫕','🍛','🥐','🧀','🌽','🫑','🥑','🍅','🧄','🫚','🥣'];
  const container = document.getElementById('foodBg');
  const count = 28;
  for (let i = 0; i < count; i++) {
    const el = document.createElement('div');
    el.className = 'food-emoji' + (Math.random() > 0.5 ? ' drift' : '');
    el.textContent = emojis[Math.floor(Math.random() * emojis.length)];
    const size = 1.4 + Math.random() * 1.8;
    el.style.fontSize = size + 'rem';
    el.style.left = (Math.random() * 100) + 'vw';
    el.style.bottom = '-80px';
    const dur = 12 + Math.random() * 18;
    const delay = -(Math.random() * dur);
    el.style.animationDuration = dur + 's';
    el.style.animationDelay = delay + 's';
    el.style.opacity = '0';
    container.appendChild(el);
  }
})();
</script>


</body>
</html>
