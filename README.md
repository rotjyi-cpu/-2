<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Тёмная тема · ИгровойУголок 2</title>
    <!-- Babylon.js -->
    <script src="https://cdn.babylonjs.com/babylon.js"></script>
    <script src="https://cdn.babylonjs.com/loaders/babylonjs.loaders.min.js"></script>
    <script src="https://cdn.babylonjs.com/gui/babylon.gui.min.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <style>
        /* ===== БАЗОВЫЕ СТИЛИ (МАКСИМАЛЬНО ТЁМНАЯ ТЕМА) ===== */
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: 'Inter', sans-serif;
            background: #000000;
            color: #e0e0f0;
            line-height: 1.6;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            transition: background-color 0.3s, color 0.3s;
        }
        body.light-theme {
            background: #f5f5fa;
            color: #1e1e2f;
        }
        /* Фоновый текст Rotjyi & R_52_X */
        body::before {
            content: "Rotjyi & R_52_X";
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) rotate(-30deg);
            font-size: clamp(2rem, 8vw, 8rem);
            color: rgba(255, 255, 255, 0.15);
            white-space: nowrap;
            pointer-events: none;
            z-index: -1;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 0.1em;
            user-select: none;
        }
        body.light-theme::before {
            color: rgba(0, 0, 0, 0.15);
        }
        .container { max-width: 1200px; margin: 0 auto; padding: 0 24px; }
        .header {
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(110, 90, 255, 0.2);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 1);
            position: sticky;
            top: 0;
            z-index: 10;
            padding: 16px 0;
            transition: background 0.3s, border-color 0.3s;
        }
        body.light-theme .header {
            background: rgba(240, 240, 255, 0.85);
            border-bottom: 1px solid rgba(70, 50, 200, 0.3);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
        }
        .header .container { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; }
        .logo {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(145deg, #b5b0ff, #8a7eff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            letter-spacing: -0.3px;
        }
        body.light-theme .logo {
            background: linear-gradient(145deg, #4a3f99, #2d2570);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .logo-wrapper { display: flex; align-items: center; gap: 12px; }
        .user-nick {
            font-size: 20px;
            font-weight: 500;
            color: #bdb6ff;
            background: rgba(70, 60, 150, 0.2);
            padding: 6px 14px;
            border-radius: 40px;
            border: 1px solid #4a3f99;
            box-shadow: 0 0 12px #5b4dcc;
            backdrop-filter: blur(4px);
            cursor: pointer;
            transition: all 0.2s;
        }
        .user-nick:hover {
            background: rgba(100, 80, 200, 0.5);
            box-shadow: 0 0 20px #8a7eff;
            transform: scale(1.05);
        }
        body.light-theme .user-nick {
            color: #2d2570;
            background: rgba(200, 190, 255, 0.5);
            border: 1px solid #4a3f99;
            box-shadow: 0 0 8px #bdb6ff;
        }
        .theme-toggle {
            background: transparent;
            border: 2px solid #5d4edb;
            color: #cec6ff;
            font-size: 24px;
            width: 48px;
            height: 48px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
            margin-left: 15px;
        }
        body.light-theme .theme-toggle {
            border-color: #2d2570;
            color: #2d2570;
        }
        .theme-toggle:hover {
            background: #5d4edb;
            color: black;
            box-shadow: 0 0 25px #6b5cff;
        }
        .nav ul { display: flex; list-style: none; gap: 40px; align-items: center; }
        .nav a {
            text-decoration: none;
            font-weight: 500;
            color: #c0c0e0;
            font-size: 18px;
            transition: color 0.2s, text-shadow 0.2s;
            cursor: pointer;
        }
        body.light-theme .nav a { color: #2d2570; }
        .nav a:hover { color: #a394ff; text-shadow: 0 0 8px #6c5eff; }
        body.light-theme .nav a:hover { color: #5d4edb; text-shadow: 0 0 8px #bdb6ff; }
        .main { flex: 1; padding: 40px 0 60px; }
        .hero { text-align: center; padding: 50px 20px 30px; }
        .hero h1 {
            font-size: 56px;
            font-weight: 700;
            background: linear-gradient(145deg, #ffffff, #b5aaff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 16px;
            line-height: 1.2;
            text-shadow: 0 0 15px rgba(130, 100, 255, 0.5);
        }
        body.light-theme .hero h1 {
            background: linear-gradient(145deg, #1e1e2f, #4a3f99);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            text-shadow: 0 0 15px rgba(70, 50, 200, 0.3);
        }
        .hero p {
            font-size: 20px;
            color: #a0a0c0;
            max-width: 650px;
            margin: 0 auto 30px;
        }
        body.light-theme .hero p { color: #4a4a6a; }
        .glow-button {
            display: inline-block;
            background: #0a0a0a;
            color: #ddd5ff;
            font-weight: 600;
            padding: 14px 40px;
            border-radius: 60px;
            text-decoration: none;
            font-size: 18px;
            border: 1px solid #4f47b0;
            box-shadow: 0 0 20px #4f3bff40, 0 8px 15px #000000;
            transition: all 0.25s;
        }
        body.light-theme .glow-button {
            background: #e0daff;
            color: #1e1e2f;
            border: 1px solid #4a3f99;
            box-shadow: 0 0 20px #bdb6ff, 0 8px 15px #c0c0e0;
        }
        .glow-button:hover {
            background: #2d2570;
            border-color: #9a8cff;
            box-shadow: 0 0 30px #6b5cff, 0 10px 20px black;
            transform: scale(1.03);
            color: white;
        }
        .games-section { margin: 80px 0 40px; }
        .section-title {
            font-size: 42px;
            font-weight: 600;
            text-align: center;
            margin-bottom: 20px;
            background: linear-gradient(145deg, #f0eaff, #bbaaff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        body.light-theme .section-title {
            background: linear-gradient(145deg, #2d2570, #1e1e2f);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .section-desc {
            text-align: center;
            color: #9a9ac0;
            font-size: 18px;
            margin-bottom: 50px;
        }
        body.light-theme .section-desc { color: #5a5a80; }
        .games-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 30px; }
        .game-card {
            background: #0a0a0a;
            border-radius: 34px;
            padding: 30px 20px 25px;
            text-align: center;
            border: 1px solid #2d274f;
            box-shadow: 0 25px 40px -15px #000000, 0 0 0 1px #2b2255 inset;
            transition: transform 0.2s, box-shadow 0.3s;
            backdrop-filter: blur(2px);
            display: flex;
            flex-direction: column;
        }
        body.light-theme .game-card {
            background: #f0f0ff;
            border: 1px solid #bdb6ff;
            box-shadow: 0 25px 40px -15px #c0c0e0, 0 0 0 1px #d0caff inset;
        }
        .game-card:hover {
            transform: translateY(-8px);
            border-color: #6d5cf0;
            box-shadow: 0 30px 55px -10px #000000, 0 0 25px #4d3ee0;
        }
        body.light-theme .game-card:hover {
            border-color: #4a3f99;
            box-shadow: 0 30px 55px -10px #b0aaff, 0 0 25px #bdb6ff;
        }
        .game-emoji { font-size: 64px; margin-bottom: 15px; filter: drop-shadow(0 0 10px #7d6aff); }
        .game-card h3 {
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 10px;
            color: #dad5ff;
        }
        body.light-theme .game-card h3 { color: #1e1e2f; }
        .game-card p {
            color: #9f9bc5;
            margin-bottom: 25px;
            font-size: 16px;
            padding: 0 10px;
            flex-grow: 1;
        }
        body.light-theme .game-card p { color: #5a5a80; }
        .play-btn {
            background: transparent;
            border: 2px solid #5d4edb;
            color: #cec6ff;
            padding: 10px 30px;
            border-radius: 40px;
            font-weight: 600;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.2s;
            display: inline-block;
            text-decoration: none;
            margin-top: auto;
        }
        body.light-theme .play-btn {
            border: 2px solid #4a3f99;
            color: #2d2570;
        }
        .play-btn:hover {
            background: #5d4edb;
            color: black;
            box-shadow: 0 0 25px #6b5cff;
            border-color: #bdb0ff;
        }
        .game-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(8px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        body.light-theme .game-modal {
            background: rgba(255, 255, 255, 0.9);
        }
        .game-modal.active { display: flex; }
        .modal-content {
            background: #0a0a0a;
            border-radius: 48px;
            padding: 30px;
            max-width: 900px;
            width: 95%;
            max-height: 85vh;
            overflow-y: auto;
            border: 2px solid #5d4edb;
            box-shadow: 0 0 50px #4d3ee0;
            position: relative;
            color: #e0e0f0;
        }
        body.light-theme .modal-content {
            background: #ffffff;
            border: 2px solid #4a3f99;
            box-shadow: 0 0 50px #bdb6ff;
            color: #1e1e2f;
        }
        .close-modal {
            position: absolute;
            top: 20px;
            right: 25px;
            font-size: 36px;
            cursor: pointer;
            color: #9a8cff;
            transition: color 0.2s;
        }
        body.light-theme .close-modal { color: #4a3f99; }
        .close-modal:hover { color: #ff6b6b; }
        .game-area {
            margin-top: 20px;
            min-height: 350px;
            background: #050505;
            border-radius: 30px;
            padding: 25px;
            border: 1px solid #3f3a6b;
        }
        body.light-theme .game-area {
            background: #f5f5ff;
            border: 1px solid #bdb6ff;
        }
        .game-btn {
            background: #5d4edb;
            color: white;
            border: none;
            padding: 10px 25px;
            border-radius: 30px;
            font-size: 16px;
            cursor: pointer;
            margin: 5px;
            transition: 0.2s;
        }
        body.light-theme .game-btn {
            background: #4a3f99;
            color: white;
        }
        .game-btn:hover {
            background: #7a6dff;
            box-shadow: 0 0 15px #6b5cff;
        }
        /* Стили для 3D-канвасов */
        .babylon-container { width: 100%; height: 400px; border-radius: 20px; overflow: hidden; border: 2px solid #5d4edb; margin-top: 15px; }
        body.light-theme .babylon-container { border: 2px solid #4a3f99; }
        /* Стили для 2D-игр */
        .dino-canvas, .balloon-canvas, .tanks-canvas, .tetris-canvas {
            width: 100%;
            height: 400px;
            display: block;
            background: #1a1a2a;
            border-radius: 20px;
            cursor: pointer;
            touch-action: none;
        }
        body.light-theme .dino-canvas, body.light-theme .balloon-canvas, body.light-theme .tanks-canvas, body.light-theme .tetris-canvas {
            background: #e0e0f0;
        }
        .game-stats {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            font-size: 20px;
            color: #ffd966;
            flex-wrap: wrap;
            gap: 10px;
        }
        /* Стили для новостей и чата */
        .news-list { list-style: none; margin: 0; padding: 0; }
        .news-item { margin-bottom: 20px; padding-bottom: 15px; border-bottom: 1px solid #3a3355; }
        body.light-theme .news-item { border-bottom: 1px solid #bdb6ff; }
        .news-title { font-size: 18px; font-weight: 600; color: #ffd966; text-decoration: none; }
        body.light-theme .news-title { color: #b85c3a; }
        .news-title:hover { text-decoration: underline; }
        .news-description { color: #b0b0d0; margin-top: 5px; font-size: 14px; }
        body.light-theme .news-description { color: #5a5a80; }
        .news-date { color: #7f76b0; font-size: 12px; }
        body.light-theme .news-date { color: #4a3f99; }
        .chat-container { display: flex; flex-direction: column; height: 400px; }
        .chat-messages { flex-grow: 1; overflow-y: auto; padding: 10px; background: #050505; border-radius: 20px; margin-bottom: 10px; }
        body.light-theme .chat-messages { background: #f5f5ff; }
        .chat-message { margin-bottom: 10px; }
        .chat-message.user { text-align: right; }
        .chat-message.bot { text-align: left; }
        .chat-message span { display: inline-block; padding: 8px 12px; border-radius: 18px; max-width: 80%; }
        .user span { background: #2a5f8a; }
        .bot span { background: #4a3f99; }
        body.light-theme .user span { background: #b0d0ff; color: #1e1e2f; }
        body.light-theme .bot span { background: #e0daff; color: #1e1e2f; }
        .chat-input-area { display: flex; gap: 10px; }
        .chat-input { flex-grow: 1; padding: 10px; background: #0a0a0a; border: 2px solid #5d4edb; color: white; border-radius: 30px; outline: none; }
        body.light-theme .chat-input { background: #ffffff; border: 2px solid #4a3f99; color: #1e1e2f; }
        .footer {
            background: #000000;
            border-top: 1px solid #26203b;
            padding: 30px 0;
            margin-top: 40px;
            transition: background 0.3s, border-color 0.3s;
        }
        body.light-theme .footer {
            background: #e0e0f0;
            border-top: 1px solid #bdb6ff;
        }
        .footer .container { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 16px; }
        .footer p { color: #6a6a90; }
        body.light-theme .footer p { color: #4a4a6a; }
        .footer-links { display: flex; gap: 28px; }
        .footer-links a { color: #7f76b0; text-decoration: none; font-weight: 500; cursor: pointer; }
        body.light-theme .footer-links a { color: #4a3f99; }
        .footer-links a:hover { color: #b3a6ff; }
        @media (max-width: 600px) { .hero h1 { font-size: 42px; } .nav ul { gap: 24px; } .section-title { font-size: 34px; } }
        html { scroll-behavior: smooth; }
        
        /* Стили для тайного раздела */
        .secret-achievement {
            text-align: center;
            font-size: 28px;
            margin-bottom: 20px;
            color: #ffd966;
        }
        body.light-theme .secret-achievement {
            color: #b85c3a;
        }
        .secret-description {
            font-size: 18px;
            line-height: 1.6;
            text-align: center;
        }
        .secret-highlight {
            color: #ffd966;
            font-weight: bold;
        }
        body.light-theme .secret-highlight {
            color: #b85c3a;
        }
        
        /* Эксклюзивная метка */
        .exclusive-badge {
            display: inline-block;
            background: linear-gradient(145deg, #ffd966, #ffaa00);
            color: #000000;
            font-size: 14px;
            font-weight: bold;
            padding: 4px 12px;
            border-radius: 20px;
            margin-left: 10px;
            text-transform: uppercase;
            letter-spacing: 1px;
            vertical-align: middle;
            box-shadow: 0 0 15px #ffaa00;
        }
        body.light-theme .exclusive-badge {
            background: linear-gradient(145deg, #b85c3a, #8a3f2a);
            color: white;
            box-shadow: 0 0 15px #b85c3a;
        }
        
        /* Стили для R-TRAINS */
        .rtrains-panel {
            background: #0a0a0a;
            border: 1px solid #5d4edb;
            border-radius: 20px;
            padding: 15px;
            margin: 10px 0;
        }
        .rtrains-station {
            background: #050505;
            border: 1px solid #3f3a6b;
            border-radius: 15px;
            padding: 15px;
            margin: 10px 0;
        }
        .rtrains-station-name {
            color: #ffd966;
            font-weight: bold;
            font-size: 18px;
            margin-bottom: 10px;
        }
        .rtrains-resource {
            color: #9f9bc5;
            font-size: 14px;
            display: flex;
            align-items: center;
            gap: 10px;
            flex-wrap: wrap;
            margin: 5px 0;
        }
        .rtrains-quantity-selector {
            display: flex;
            align-items: center;
            gap: 5px;
            background: #1a1a2a;
            border-radius: 20px;
            padding: 5px 10px;
        }
        .rtrains-quantity-selector input {
            width: 70px;
            background: #0a0a0a;
            border: 1px solid #5d4edb;
            color: white;
            padding: 5px;
            border-radius: 10px;
            text-align: center;
        }
        .rtrains-quantity-selector button {
            background: #5d4edb;
            color: white;
            border: none;
            width: 30px;
            height: 30px;
            border-radius: 15px;
            cursor: pointer;
            font-weight: bold;
        }
        .rtrains-quantity-selector button:hover {
            background: #7a6dff;
        }
        .rtrains-total-price {
            color: #ffd966;
            font-size: 16px;
            margin-left: 10px;
        }
        
        /* Стили для достижений */
        .achievements-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 15px;
            padding: 10px;
        }
        .achievement-card {
            background: #0a0a0a;
            border: 2px solid #5d4edb;
            border-radius: 20px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            transition: transform 0.2s;
        }
        .achievement-card.completed {
            border-color: #ffd966;
            background: #1a1a2a;
        }
        .achievement-icon {
            font-size: 40px;
            min-width: 60px;
            text-align: center;
        }
        .achievement-info {
            flex: 1;
        }
        .achievement-title {
            font-size: 18px;
            font-weight: bold;
            color: #ffd966;
            margin-bottom: 5px;
        }
        .achievement-desc {
            font-size: 14px;
            color: #9f9bc5;
            margin-bottom: 5px;
        }
        .achievement-status {
            font-size: 14px;
            color: #5d4edb;
        }
        .achievement-card.completed .achievement-status {
            color: #ffd966;
        }
        
        /* Уведомление о достижении */
        .achievement-toast {
            position: fixed;
            top: 20px;
            right: 20px;
            background: #0a0a0a;
            border: 2px solid #ffd966;
            border-radius: 20px;
            padding: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            z-index: 2000;
            animation: slideIn 0.5s, fadeOut 0.5s 4.5s forwards;
            max-width: 350px;
            box-shadow: 0 0 30px #ffd966;
        }
        @keyframes slideIn {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; display: none; }
        }
        .toast-icon {
            font-size: 40px;
        }
        .toast-content {
            flex: 1;
        }
        .toast-title {
            font-size: 16px;
            color: #ffd966;
            margin-bottom: 5px;
        }
        .toast-name {
            font-size: 18px;
            font-weight: bold;
            color: white;
        }
        
        /* Мобильное управление для танчиков */
        .tank-controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
            flex-wrap: wrap;
        }
        .tank-controls button {
            width: 60px;
            height: 60px;
            border-radius: 30px;
            background: #5d4edb;
            color: white;
            border: none;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 0 15px #6b5cff;
        }
        .tank-controls button:active {
            background: #7a6dff;
        }
        @media (min-width: 769px) {
            .tank-controls {
                display: none;
            }
        }

        /* Стили для модального окна пароля */
        .password-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(8px);
            z-index: 2000;
            justify-content: center;
            align-items: center;
        }
        .password-modal.active {
            display: flex;
        }
        .password-content {
            background: #0a0a0a;
            border: 2px solid #5d4edb;
            border-radius: 30px;
            padding: 30px;
            text-align: center;
            max-width: 400px;
            width: 90%;
        }
        .password-input {
            width: 100%;
            padding: 15px;
            margin: 20px 0;
            background: #050505;
            border: 2px solid #5d4edb;
            color: white;
            border-radius: 30px;
            font-size: 18px;
            text-align: center;
        }
    </style>
</head>
<body>
    <header class="header">
        <div class="container">
            <div class="logo-wrapper">
                <span class="logo">🎮 ИгровойУголок 2</span>
                <span class="user-nick" onclick="openPasswordModal()">R_52_X BETA</span>
            </div>
            <nav class="nav">
                <ul>
                    <li><a href="#home">Главная</a></li>
                    <li><a href="#games">Игры</a></li>
                    <li><a onclick="openNews()">Новости</a></li>
                    <li><a onclick="openAI()">ИИ</a></li>
                    <li><a onclick="openAchievements()">🏆 Достижения</a></li>
                    <li><button id="themeToggle" class="theme-toggle" onclick="toggleTheme()">🌙</button></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- МОДАЛЬНОЕ ОКНО ДЛЯ ПАРОЛЯ -->
    <div id="passwordModal" class="password-modal">
        <div class="password-content">
            <h2 style="color:#ffd966; margin-bottom:20px;">🔐 Введите пароль</h2>
            <input type="password" id="passwordInput" class="password-input" placeholder="Пароль" maxlength="8">
            <div style="display:flex; gap:10px; justify-content:center;">
                <button class="game-btn" onclick="checkPassword()">Подтвердить</button>
                <button class="game-btn" onclick="closePasswordModal()">Отмена</button>
            </div>
        </div>
    </div>

    <main class="main">
        <div class="container">
            <section id="home" class="hero">
                <h1>Добро пожаловать в ночь</h1>
                <p>Максимально тёмная тема, эксклюзивные игры, свежие новости, улучшенный ИИ-помощник и система достижений от R_52_X BETA.</p>
                <a href="#games" class="glow-button">К играм</a>
            </section>

            <section id="games" class="games-section">
                <h2 class="section-title">🎮 Наши игры</h2>
                <p class="section-desc">Эксклюзивные и классические</p>
                <div class="games-grid">
                    <!-- Игра 1: Добеги до электробуса (ЭКСКЛЮЗИВ) -->
                    <div class="game-card">
                        <div class="game-emoji">🚌⚡</div>
                        <h3>Добеги до электробуса <span class="exclusive-badge">ЭКСКЛЮЗИВ</span></h3>
                        <p>Своя игра от R_52_X. Два режима: автобус (движение по стрелкам вверх/вниз) и бег (стрелки влево/вправо). Собирайте людей и получайте достижения!</p>
                        <button class="play-btn" onclick="openGame3D('bus')">Играть</button>
                    </div>
                    <!-- Игра 2: R-TRAINS (ЭКСКЛЮЗИВ) -->
                    <div class="game-card">
                        <div class="game-emoji">🚂🛤️</div>
                        <h3>R-TRAINS <span class="exclusive-badge">ЭКСКЛЮЗИВ</span></h3>
                        <p>Стратегия про поезда. 10 станций, покупайте до 1000 единиц товара за раз, торгуйте ресурсами и зарабатывайте миллионы!</p>
                        <button class="play-btn" onclick="openGame2D('rtrains')">Играть</button>
                    </div>
                    <!-- Игра 3: Охота на птиц (ЭКСКЛЮЗИВ) -->
                    <div class="game-card">
                        <div class="game-emoji">🔫🐦</div>
                        <h3>Охота на птиц <span class="exclusive-badge">ЭКСКЛЮЗИВ</span></h3>
                        <p>3D-шутер на Babylon.js. Стреляйте по птицам, зарабатывайте очки и улучшайте ружьё. Птицы спавнятся бесконечно (до 10 одновременно)!</p>
                        <button class="play-btn" onclick="openGame3D('birds')">Играть</button>
                    </div>
                    <!-- Игра 4: Minecraft (ЭКСКЛЮЗИВ) -->
                    <div class="game-card">
                        <div class="game-emoji">⛏️🌳</div>
                        <h3>Minecraft <span class="exclusive-badge">ЭКСКЛЮЗИВ</span></h3>
                        <p>Полноценная 3D-игра на Babylon.js. Ломайте и ставьте блоки, исследуйте мир. WASD — движение, пробел — прыжок, Shift — присесть, мышь — осмотр, ЛКМ — сломать блок, ПКМ — поставить камень.</p>
                        <button class="play-btn" onclick="openGame3D('minecraft')">Играть</button>
                    </div>
                    <!-- Игра 5: Динозаврик (обычная) -->
                    <div class="game-card">
                        <div class="game-emoji">🦖</div>
                        <h3>Динозаврик</h3>
                        <p>Бесконечный раннер с текстурами. Прыгайте через кактусы (пробел или клик). Чем дольше бежите, тем выше счёт.</p>
                        <button class="play-btn" onclick="openGame2D('dino')">Играть</button>
                    </div>
                    <!-- Игра 6: Воздушный шарик (обычная) -->
                    <div class="game-card">
                        <div class="game-emoji">🎈</div>
                        <h3>Воздушный шарик</h3>
                        <p>Летите вверх, уворачиваясь от облаков (стрелки влево/вправо). С каждым облаком +10 очков. Улучшенные текстуры и повышенная скорость!</p>
                        <button class="play-btn" onclick="openGame2D('balloon')">Играть</button>
                    </div>
                    <!-- Игра 7: Танчики 1985 -->
                    <div class="game-card">
                        <div class="game-emoji">🚜💥</div>
                        <h3>Танчики 1985</h3>
                        <p>Классическая аркада. Сражайтесь с ботами, 4 уровня сложности, бесконечные враги, 3 жизни. На ПК: стрелки + пробел. На телефоне: кнопки на экране.</p>
                        <button class="play-btn" onclick="openGame2D('tanks')">Играть</button>
                    </div>
                    <!-- Игра 8: Тетрис -->
                    <div class="game-card">
                        <div class="game-emoji">🔷</div>
                        <h3>Тетрис</h3>
                        <p>Классический Тетрис. Стрелки — движение, вверх — поворот, вниз — ускорение. Собирайте линии и ставьте рекорды!</p>
                        <button class="play-btn" onclick="openGame2D('tetris')">Играть</button>
                    </div>
                    <!-- Игра 9: Гонки 3D (исправлено) -->
                    <div class="game-card">
                        <div class="game-emoji">🏎️</div>
                        <h3>Гонки 3D</h3>
                        <p>3D-гонки с круговой трассой. ↑ — газ, ↓ — тормоз, ← → — поворот, пробел — ускорение (нитро). Считает круги и дистанцию!</p>
                        <button class="play-btn" onclick="openGame3D('racing')">Играть</button>
                    </div>
                </div>
            </section>
        </div>
    </main>

    <footer class="footer">
        <div class="container">
            <p>© 2026 ИгровойУголок 2 — эксклюзивные и классические игры, новости, ИИ и достижения</p>
            <div class="footer-links">
                <a onclick="openNews()">Новости</a>
                <a onclick="openAI()">ИИ</a>
                <a onclick="openAchievements()">🏆 Достижения</a>
            </div>
        </div>
    </footer>

    <!-- МОДАЛЬНОЕ ОКНО ДЛЯ 3D ИГР -->
    <div id="gameModal3D" class="game-modal">
        <div class="modal-content" style="max-width: 900px;">
            <span class="close-modal" onclick="closeGame3D()">&times;</span>
            <h2 id="gameTitle3D">3D Игра</h2>
            <div id="gameContent3D" class="game-area" style="background: transparent; padding: 0;">
                <div id="babylonContainer" class="babylon-container"></div>
                <div id="game3dControls" style="margin-top:15px; text-align:center;"></div>
            </div>
        </div>
    </div>

    <!-- МОДАЛЬНОЕ ОКНО ДЛЯ 2D ИГР -->
    <div id="gameModal2D" class="game-modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeGame2D()">&times;</span>
            <h2 id="gameTitle2D">2D Игра</h2>
            <div id="gameContent2D" class="game-area" style="overflow-y: auto;"></div>
        </div>
    </div>

    <!-- МОДАЛЬНОЕ ОКНО ДЛЯ НОВОСТЕЙ -->
    <div id="newsModal" class="game-modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeNews()">&times;</span>
            <h2>📰 Новости России</h2>
            <div id="newsContent" class="game-area" style="overflow-y: auto;">
                <p>Загрузка новостей...</p>
            </div>
        </div>
    </div>

    <!-- МОДАЛЬНОЕ ОКНО ДЛЯ ИИ (УЛУЧШЕННЫЙ БОТ) -->
    <div id="aiModal" class="game-modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeAI()">&times;</span>
            <h2>🤖 ИИ от R_52_X BETA (улучшенный)</h2>
            <div id="aiContent" class="game-area">
                <div class="chat-container">
                    <div id="chatMessages" class="chat-messages">
                        <div class="chat-message bot"><span>Привет! Я улучшенный ИИ-помощник. Спроси меня о чём угодно!</span></div>
                    </div>
                    <div class="chat-input-area">
                        <input type="text" id="chatInput" class="chat-input" placeholder="Введите сообщение...">
                        <button class="game-btn" onclick="sendMessage()">Отправить</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- МОДАЛЬНОЕ ОКНО ДЛЯ ДОСТИЖЕНИЙ -->
    <div id="achievementsModal" class="game-modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeAchievements()">&times;</span>
            <h2>🏆 Достижения</h2>
            <div id="achievementsContent" class="game-area" style="overflow-y: auto;"></div>
        </div>
    </div>

    <!-- ТАЙНЫЙ РАЗДЕЛ (достижение) -->
    <div id="secretModal" class="game-modal">
        <div class="modal-content">
            <span class="close-modal" onclick="closeSecret()">&times;</span>
            <h2>🔐 Тайный раздел</h2>
            <div id="secretContent" class="game-area" style="text-align: center;">
                <div class="secret-achievement">🏆 ПОЗДРАВЛЯЮ! 🏆</div>
                <div class="secret-achievement">Ты открыл тайный раздел!</div>
                <div class="secret-description">
                    <p><span class="secret-highlight">R_52_X</span> — это компания, создающая сайты с играми.</p>
                    <p><span class="secret-highlight">BETA</span> — значит, что функции ещё тестируются.</p>
                    <p style="margin-top: 20px;">Спасибо, что ты с нами! ❤️</p>
                </div>
            </div>
        </div>
    </div>

    <!-- КОНТЕЙНЕР ДЛЯ УВЕДОМЛЕНИЙ О ДОСТИЖЕНИЯХ -->
    <div id="achievementToastContainer" style="position: fixed; top: 20px; right: 20px; z-index: 2000;"></div>

    <script>
        // ================== СИСТЕМА ДОСТИЖЕНИЙ ==================
        const achievements = [
            { id: 'playAllGames', name: 'Игроман', desc: 'Поиграть во все игры', icon: '🎮', condition: 'allGames', progress: 0, maxProgress: 9 },
            { id: 'rtrainsMoney', name: 'Магнат', desc: 'Получить 10000 монет в R-TRAINS', icon: '💰', condition: 'rtrainsMoney', progress: 0, maxProgress: 10000 },
            { id: 'secretSection', name: 'Тайна', desc: 'Найти тайный раздел', icon: '🔐', condition: 'secret', completed: false },
            { id: 'news', name: 'Новостник', desc: 'Зайти в новости', icon: '📰', condition: 'news', completed: false },
            { id: 'ai', name: 'Друг', desc: 'Зайти в бота', icon: '🤖', condition: 'ai', completed: false },
            { id: 'birdGun', name: 'Охотник', desc: 'Прокачать оружие до 10 уровня в Охота на птиц', icon: '🔫', condition: 'birdGun', progress: 0, maxProgress: 10 },
            { id: 'busPeople', name: 'Спринтер', desc: 'Пройти 100 людей в Добеги до электробуса', icon: '🚌', condition: 'busPeople', progress: 0, maxProgress: 100 },
            { id: 'minecraftWalk', name: 'Первооткрыватель', desc: 'Зайти в Minecraft и пройтись', icon: '⛏️', condition: 'minecraft', completed: false },
            { id: 'tanksPlay', name: 'Танкист', desc: 'Зайти в Танчики', icon: '🚜', condition: 'tanksPlay', completed: false },
            { id: 'tanksScore', name: 'Легенда танков', desc: 'Получить 10000 очков в Танчиках', icon: '💥', condition: 'tanksScore', progress: 0, maxProgress: 10000 },
            { id: 'racingWin', name: 'Победитель гонок', desc: 'Первый раз проехать 1000 метров в гонке', icon: '🏆', condition: 'racingWin', progress: 0, maxProgress: 1000 },
            { id: 'tetrisLine', name: 'Тетрис-мастер', desc: 'Первый раз собрать полную линию в тетрисе', icon: '🔷', condition: 'tetrisLine', completed: false }
        ];

        let achievementData = loadAchievements();

        function loadAchievements() {
            const saved = localStorage.getItem('achievements');
            if (saved) {
                return JSON.parse(saved);
            } else {
                const initial = {};
                achievements.forEach(a => {
                    if (a.progress !== undefined) {
                        initial[a.id] = { completed: false, progress: 0 };
                    } else {
                        initial[a.id] = { completed: false };
                    }
                });
                return initial;
            }
        }

        function saveAchievements() {
            localStorage.setItem('achievements', JSON.stringify(achievementData));
        }

        function showAchievementToast(achievement) {
            const container = document.getElementById('achievementToastContainer');
            const toast = document.createElement('div');
            toast.className = 'achievement-toast';
            toast.innerHTML = `
                <div class="toast-icon">${achievement.icon}</div>
                <div class="toast-content">
                    <div class="toast-title">🏆 Достижение получено!</div>
                    <div class="toast-name">${achievement.name}</div>
                </div>
            `;
            container.appendChild(toast);
            setTimeout(() => {
                toast.remove();
            }, 5000);
        }

        function updateAchievement(id, completed, progress = null) {
            if (achievementData[id].completed) return;
            
            if (progress !== null) {
                achievementData[id].progress = progress;
                const achievement = achievements.find(a => a.id === id);
                if (progress >= achievement.maxProgress) {
                    achievementData[id].completed = true;
                    showAchievementToast(achievement);
                }
            } else if (completed) {
                achievementData[id].completed = true;
                const achievement = achievements.find(a => a.id === id);
                showAchievementToast(achievement);
            }
            saveAchievements();
            renderAchievements();
        }

        function checkAllGamesProgress() {
            const games = ['bus', 'rtrains', 'birds', 'minecraft', 'dino', 'balloon', 'tanks', 'tetris', 'racing'];
            const playedGames = JSON.parse(localStorage.getItem('playedGames') || '[]');
            const progress = playedGames.length;
            updateAchievement('playAllGames', false, progress);
        }

        function registerGamePlayed(gameId) {
            let played = JSON.parse(localStorage.getItem('playedGames') || '[]');
            if (!played.includes(gameId)) {
                played.push(gameId);
                localStorage.setItem('playedGames', JSON.stringify(played));
                checkAllGamesProgress();
            }
        }

        // ================== ПАРОЛЬ НА ТАЙНЫЙ РАЗДЕЛ ==================
        const passwordModal = document.getElementById('passwordModal');
        const secretModal = document.getElementById('secretModal');
        const passwordInput = document.getElementById('passwordInput');
        const SECRET_PASSWORD = "52525267";

        function openPasswordModal() {
            passwordModal.classList.add('active');
            passwordInput.value = '';
        }

        function closePasswordModal() {
            passwordModal.classList.remove('active');
        }

        function checkPassword() {
            if (passwordInput.value === SECRET_PASSWORD) {
                closePasswordModal();
                secretModal.classList.add('active');
                updateAchievement('secretSection', true);
            } else {
                alert('Неверный пароль!');
            }
        }

        function closeSecret() {
            secretModal.classList.remove('active');
        }

        // ================== ПЕРЕКЛЮЧЕНИЕ ТЕМЫ ==================
        function toggleTheme() {
            document.body.classList.toggle('light-theme');
            const btn = document.getElementById('themeToggle');
            btn.textContent = document.body.classList.contains('light-theme') ? '☀️' : '🌙';
        }

        // ================== ДОСТИЖЕНИЯ ==================
        const achievementsModal = document.getElementById('achievementsModal');
        const achievementsContent = document.getElementById('achievementsContent');

        function openAchievements() {
            achievementsModal.classList.add('active');
            renderAchievements();
        }

        function closeAchievements() {
            achievementsModal.classList.remove('active');
        }

        function renderAchievements() {
            let html = '<div class="achievements-container">';
            achievements.forEach(achievement => {
                const data = achievementData[achievement.id];
                const completed = data && data.completed;
                const progress = data && data.progress !== undefined ? data.progress : (completed ? achievement.maxProgress || 1 : 0);
                const maxProgress = achievement.maxProgress || 1;
                const percent = Math.floor((progress / maxProgress) * 100);
                
                html += `
                    <div class="achievement-card ${completed ? 'completed' : ''}">
                        <div class="achievement-icon">${achievement.icon}</div>
                        <div class="achievement-info">
                            <div class="achievement-title">${achievement.name}</div>
                            <div class="achievement-desc">${achievement.desc}</div>
                            ${achievement.progress !== undefined ? 
                                `<div class="achievement-status">Прогресс: ${progress}/${maxProgress} (${percent}%)</div>` : 
                                `<div class="achievement-status">${completed ? '✅ Выполнено' : '❌ Не выполнено'}</div>`
                            }
                        </div>
                    </div>
                `;
            });
            html += '</div>';
            achievementsContent.innerHTML = html;
        }

        // ================== 2D ИГРЫ ==================
        const modal2D = document.getElementById('gameModal2D');
        const title2D = document.getElementById('gameTitle2D');
        const content2D = document.getElementById('gameContent2D');
        let currentGame2D = null;
        let gameInterval = null;
        let gameAnimationFrame = null;

        function openGame2D(game) {
            modal2D.classList.add('active');
            currentGame2D = game;
            registerGamePlayed(game);
            
            if (game === 'rtrains') {
                title2D.textContent = '🚂 R-TRAINS (ЭКСКЛЮЗИВ)';
                content2D.innerHTML = rtrainsHTML;
                initRTrains();
            } else if (game === 'dino') {
                title2D.textContent = '🦖 Динозаврик';
                content2D.innerHTML = dinoHTML;
                initDino();
            } else if (game === 'balloon') {
                title2D.textContent = '🎈 Воздушный шарик';
                content2D.innerHTML = balloonHTML;
                initBalloon();
            } else if (game === 'tanks') {
                title2D.textContent = '🚜 Танчики 1985';
                content2D.innerHTML = tanksHTML;
                initTanks();
                updateAchievement('tanksPlay', true);
            } else if (game === 'tetris') {
                title2D.textContent = '🔷 Тетрис';
                content2D.innerHTML = tetrisHTML;
                initTetris();
            } else {
                closeGame2D();
            }
        }

        function closeGame2D() {
            modal2D.classList.remove('active');
            if (gameInterval) {
                clearInterval(gameInterval);
                gameInterval = null;
            }
            if (gameAnimationFrame) {
                cancelAnimationFrame(gameAnimationFrame);
                gameAnimationFrame = null;
            }
            currentGame2D = null;
        }

        // ================== ТЕТРИС ==================
        const tetrisHTML = `
            <div>
                <div class="game-stats">
                    <span>Очки: <span id="tetris-score">0</span></span>
                    <span>Линии: <span id="tetris-lines">0</span></span>
                </div>
                <canvas id="tetrisCanvas" class="tetris-canvas" width="400" height="400"></canvas>
                <p style="text-align:center; color:#ffd966; margin-top:10px;">Стрелки: движение, вверх — поворот, вниз — ускорение</p>
            </div>
        `;

        let tetrisCanvas, tetrisCtx;
        let tetrisBoard, tetrisPiece, tetrisScore, tetrisLines;
        let tetrisGameOver = false;
        let tetrisInterval = null;
        let tetrisSpeed = 500;

        const tetrisPieces = [
            { shape: [[1,1,1,1]], color: '#00FFFF' },
            { shape: [[1,1],[1,1]], color: '#FFFF00' },
            { shape: [[0,1,0],[1,1,1]], color: '#FF00FF' },
            { shape: [[0,1,1],[1,1,0]], color: '#00FF00' },
            { shape: [[1,1,0],[0,1,1]], color: '#FF0000' },
            { shape: [[1,0,0],[1,1,1]], color: '#FFA500' },
            { shape: [[0,0,1],[1,1,1]], color: '#0000FF' }
        ];

        function initTetris() {
            tetrisCanvas = document.getElementById('tetrisCanvas');
            tetrisCtx = tetrisCanvas.getContext('2d');
            
            tetrisBoard = Array(20).fill().map(() => Array(10).fill(0));
            tetrisScore = 0;
            tetrisLines = 0;
            tetrisGameOver = false;
            
            document.getElementById('tetris-score').textContent = tetrisScore;
            document.getElementById('tetris-lines').textContent = tetrisLines;
            
            spawnTetrisPiece();
            
            if (tetrisInterval) clearInterval(tetrisInterval);
            tetrisInterval = setInterval(() => {
                if (!tetrisGameOver) {
                    moveTetrisPieceDown();
                }
            }, tetrisSpeed);
            
            window.addEventListener('keydown', tetrisKeyDown);
            
            drawTetris();
        }

        function spawnTetrisPiece() {
            const randomIndex = Math.floor(Math.random() * tetrisPieces.length);
            tetrisPiece = {
                shape: tetrisPieces[randomIndex].shape.map(row => [...row]),
                color: tetrisPieces[randomIndex].color,
                x: Math.floor((10 - tetrisPieces[randomIndex].shape[0].length) / 2),
                y: 0
            };
            
            if (collision()) {
                tetrisGameOver = true;
                alert('Игра окончена!');
            }
        }

        function collision() {
            for (let y = 0; y < tetrisPiece.shape.length; y++) {
                for (let x = 0; x < tetrisPiece.shape[y].length; x++) {
                    if (tetrisPiece.shape[y][x]) {
                        const boardX = tetrisPiece.x + x;
                        const boardY = tetrisPiece.y + y;
                        if (boardX < 0 || boardX >= 10 || boardY >= 20 || (boardY >= 0 && tetrisBoard[boardY][boardX])) {
                            return true;
                        }
                    }
                }
            }
            return false;
        }

        function mergePiece() {
            for (let y = 0; y < tetrisPiece.shape.length; y++) {
                for (let x = 0; x < tetrisPiece.shape[y].length; x++) {
                    if (tetrisPiece.shape[y][x]) {
                        const boardY = tetrisPiece.y + y;
                        const boardX = tetrisPiece.x + x;
                        if (boardY >= 0 && boardY < 20) {
                            tetrisBoard[boardY][boardX] = tetrisPiece.color;
                        }
                    }
                }
            }
        }

        function clearLines() {
            let linesCleared = 0;
            for (let y = 19; y >= 0; y--) {
                if (tetrisBoard[y].every(cell => cell !== 0)) {
                    linesCleared++;
                    for (let y2 = y; y2 > 0; y2--) {
                        tetrisBoard[y2] = [...tetrisBoard[y2-1]];
                    }
                    tetrisBoard[0] = Array(10).fill(0);
                    y++;
                }
            }
            
            if (linesCleared > 0) {
                tetrisLines += linesCleared;
                tetrisScore += linesCleared * 100;
                document.getElementById('tetris-score').textContent = tetrisScore;
                document.getElementById('tetris-lines').textContent = tetrisLines;
                updateAchievement('tetrisLine', true);
            }
        }

        function moveTetrisPieceDown() {
            tetrisPiece.y++;
            if (collision()) {
                tetrisPiece.y--;
                mergePiece();
                clearLines();
                spawnTetrisPiece();
            }
            drawTetris();
        }

        function tetrisKeyDown(e) {
            if (tetrisGameOver) return;
            
            switch(e.key) {
                case 'ArrowLeft':
                    tetrisPiece.x--;
                    if (collision()) tetrisPiece.x++;
                    break;
                case 'ArrowRight':
                    tetrisPiece.x++;
                    if (collision()) tetrisPiece.x--;
                    break;
                case 'ArrowDown':
                    moveTetrisPieceDown();
                    break;
                case 'ArrowUp':
                    const rotated = tetrisPiece.shape[0].map((val, index) => 
                        tetrisPiece.shape.map(row => row[index]).reverse()
                    );
                    const originalShape = tetrisPiece.shape;
                    tetrisPiece.shape = rotated;
                    if (collision()) {
                        tetrisPiece.shape = originalShape;
                    }
                    break;
            }
            drawTetris();
        }

        function drawTetris() {
            tetrisCtx.clearRect(0, 0, 400, 400);
            
            tetrisCtx.strokeStyle = '#333';
            tetrisCtx.lineWidth = 1;
            for (let i = 0; i <= 20; i++) {
                tetrisCtx.beginPath();
                tetrisCtx.moveTo(0, i * 20);
                tetrisCtx.lineTo(400, i * 20);
                tetrisCtx.stroke();
            }
            for (let i = 0; i <= 10; i++) {
                tetrisCtx.beginPath();
                tetrisCtx.moveTo(i * 40, 0);
                tetrisCtx.lineTo(i * 40, 400);
                tetrisCtx.stroke();
            }
            
            for (let y = 0; y < 20; y++) {
                for (let x = 0; x < 10; x++) {
                    if (tetrisBoard[y][x]) {
                        tetrisCtx.fillStyle = tetrisBoard[y][x];
                        tetrisCtx.fillRect(x * 40, y * 20, 40, 20);
                        tetrisCtx.strokeStyle = '#fff';
                        tetrisCtx.strokeRect(x * 40, y * 20, 40, 20);
                    }
                }
            }
            
            for (let y = 0; y < tetrisPiece.shape.length; y++) {
                for (let x = 0; x < tetrisPiece.shape[y].length; x++) {
                    if (tetrisPiece.shape[y][x]) {
                        const boardX = (tetrisPiece.x + x) * 40;
                        const boardY = (tetrisPiece.y + y) * 20;
                        tetrisCtx.fillStyle = tetrisPiece.color;
                        tetrisCtx.fillRect(boardX, boardY, 40, 20);
                        tetrisCtx.strokeStyle = '#fff';
                        tetrisCtx.strokeRect(boardX, boardY, 40, 20);
                    }
                }
            }
        }

        // ================== ДИНОЗАВРИК ==================
        const dinoHTML = `
            <div>
                <div class="game-stats">
                    <span>Счёт: <span id="dino-score">0</span></span>
                    <span>Рекорд: <span id="dino-record">0</span></span>
                </div>
                <canvas id="dinoCanvas" class="dino-canvas" width="800" height="400"></canvas>
                <p style="text-align:center; color:#ffd966; margin-top:10px;">Пробел или клик — прыжок</p>
            </div>
        `;

        function initDino() {
            const canvas = document.getElementById('dinoCanvas');
            const ctx = canvas.getContext('2d');
            
            let dino = {
                x: 50,
                y: 300,
                width: 30,
                height: 30,
                vy: 0,
                gravity: 0.5,
                jumpPower: -10,
                grounded: true
            };
            
            let obstacles = [];
            let score = 0;
            let record = localStorage.getItem('dinoRecord') || 0;
            let gameOver = false;
            let frameCount = 0;
            
            document.getElementById('dino-score').textContent = score;
            document.getElementById('dino-record').textContent = record;
            
            function jump() {
                if (!gameOver && dino.grounded) {
                    dino.vy = dino.jumpPower;
                    dino.grounded = false;
                }
            }
            
            canvas.addEventListener('click', jump);
            window.addEventListener('keydown', (e) => {
                if (e.code === 'Space') {
                    e.preventDefault();
                    jump();
                }
            });
            
            function update() {
                if (gameOver) return;
                
                dino.vy += dino.gravity;
                dino.y += dino.vy;
                
                if (dino.y >= 300) {
                    dino.y = 300;
                    dino.vy = 0;
                    dino.grounded = true;
                }
                
                if (frameCount % 60 === 0 && obstacles.length < 3) {
                    obstacles.push({
                        x: 800,
                        y: 310,
                        width: 20,
                        height: 30,
                        speed: 8
                    });
                }
                
                obstacles.forEach(obs => {
                    obs.x -= obs.speed;
                });
                
                obstacles = obstacles.filter(obs => {
                    if (obs.x + obs.width < 0) {
                        score += 10;
                        document.getElementById('dino-score').textContent = score;
                        return false;
                    }
                    return true;
                });
                
                obstacles.forEach(obs => {
                    if (dino.x < obs.x + obs.width &&
                        dino.x + dino.width > obs.x &&
                        dino.y < obs.y + obs.height &&
                        dino.y + dino.height > obs.y) {
                        gameOver = true;
                        if (score > record) {
                            record = score;
                            localStorage.setItem('dinoRecord', record);
                            document.getElementById('dino-record').textContent = record;
                        }
                        alert(`Игра окончена! Ваш счёт: ${score}`);
                    }
                });
                
                frameCount++;
            }
            
            function draw() {
                ctx.clearRect(0, 0, 800, 400);
                
                const gradient = ctx.createLinearGradient(0, 0, 0, 400);
                gradient.addColorStop(0, '#87CEEB');
                gradient.addColorStop(1, '#B0E0E6');
                ctx.fillStyle = gradient;
                ctx.fillRect(0, 0, 800, 400);
                
                ctx.fillStyle = '#8B4513';
                ctx.fillRect(0, 350, 800, 50);
                ctx.fillStyle = '#A0522D';
                for (let i = 0; i < 800; i += 10) {
                    ctx.fillRect(i, 355, 5, 10);
                }
                
                ctx.fillStyle = '#228B22';
                ctx.fillRect(dino.x, dino.y, dino.width, dino.height);
                ctx.fillStyle = '#006400';
                ctx.fillRect(dino.x + 5, dino.y + 5, 5, 5);
                ctx.fillStyle = '#000000';
                ctx.fillRect(dino.x + 7, dino.y + 7, 3, 3);
                
                ctx.fillStyle = '#2E8B57';
                ctx.fillRect(dino.x + 20, dino.y + 5, 3, 5);
                ctx.fillRect(dino.x + 20, dino.y + 15, 3, 5);
                
                obstacles.forEach(obs => {
                    ctx.fillStyle = '#228B22';
                    ctx.fillRect(obs.x, obs.y, obs.width, obs.height);
                    ctx.fillStyle = '#2E8B57';
                    ctx.fillRect(obs.x + 3, obs.y - 5, 5, 5);
                    ctx.fillRect(obs.x + 10, obs.y - 8, 5, 8);
                });
                
                ctx.fillStyle = '#000';
                ctx.font = '20px Inter';
                ctx.fillText(`Счёт: ${score}`, 10, 30);
                ctx.fillStyle = '#fff';
                ctx.font = '16px Inter';
                ctx.fillText(`Рекорд: ${record}`, 10, 60);
            }
            
            function gameLoop() {
                update();
                draw();
                gameAnimationFrame = requestAnimationFrame(gameLoop);
            }
            
            gameLoop();
        }

        // ================== ВОЗДУШНЫЙ ШАРИК ==================
        const balloonHTML = `
            <div>
                <div class="game-stats">
                    <span>Счёт: <span id="balloon-score">0</span></span>
                    <span>Рекорд: <span id="balloon-record">0</span></span>
                </div>
                <canvas id="balloonCanvas" class="balloon-canvas" width="800" height="400"></canvas>
                <p style="text-align:center; color:#ffd966; margin-top:10px;">Стрелки влево/вправо — управление</p>
            </div>
        `;

        function initBalloon() {
            const canvas = document.getElementById('balloonCanvas');
            const ctx = canvas.getContext('2d');
            
            let balloon = {
                x: 400,
                y: 350,
                radius: 15,
                speed: 12
            };
            
            let obstacles = [];
            let score = 0;
            let record = localStorage.getItem('balloonRecord') || 0;
            let gameOver = false;
            let frameCount = 0;
            
            document.getElementById('balloon-score').textContent = score;
            document.getElementById('balloon-record').textContent = record;
            
            let leftPressed = false;
            let rightPressed = false;
            
            window.addEventListener('keydown', (e) => {
                if (e.key === 'ArrowLeft') leftPressed = true;
                if (e.key === 'ArrowRight') rightPressed = true;
            });
            
            window.addEventListener('keyup', (e) => {
                if (e.key === 'ArrowLeft') leftPressed = false;
                if (e.key === 'ArrowRight') rightPressed = false;
            });
            
            function update() {
                if (gameOver) return;
                
                if (leftPressed) balloon.x -= balloon.speed;
                if (rightPressed) balloon.x += balloon.speed;
                
                if (balloon.x < balloon.radius) balloon.x = balloon.radius;
                if (balloon.x > 800 - balloon.radius) balloon.x = 800 - balloon.radius;
                
                if (frameCount % 30 === 0) {
                    obstacles.push({
                        x: Math.random() * 700 + 50,
                        y: 0,
                        width: 60,
                        height: 30,
                        speed: 6
                    });
                }
                
                obstacles.forEach(obs => {
                    obs.y += obs.speed;
                });
                
                obstacles = obstacles.filter(obs => {
                    if (obs.y > 400) {
                        score += 10;
                        document.getElementById('balloon-score').textContent = score;
                        return false;
                    }
                    return true;
                });
                
                obstacles.forEach(obs => {
                    const dx = balloon.x - Math.max(obs.x, Math.min(balloon.x, obs.x + obs.width));
                    const dy = balloon.y - Math.max(obs.y, Math.min(balloon.y, obs.y + obs.height));
                    if (dx * dx + dy * dy < balloon.radius * balloon.radius) {
                        gameOver = true;
                        if (score > record) {
                            record = score;
                            localStorage.setItem('balloonRecord', record);
                            document.getElementById('balloon-record').textContent = record;
                        }
                        alert(`Игра окончена! Ваш счёт: ${score}`);
                    }
                });
                
                frameCount++;
            }
            
            function draw() {
                ctx.clearRect(0, 0, 800, 400);
                
                const skyGradient = ctx.createLinearGradient(0, 0, 0, 400);
                skyGradient.addColorStop(0, '#87CEEB');
                skyGradient.addColorStop(1, '#B0E0E6');
                ctx.fillStyle = skyGradient;
                ctx.fillRect(0, 0, 800, 400);
                
                obstacles.forEach(obs => {
                    ctx.fillStyle = '#FFFFFF';
                    ctx.beginPath();
                    ctx.arc(obs.x + 15, obs.y + 15, 15, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.beginPath();
                    ctx.arc(obs.x + 35, obs.y + 10, 12, 0, Math.PI * 2);
                    ctx.fill();
                    ctx.beginPath();
                    ctx.arc(obs.x + 45, obs.y + 20, 10, 0, Math.PI * 2);
                    ctx.fill();
                    
                    ctx.fillStyle = '#F0F0F0';
                    ctx.beginPath();
                    ctx.arc(obs.x + 20, obs.y + 18, 8, 0, Math.PI * 2);
                    ctx.fill();
                });
                
                const balloonGradient = ctx.createRadialGradient(
                    balloon.x - 5, balloon.y - 5, 5,
                    balloon.x, balloon.y, balloon.radius + 5
                );
                balloonGradient.addColorStop(0, '#FF69B4');
                balloonGradient.addColorStop(1, '#FF1493');
                
                ctx.beginPath();
                ctx.arc(balloon.x, balloon.y, balloon.radius, 0, Math.PI * 2);
                ctx.fillStyle = balloonGradient;
                ctx.fill();
                
                ctx.beginPath();
                ctx.arc(balloon.x - 5, balloon.y - 5, 5, 0, Math.PI * 2);
                ctx.fillStyle = 'rgba(255, 255, 255, 0.3)';
                ctx.fill();
                
                ctx.beginPath();
                ctx.moveTo(balloon.x - 2, balloon.y + balloon.radius - 2);
                ctx.lineTo(balloon.x - 2, balloon.y + balloon.radius + 10);
                ctx.strokeStyle = '#8B4513';
                ctx.lineWidth = 2;
                ctx.stroke();
                
                ctx.fillStyle = '#8B4513';
                ctx.fillRect(balloon.x - 8, balloon.y + balloon.radius + 10, 12, 8);
                
                ctx.fillStyle = '#000';
                ctx.font = '20px Inter';
                ctx.fillText(`Счёт: ${score}`, 10, 30);
                ctx.fillStyle = '#fff';
                ctx.font = '16px Inter';
                ctx.fillText(`Рекорд: ${record}`, 10, 60);
            }
            
            function gameLoop() {
                update();
                draw();
                gameAnimationFrame = requestAnimationFrame(gameLoop);
            }
            
            gameLoop();
        }

        // ================== R-TRAINS ==================
        const rtrainsHTML = `
            <div style="color:#e0e0f0;">
                <div class="rtrains-panel">
                    <div style="display:flex; justify-content:space-between; margin-bottom:10px; flex-wrap:wrap; gap:10px;">
                        <span>💰 Кредиты: <span id="rtrains-money" style="color:#ffd966;">1000</span></span>
                        <span>🚂 Поезда: <span id="rtrains-trains">3</span></span>
                        <span>🏭 Станций: <span id="rtrains-stations">10</span></span>
                    </div>
                    <div style="display:flex; gap:10px; justify-content:center; flex-wrap:wrap;">
                        <button class="game-btn" onclick="rtrainsBuyTrain()">Купить поезд (500 + 100×кол-во)</button>
                        <button class="game-btn" onclick="rtrainsNextTurn()">Следующий ход</button>
                    </div>
                </div>
                
                <div id="rtrains-stations-container" class="rtrains-panel">
                    <!-- Станции будут сгенерированы динамически -->
                </div>
                
                <div class="rtrains-panel">
                    <h4 style="color:#ffd966; margin-bottom:10px;">Ваш инвентарь</h4>
                    <div id="rtrains-inventory" style="display:flex; gap:20px; justify-content:center; flex-wrap:wrap;">
                        <span>🪨 Уголь: <span id="rtrains-inv-coal">0</span></span>
                        <span>⚙️ Сталь: <span id="rtrains-inv-steel">0</span></span>
                        <span>🌾 Зерно: <span id="rtrains-inv-grain">0</span></span>
                    </div>
                </div>
                
                <div id="rtrains-message" class="rtrains-panel" style="color:#9f9bc5; text-align:center;">
                    Добро пожаловать в R-TRAINS! Покупайте ресурсы дёшево, продавайте дорого.
                </div>
            </div>
        `;

        let rtrainsMoney = 1000;
        let rtrainsTrains = 3;
        let rtrainsStations = [];
        let rtrainsInventory = { coal: 0, steel: 0, grain: 0 };
        let rtrainsQuantities = {};
        const stationNames = ['Северная', 'Южная', 'Восточная', 'Западная', 'Центральная', 'Лесная', 'Горная', 'Речная', 'Озёрная', 'Полевая'];

        function initRTrains() {
            rtrainsMoney = 1000;
            rtrainsTrains = 3;
            rtrainsInventory = { coal: 0, steel: 0, grain: 0 };
            rtrainsQuantities = {};
            generateStations();
            updateRTrainsUI();
        }

        function generateStations() {
            rtrainsStations = [];
            for (let i = 0; i < 10; i++) {
                rtrainsStations.push({
                    name: stationNames[Math.floor(Math.random() * stationNames.length)] + ' ' + (i+1),
                    prices: {
                        coal: Math.floor(Math.random() * 30) + 10,
                        steel: Math.floor(Math.random() * 50) + 30,
                        grain: Math.floor(Math.random() * 20) + 5
                    }
                });
            }
        }

        function getQuantity(stationIndex, resource) {
            const key = stationIndex + '-' + resource;
            return rtrainsQuantities[key] || 1;
        }

        function setQuantity(stationIndex, resource, value) {
            const key = stationIndex + '-' + resource;
            rtrainsQuantities[key] = Math.min(1000, Math.max(1, parseInt(value) || 1));
            updateRTrainsUI();
        }

        function updateRTrainsUI() {
            document.getElementById('rtrains-money').textContent = rtrainsMoney;
            document.getElementById('rtrains-trains').textContent = rtrainsTrains;
            document.getElementById('rtrains-stations').textContent = rtrainsStations.length;
            
            document.getElementById('rtrains-inv-coal').textContent = rtrainsInventory.coal;
            document.getElementById('rtrains-inv-steel').textContent = rtrainsInventory.steel;
            document.getElementById('rtrains-inv-grain').textContent = rtrainsInventory.grain;

            const container = document.getElementById('rtrains-stations-container');
            let html = '<h4 style="color:#ffd966; margin-bottom:10px;">Станции (цены за единицу)</h4>';
            
            rtrainsStations.forEach((station, index) => {
                const coalQty = getQuantity(index, 'coal');
                const steelQty = getQuantity(index, 'steel');
                const grainQty = getQuantity(index, 'grain');
                
                html += `
                    <div class="rtrains-station">
                        <div class="rtrains-station-name">${station.name}</div>
                        
                        <div class="rtrains-resource">
                            <span>🪨 Уголь: ${station.prices.coal} кредитов</span>
                            <div class="rtrains-quantity-selector">
                                <button onclick="adjustQuantity(${index}, 'coal', -1)">-</button>
                                <input type="number" id="qty-${index}-coal" value="${coalQty}" min="1" max="1000" onchange="setQuantity(${index}, 'coal', this.value)">
                                <button onclick="adjustQuantity(${index}, 'coal', 1)">+</button>
                                <span class="rtrains-total-price">= ${coalQty * station.prices.coal} кр.</span>
                            </div>
                            <button class="game-btn" style="padding:5px 15px;" onclick="rtrainsBuy(${index}, 'coal')">Купить</button>
                            <button class="game-btn" style="padding:5px 15px;" onclick="rtrainsSell(${index}, 'coal')">Продать</button>
                        </div>
                        
                        <div class="rtrains-resource">
                            <span>⚙️ Сталь: ${station.prices.steel} кредитов</span>
                            <div class="rtrains-quantity-selector">
                                <button onclick="adjustQuantity(${index}, 'steel', -1)">-</button>
                                <input type="number" id="qty-${index}-steel" value="${steelQty}" min="1" max="1000" onchange="setQuantity(${index}, 'steel', this.value)">
                                <button onclick="adjustQuantity(${index}, 'steel', 1)">+</button>
                                <span class="rtrains-total-price">= ${steelQty * station.prices.steel} кр.</span>
                            </div>
                            <button class="game-btn" style="padding:5px 15px;" onclick="rtrainsBuy(${index}, 'steel')">Купить</button>
                            <button class="game-btn" style="padding:5px 15px;" onclick="rtrainsSell(${index}, 'steel')">Продать</button>
                        </div>
                        
                        <div class="rtrains-resource">
                            <span>🌾 Зерно: ${station.prices.grain} кредитов</span>
                            <div class="rtrains-quantity-selector">
                                <button onclick="adjustQuantity(${index}, 'grain', -1)">-</button>
                                <input type="number" id="qty-${index}-grain" value="${grainQty}" min="1" max="1000" onchange="setQuantity(${index}, 'grain', this.value)">
                                <button onclick="adjustQuantity(${index}, 'grain', 1)">+</button>
                                <span class="rtrains-total-price">= ${grainQty * station.prices.grain} кр.</span>
                            </div>
                            <button class="game-btn" style="padding:5px 15px;" onclick="rtrainsBuy(${index}, 'grain')">Купить</button>
                            <button class="game-btn" style="padding:5px 15px;" onclick="rtrainsSell(${index}, 'grain')">Продать</button>
                        </div>
                    </div>
                `;
            });
            
            container.innerHTML = html;
        }

        window.adjustQuantity = function(stationIndex, resource, delta) {
            const current = getQuantity(stationIndex, resource);
            setQuantity(stationIndex, resource, current + delta);
        };

        window.rtrainsBuy = function(stationIndex, resource) {
            const station = rtrainsStations[stationIndex];
            const price = station.prices[resource];
            const qty = getQuantity(stationIndex, resource);
            const totalCost = price * qty;
            
            if (rtrainsMoney >= totalCost) {
                rtrainsMoney -= totalCost;
                rtrainsInventory[resource] += qty;
                document.getElementById('rtrains-message').innerHTML = `Куплено ${qty} ед. ${getResourceName(resource)} за ${totalCost} кредитов.`;
                updateRTrainsUI();
                updateAchievement('rtrainsMoney', false, rtrainsMoney);
            } else {
                document.getElementById('rtrains-message').innerHTML = 'Недостаточно кредитов!';
            }
        };

        window.rtrainsSell = function(stationIndex, resource) {
            const station = rtrainsStations[stationIndex];
            const price = station.prices[resource];
            const qty = getQuantity(stationIndex, resource);
            const totalIncome = price * qty;
            
            if (rtrainsInventory[resource] >= qty) {
                rtrainsMoney += totalIncome;
                rtrainsInventory[resource] -= qty;
                document.getElementById('rtrains-message').innerHTML = `Продано ${qty} ед. ${getResourceName(resource)} за ${totalIncome} кредитов.`;
                updateRTrainsUI();
                updateAchievement('rtrainsMoney', false, rtrainsMoney);
            } else {
                document.getElementById('rtrains-message').innerHTML = `Недостаточно ${getResourceName(resource)} в инвентаре!`;
            }
        };

        window.rtrainsBuyTrain = function() {
            const cost = 500 + 100 * rtrainsTrains;
            if (rtrainsMoney >= cost) {
                rtrainsMoney -= cost;
                rtrainsTrains++;
                document.getElementById('rtrains-message').innerHTML = `Куплен новый поезд за ${cost} кредитов. Теперь у вас ${rtrainsTrains} поездов.`;
                updateRTrainsUI();
                updateAchievement('rtrainsMoney', false, rtrainsMoney);
            } else {
                document.getElementById('rtrains-message').innerHTML = 'Недостаточно кредитов для покупки поезда!';
            }
        };

        window.rtrainsNextTurn = function() {
            rtrainsStations.forEach(station => {
                station.prices.coal = Math.max(5, station.prices.coal + Math.floor(Math.random() * 10) - 5);
                station.prices.steel = Math.max(10, station.prices.steel + Math.floor(Math.random() * 20) - 10);
                station.prices.grain = Math.max(2, station.prices.grain + Math.floor(Math.random() * 8) - 4);
            });
            
            const events = [
                'Цены стабилизировались.',
                'На рынке ажиотаж!',
                'Кризис перепроизводства.',
                'Спрос на ресурсы вырос.',
                'Поезда ходят по расписанию.'
            ];
            document.getElementById('rtrains-message').innerHTML = events[Math.floor(Math.random() * events.length)];
            
            updateRTrainsUI();
        };

        function getResourceName(res) {
            const names = { coal: 'угля', steel: 'стали', grain: 'зерна' };
            return names[res];
        }

        // ================== ТАНЧИКИ 1985 ==================
        const tanksHTML = `
            <div>
                <div class="game-stats">
                    <span>❤️ Жизни: <span id="tanks-lives">3</span></span>
                    <span>💥 Счёт: <span id="tanks-score">0</span></span>
                    <span>🎚️ Уровень: 
                        <select id="tanks-difficulty" style="background:#0a0a0a; border:2px solid #5d4edb; color:white; padding:5px; border-radius:10px;">
                            <option value="easy">Лёгкий</option>
                            <option value="medium" selected>Средний</option>
                            <option value="hard">Сложный</option>
                            <option value="impossible">Невозможно</option>
                        </select>
                    </span>
                </div>
                <canvas id="tanksCanvas" class="tanks-canvas" width="800" height="400"></canvas>
                <div class="tank-controls">
                    <button onclick="tanksMove('up')">⬆️</button>
                    <button onclick="tanksMove('left')">⬅️</button>
                    <button onclick="tanksMove('down')">⬇️</button>
                    <button onclick="tanksMove('right')">➡️</button>
                    <button onclick="tanksShoot()">🔫</button>
                </div>
                <p style="text-align:center; color:#ffd966; margin-top:10px;">На ПК: стрелки + пробел. На телефоне: кнопки сверху.</p>
            </div>
        `;

        let tanksCanvas, tanksCtx;
        let tank, enemies, bullets, enemyBullets, walls;
        let tankLives = 3;
        let tanksScore = 0;
        let tanksGameOver = false;
        let tanksFrameCount = 0;
        let enemySpawnTimer = 0;
        let tankDirection = 'up';
        let keysPressed = { up: false, down: false, left: false, right: false, space: false };

        function initTanks() {
            tanksCanvas = document.getElementById('tanksCanvas');
            tanksCtx = tanksCanvas.getContext('2d');
            
            tankLives = 3;
            tanksScore = 0;
            tanksGameOver = false;
            tankDirection = 'up';
            
            document.getElementById('tanks-lives').textContent = tankLives;
            document.getElementById('tanks-score').textContent = tanksScore;
            
            generateTanksMap();
            
            tank = { x: 60, y: 60, width: 30, height: 30, speed: 3 };
            
            enemies = [];
            bullets = [];
            enemyBullets = [];
            
            for (let i = 0; i < 3; i++) {
                spawnEnemy();
            }
            
            window.addEventListener('keydown', tanksKeyDown);
            window.addEventListener('keyup', tanksKeyUp);
            
            if (gameInterval) clearInterval(gameInterval);
            gameInterval = setInterval(tanksUpdate, 50);
        }

        function generateTanksMap() {
            walls = [];
            const wallSize = 30;
            const cols = Math.floor(800 / wallSize);
            const rows = Math.floor(400 / wallSize);
            
            for (let i = 0; i < cols; i++) {
                for (let j = 0; j < rows; j++) {
                    if (i < 3 && j < 3) continue;
                    if (i > cols - 4 && j < 3) continue;
                    if (i < 3 && j > rows - 4) continue;
                    if (i > cols - 4 && j > rows - 4) continue;
                    
                    if (Math.random() < 0.3) {
                        walls.push({
                            x: i * wallSize,
                            y: j * wallSize,
                            width: wallSize,
                            height: wallSize
                        });
                    }
                }
            }
        }

        function spawnEnemy() {
            const difficulty = document.getElementById('tanks-difficulty').value;
            let speed;
            switch(difficulty) {
                case 'easy': speed = 1; break;
                case 'medium': speed = 2; break;
                case 'hard': speed = 3; break;
                case 'impossible': speed = 4; break;
                default: speed = 2;
            }
            
            const corner = Math.floor(Math.random() * 4);
            let x, y;
            switch(corner) {
                case 0: x = 750; y = 50; break;
                case 1: x = 50; y = 350; break;
                case 2: x = 750; y = 350; break;
                default: x = 700; y = 300; break;
            }
            
            enemies.push({
                x: x, y: y,
                width: 30, height: 30,
                speed: speed,
                direction: Math.floor(Math.random() * 4),
                shootTimer: 0
            });
        }

        function tanksKeyDown(e) {
            if (tanksGameOver) return;
            switch(e.key) {
                case 'ArrowUp': keysPressed.up = true; e.preventDefault(); tankDirection = 'up'; break;
                case 'ArrowDown': keysPressed.down = true; e.preventDefault(); tankDirection = 'down'; break;
                case 'ArrowLeft': keysPressed.left = true; e.preventDefault(); tankDirection = 'left'; break;
                case 'ArrowRight': keysPressed.right = true; e.preventDefault(); tankDirection = 'right'; break;
                case ' ': keysPressed.space = true; e.preventDefault(); tanksShoot(); break;
            }
        }

        function tanksKeyUp(e) {
            switch(e.key) {
                case 'ArrowUp': keysPressed.up = false; break;
                case 'ArrowDown': keysPressed.down = false; break;
                case 'ArrowLeft': keysPressed.left = false; break;
                case 'ArrowRight': keysPressed.right = false; break;
                case ' ': keysPressed.space = false; break;
            }
        }

        window.tanksMove = function(dir) {
            if (tanksGameOver) return;
            switch(dir) {
                case 'up': tank.y -= tank.speed; tankDirection = 'up'; break;
                case 'down': tank.y += tank.speed; tankDirection = 'down'; break;
                case 'left': tank.x -= tank.speed; tankDirection = 'left'; break;
                case 'right': tank.x += tank.speed; tankDirection = 'right'; break;
            }
            checkTankCollisions();
        };

        window.tanksShoot = function() {
            if (tanksGameOver) return;
            let bullet = {
                x: tank.x + tank.width/2 - 2,
                y: tank.y + tank.height/2 - 2,
                width: 4, height: 4,
                speed: 5,
                direction: tankDirection
            };
            bullets.push(bullet);
        };

        function checkTankCollisions() {
            if (tank.x < 0) tank.x = 0;
            if (tank.x > 770) tank.x = 770;
            if (tank.y < 0) tank.y = 0;
            if (tank.y > 370) tank.y = 370;
            
            walls.forEach(wall => {
                if (tank.x < wall.x + wall.width &&
                    tank.x + tank.width > wall.x &&
                    tank.y < wall.y + wall.height &&
                    tank.y + tank.height > wall.y) {
                    if (keysPressed.up) tank.y += tank.speed;
                    if (keysPressed.down) tank.y -= tank.speed;
                    if (keysPressed.left) tank.x += tank.speed;
                    if (keysPressed.right) tank.x -= tank.speed;
                }
            });
        }

        function tanksUpdate() {
            if (tanksGameOver) return;
            
            if (keysPressed.up) { tank.y -= tank.speed; tankDirection = 'up'; }
            if (keysPressed.down) { tank.y += tank.speed; tankDirection = 'down'; }
            if (keysPressed.left) { tank.x -= tank.speed; tankDirection = 'left'; }
            if (keysPressed.right) { tank.x += tank.speed; tankDirection = 'right'; }
            checkTankCollisions();
            
            enemies.forEach(enemy => {
                if (Math.random() < 0.02) {
                    enemy.direction = Math.floor(Math.random() * 4);
                }
                
                let newX = enemy.x, newY = enemy.y;
                switch(enemy.direction) {
                    case 0: newY -= enemy.speed; break;
                    case 1: newY += enemy.speed; break;
                    case 2: newX -= enemy.speed; break;
                    case 3: newX += enemy.speed; break;
                }
                
                if (newX >= 0 && newX <= 770 && newY >= 0 && newY <= 370) {
                    let collision = false;
                    walls.forEach(wall => {
                        if (newX < wall.x + wall.width &&
                            newX + enemy.width > wall.x &&
                            newY < wall.y + wall.height &&
                            newY + enemy.height > wall.y) {
                            collision = true;
                        }
                    });
                    if (!collision) {
                        enemy.x = newX;
                        enemy.y = newY;
                    } else {
                        enemy.direction = Math.floor(Math.random() * 4);
                    }
                } else {
                    enemy.direction = Math.floor(Math.random() * 4);
                }
                
                enemy.shootTimer++;
                const difficulty = document.getElementById('tanks-difficulty').value;
                let shootInterval = 100;
                switch(difficulty) {
                    case 'easy': shootInterval = 150; break;
                    case 'medium': shootInterval = 100; break;
                    case 'hard': shootInterval = 70; break;
                    case 'impossible': shootInterval = 40; break;
                }
                
                if (enemy.shootTimer > shootInterval) {
                    enemy.shootTimer = 0;
                    let dx = tank.x - enemy.x;
                    let dy = tank.y - enemy.y;
                    let bulletDir;
                    if (Math.abs(dx) > Math.abs(dy)) {
                        bulletDir = dx > 0 ? 'right' : 'left';
                    } else {
                        bulletDir = dy > 0 ? 'down' : 'up';
                    }
                    
                    enemyBullets.push({
                        x: enemy.x + enemy.width/2 - 2,
                        y: enemy.y + enemy.height/2 - 2,
                        width: 4, height: 4,
                        speed: 4,
                        direction: bulletDir
                    });
                }
            });
            
            bullets.forEach((bullet, index) => {
                switch(bullet.direction) {
                    case 'up': bullet.y -= bullet.speed; break;
                    case 'down': bullet.y += bullet.speed; break;
                    case 'left': bullet.x -= bullet.speed; break;
                    case 'right': bullet.x += bullet.speed; break;
                }
                
                enemies.forEach((enemy, eIndex) => {
                    if (bullet.x < enemy.x + enemy.width &&
                        bullet.x + bullet.width > enemy.x &&
                        bullet.y < enemy.y + enemy.height &&
                        bullet.y + bullet.height > enemy.y) {
                        enemies.splice(eIndex, 1);
                        bullets.splice(index, 1);
                        tanksScore += 100;
                        document.getElementById('tanks-score').textContent = tanksScore;
                        updateAchievement('tanksScore', false, tanksScore);
                        
                        spawnEnemy();
                    }
                });
                
                walls.forEach((wall, wIndex) => {
                    if (bullet.x < wall.x + wall.width &&
                        bullet.x + bullet.width > wall.x &&
                        bullet.y < wall.y + wall.height &&
                        bullet.y + bullet.height > wall.y) {
                        bullets.splice(index, 1);
                        walls.splice(wIndex, 1);
                    }
                });
                
                if (bullet.x < 0 || bullet.x > 800 || bullet.y < 0 || bullet.y > 400) {
                    bullets.splice(index, 1);
                }
            });
            
            enemyBullets.forEach((bullet, index) => {
                switch(bullet.direction) {
                    case 'up': bullet.y -= bullet.speed; break;
                    case 'down': bullet.y += bullet.speed; break;
                    case 'left': bullet.x -= bullet.speed; break;
                    case 'right': bullet.x += bullet.speed; break;
                }
                
                if (bullet.x < tank.x + tank.width &&
                    bullet.x + bullet.width > tank.x &&
                    bullet.y < tank.y + tank.height &&
                    bullet.y + bullet.height > tank.y) {
                    enemyBullets.splice(index, 1);
                    tankLives--;
                    document.getElementById('tanks-lives').textContent = tankLives;
                    
                    if (tankLives <= 0) {
                        tanksGameOver = true;
                        alert(`Игра окончена! Ваш счёт: ${tanksScore}`);
                        clearInterval(gameInterval);
                    }
                }
                
                walls.forEach((wall, wIndex) => {
                    if (bullet.x < wall.x + wall.width &&
                        bullet.x + bullet.width > wall.x &&
                        bullet.y < wall.y + wall.height &&
                        bullet.y + bullet.height > wall.y) {
                        enemyBullets.splice(index, 1);
                    }
                });
                
                if (bullet.x < 0 || bullet.x > 800 || bullet.y < 0 || bullet.y > 400) {
                    enemyBullets.splice(index, 1);
                }
            });
            
            enemySpawnTimer++;
            const difficulty = document.getElementById('tanks-difficulty').value;
            let spawnInterval = 100;
            switch(difficulty) {
                case 'easy': spawnInterval = 150; break;
                case 'medium': spawnInterval = 100; break;
                case 'hard': spawnInterval = 70; break;
                case 'impossible': spawnInterval = 40; break;
            }
            
            if (enemySpawnTimer > spawnInterval && enemies.length < 8) {
                enemySpawnTimer = 0;
                spawnEnemy();
            }
            
            tanksDraw();
        }

        function tanksDraw() {
            tanksCtx.clearRect(0, 0, 800, 400);
            
            tanksCtx.fillStyle = '#1a1a2a';
            tanksCtx.fillRect(0, 0, 800, 400);
            
            tanksCtx.fillStyle = '#8B4513';
            walls.forEach(wall => {
                tanksCtx.fillRect(wall.x, wall.y, wall.width, wall.height);
                tanksCtx.strokeStyle = '#A0522D';
                tanksCtx.lineWidth = 2;
                tanksCtx.strokeRect(wall.x, wall.y, wall.width, wall.height);
            });
            
            enemies.forEach(enemy => {
                tanksCtx.fillStyle = '#FF0000';
                tanksCtx.fillRect(enemy.x, enemy.y, enemy.width, enemy.height);
                tanksCtx.fillStyle = '#8B0000';
                switch(enemy.direction) {
                    case 0: tanksCtx.fillRect(enemy.x + 12, enemy.y - 5, 6, 10); break;
                    case 1: tanksCtx.fillRect(enemy.x + 12, enemy.y + 25, 6, 10); break;
                    case 2: tanksCtx.fillRect(enemy.x - 5, enemy.y + 12, 10, 6); break;
                    case 3: tanksCtx.fillRect(enemy.x + 25, enemy.y + 12, 10, 6); break;
                }
            });
            
            tanksCtx.fillStyle = '#00FF00';
            tanksCtx.fillRect(tank.x, tank.y, tank.width, tank.height);
            tanksCtx.fillStyle = '#006400';
            switch(tankDirection) {
                case 'up': tanksCtx.fillRect(tank.x + 12, tank.y - 5, 6, 10); break;
                case 'down': tanksCtx.fillRect(tank.x + 12, tank.y + 25, 6, 10); break;
                case 'left': tanksCtx.fillRect(tank.x - 5, tank.y + 12, 10, 6); break;
                case 'right': tanksCtx.fillRect(tank.x + 25, tank.y + 12, 10, 6); break;
            }
            
            tanksCtx.fillStyle = '#FFFF00';
            bullets.forEach(bullet => {
                tanksCtx.fillRect(bullet.x, bullet.y, bullet.width, bullet.height);
            });
            
            tanksCtx.fillStyle = '#FFA500';
            enemyBullets.forEach(bullet => {
                tanksCtx.fillRect(bullet.x, bullet.y, bullet.width, bullet.height);
            });
        }

        // ================== 3D ИГРЫ ==================
        const modal3D = document.getElementById('gameModal3D');
        const title3D = document.getElementById('gameTitle3D');
        const container3D = document.getElementById('babylonContainer');
        const controls3D = document.getElementById('game3dControls');
        let current3DGame = null;
        let engine, scene, camera, canvas;

        function openGame3D(game) {
            modal3D.classList.add('active');
            current3DGame = game;
            registerGamePlayed(game);
            
            if (game === 'bus') {
                title3D.textContent = '🚌 Добеги до электробуса (ЭКСКЛЮЗИВ)';
            } else if (game === 'birds') {
                title3D.textContent = '🔫 Охота на птиц (ЭКСКЛЮЗИВ)';
            } else if (game === 'minecraft') {
                title3D.textContent = '⛏️ Minecraft (ЭКСКЛЮЗИВ)';
                updateAchievement('minecraftWalk', true);
            } else if (game === 'racing') {
                title3D.textContent = '🏎️ Гонки 3D';
            }
            
            container3D.innerHTML = '<canvas id="babylonCanvas" style="width:100%; height:100%;"></canvas>';
            canvas = document.getElementById('babylonCanvas');
            if (engine) engine.dispose();
            engine = new BABYLON.Engine(canvas, true);
            
            if (game === 'bus') {
                createBusScene();
            } else if (game === 'birds') {
                createBirdHuntScene();
            } else if (game === 'minecraft') {
                createMinecraftScene();
            } else if (game === 'racing') {
                createRacingScene();
            }
            
            engine.runRenderLoop(() => scene.render());
            window.addEventListener('resize', () => engine.resize());
        }

        function closeGame3D() {
            modal3D.classList.remove('active');
            if (engine) engine.dispose();
            engine = null;
            current3DGame = null;
            window.removeEventListener('keydown', window.busKeyHandler);
            window.removeEventListener('keydown', window.racingKeyHandler);
            if (canvas) {
                canvas.removeEventListener('click', window.birdShootHandler);
            }
        }

        // ---------- 3D Добеги до электробуса ----------
        function createBusScene() {
            scene = new BABYLON.Scene(engine);
            scene.clearColor = new BABYLON.Color3(0.1, 0.1, 0.2);
            camera = new BABYLON.ArcRotateCamera("camera", -Math.PI/2, Math.PI/3, 20, BABYLON.Vector3.Zero(), scene);
            camera.attachControl(canvas, true);
            new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0,1,0), scene);

            const road = BABYLON.MeshBuilder.CreateGround("road", {width: 50, height: 10}, scene);
            road.material = new BABYLON.StandardMaterial("roadMat", scene);
            road.material.diffuseColor = new BABYLON.Color3(0.2, 0.2, 0.3);

            const bus = BABYLON.MeshBuilder.CreateBox("bus", {width: 2, height: 1, depth: 4}, scene);
            bus.position.y = 0.5;
            bus.material = new BABYLON.StandardMaterial("busMat", scene);
            bus.material.diffuseColor = new BABYLON.Color3(1, 0.8, 0);

            const runner = BABYLON.MeshBuilder.CreateCapsule("runner", {radius: 0.3, height: 1.5}, scene);
            runner.position.y = 0.75;
            runner.position.x = -8;
            runner.material = new BABYLON.StandardMaterial("runnerMat", scene);
            runner.material.diffuseColor = new BABYLON.Color3(0, 0.5, 1);

            let people = [];
            for (let i = 0; i < 20; i++) {
                const person = BABYLON.MeshBuilder.CreateSphere("person"+i, {diameter: 0.6}, scene);
                resetPerson(person, i);
                person.material = new BABYLON.StandardMaterial("personMat", scene);
                person.material.diffuseColor = new BABYLON.Color3(1, 0, 0);
                people.push(person);
            }

            function resetPerson(person, index) {
                person.position.x = Math.random() * 20 - 10;
                person.position.z = 10 + Math.random() * 5;
                person.position.y = 0.3;
                person.speed = 0.15;
            }

            const stops = [];
            for (let i = 0; i < 10; i++) {
                const stop = BABYLON.MeshBuilder.CreateBox("stop"+i, {width: 0.5, height: 0.2, depth: 1}, scene);
                stop.position.x = i * 4 - 18;
                stop.position.y = 0.1;
                stop.material = new BABYLON.StandardMaterial("stopMat", scene);
                stop.material.diffuseColor = new BABYLON.Color3(0.8, 0.2, 0.2);
                stops.push(stop);
            }

            let mode = 'bus';
            let stopIndex = 0;
            let peoplePassed = 0;
            let achievementShown = false;

            const gui = BABYLON.GUI.AdvancedDynamicTexture.CreateFullscreenUI("UI");
            const counterText = new BABYLON.GUI.TextBlock();
            counterText.text = "Пройдено людей: 0";
            counterText.color = "white";
            counterText.fontSize = 24;
            counterText.top = "20px";
            counterText.left = "20px";
            counterText.horizontalAlignment = BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
            counterText.verticalAlignment = BABYLON.GUI.Control.VERTICAL_ALIGNMENT_TOP;
            gui.addControl(counterText);

            controls3D.innerHTML = `
                <button class="game-btn" onclick="setBusMode('bus')">За руль</button>
                <button class="game-btn" onclick="setBusMode('run')">Бежать</button>
                <p id="busInfo">Остановка 0/10 | Людей: 0</p>
                <p style="color:#ffd966; font-size:14px;">Управление стрелками: вверх/вниз (автобус), влево/вправо (бег)</p>
            `;

            window.setBusMode = function(m) {
                mode = m;
                bus.setEnabled(mode === 'bus');
                runner.setEnabled(mode === 'run');
                if (mode === 'run') {
                    peoplePassed = 0;
                    counterText.text = "Пройдено людей: 0";
                    achievementShown = false;
                    people.forEach((p, idx) => resetPerson(p, idx));
                }
            };

            window.busMove = function(dir) {
                if (mode !== 'bus') return;
                if (dir === 'next') {
                    stopIndex = (stopIndex + 1) % 10;
                    bus.position.x = stopIndex * 4 - 18;
                    document.getElementById('busInfo').innerText = `Остановка ${stopIndex}/10 | Людей: ${peoplePassed}`;
                    if ('speechSynthesis' in window) {
                        const msg = new SpeechSynthesisUtterance(`Остановка ${stopIndex + 1}`);
                        msg.lang = 'ru-RU';
                        window.speechSynthesis.speak(msg);
                    }
                    peoplePassed += Math.floor(Math.random() * 3);
                }
            };

            window.runnerMove = function(dir) {
                if (mode !== 'run') return;
                if (dir === 'left') runner.position.x -= 1;
                else if (dir === 'right') runner.position.x += 1;
                if (runner.position.x < -10) runner.position.x = -10;
                if (runner.position.x > 10) runner.position.x = 10;
            };

            window.busKeyHandler = function(e) {
                const key = e.key;
                if (mode === 'bus') {
                    if (key === 'ArrowUp' || key === 'ArrowDown') {
                        window.busMove('next');
                    }
                } else if (mode === 'run') {
                    if (key === 'ArrowLeft') window.runnerMove('left');
                    if (key === 'ArrowRight') window.runnerMove('right');
                }
            };
            window.addEventListener('keydown', window.busKeyHandler);

            let busPeoplePassed = 0;
            scene.onBeforeRenderObservable.add(() => {
                if (mode !== 'run') return;

                people.forEach(person => {
                    person.position.z -= person.speed;

                    if (BABYLON.Vector3.Distance(runner.position, person.position) < 1) {
                        alert('Столкновение! Конец игры');
                        runner.position.x = -8;
                        peoplePassed = 0;
                        counterText.text = "Пройдено людей: 0";
                        people.forEach((p, idx) => resetPerson(p, idx));
                        return;
                    }

                    if (person.position.z < -10) {
                        peoplePassed++;
                        counterText.text = "Пройдено людей: " + peoplePassed;
                        busPeoplePassed = peoplePassed;
                        updateAchievement('busPeople', false, peoplePassed);

                        if (peoplePassed >= 1000 && !achievementShown) {
                            achievementShown = true;
                            alert('Слушай, иди отдохни! Ты 1000 людей пробежал и много времени потратил.');
                        }

                        resetPerson(person, 0);
                    }
                });
            });

            window.saveBus3DScore = function(name, score) {
                let records = JSON.parse(localStorage.getItem('bus3DLeaderboard') || '[]');
                records.push({name, score});
                records.sort((a,b) => b.score - a.score);
                records = records.slice(0,5);
                localStorage.setItem('bus3DLeaderboard', JSON.stringify(records));
                alert('Рекорд сохранён');
            };
        }

        // ---------- Охота на птиц ----------
        function createBirdHuntScene() {
            scene = new BABYLON.Scene(engine);
            scene.clearColor = new BABYLON.Color3(0.2, 0.5, 0.8);
            
            camera = new BABYLON.UniversalCamera("camera", new BABYLON.Vector3(0, 2, -10), scene);
            camera.setTarget(BABYLON.Vector3.Zero());
            camera.attachControl(canvas, true);
            
            new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene);
            
            const ground = BABYLON.MeshBuilder.CreateGround("ground", {width: 30, height: 30}, scene);
            ground.material = new BABYLON.StandardMaterial("groundMat", scene);
            ground.material.diffuseColor = new BABYLON.Color3(0.3, 0.6, 0.2);
            ground.position.y = -0.5;
            
            for (let i = 0; i < 10; i++) {
                const treeTrunk = BABYLON.MeshBuilder.CreateCylinder("treeTrunk" + i, {height: 2, diameter: 0.3}, scene);
                treeTrunk.position.x = Math.random() * 20 - 10;
                treeTrunk.position.z = Math.random() * 20 - 10;
                treeTrunk.position.y = 0.5;
                treeTrunk.material = new BABYLON.StandardMaterial("treeMat", scene);
                treeTrunk.material.diffuseColor = new BABYLON.Color3(0.5, 0.3, 0.1);
                
                const treeTop = BABYLON.MeshBuilder.CreateSphere("treeTop" + i, {diameter: 0.8}, scene);
                treeTop.position.x = treeTrunk.position.x;
                treeTop.position.y = 1.8;
                treeTop.position.z = treeTrunk.position.z;
                treeTop.material = new BABYLON.StandardMaterial("treeTopMat", scene);
                treeTop.material.diffuseColor = new BABYLON.Color3(0, 0.8, 0);
            }
            
            const gun = BABYLON.MeshBuilder.CreateBox("gun", {width: 0.2, height: 0.2, depth: 1}, scene);
            gun.position = new BABYLON.Vector3(0, 1.5, -8);
            gun.rotation.x = Math.PI / 4;
            gun.material = new BABYLON.StandardMaterial("gunMat", scene);
            gun.material.diffuseColor = new BABYLON.Color3(0.4, 0.4, 0.4);
            
            let birds = [];
            const maxBirds = 10;
            let score = 0;
            let gunLevel = 1;
            let lastShotTime = 0;
            const shotCooldown = 500 / gunLevel;
            
            const gui = BABYLON.GUI.AdvancedDynamicTexture.CreateFullscreenUI("UI");
            const scoreText = new BABYLON.GUI.TextBlock();
            scoreText.text = "Очки: 0";
            scoreText.color = "white";
            scoreText.fontSize = 24;
            scoreText.top = "20px";
            scoreText.left = "20px";
            scoreText.horizontalAlignment = BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
            scoreText.verticalAlignment = BABYLON.GUI.Control.VERTICAL_ALIGNMENT_TOP;
            gui.addControl(scoreText);
            
            const gunLevelText = new BABYLON.GUI.TextBlock();
            gunLevelText.text = "Ружьё: уровень 1";
            gunLevelText.color = "white";
            gunLevelText.fontSize = 24;
            gunLevelText.top = "60px";
            gunLevelText.left = "20px";
            gunLevelText.horizontalAlignment = BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_LEFT;
            gunLevelText.verticalAlignment = BABYLON.GUI.Control.VERTICAL_ALIGNMENT_TOP;
            gui.addControl(gunLevelText);
            
            const upgradeButton = BABYLON.GUI.Button.CreateSimpleButton("upgrade", "Купить новое ружьё (50 очков)");
            upgradeButton.width = "200px";
            upgradeButton.height = "40px";
            upgradeButton.color = "white";
            upgradeButton.background = "#5d4edb";
            upgradeButton.top = "20px";
            upgradeButton.right = "20px";
            upgradeButton.horizontalAlignment = BABYLON.GUI.Control.HORIZONTAL_ALIGNMENT_RIGHT;
            upgradeButton.verticalAlignment = BABYLON.GUI.Control.VERTICAL_ALIGNMENT_TOP;
            upgradeButton.onPointerUpObservable.add(() => {
                if (score >= 50) {
                    score -= 50;
                    gunLevel++;
                    gunLevelText.text = "Ружьё: уровень " + gunLevel;
                    scoreText.text = "Очки: " + score;
                    updateAchievement('birdGun', false, gunLevel);
                } else {
                    alert("Недостаточно очков! Нужно 50.");
                }
            });
            gui.addControl(upgradeButton);
            
            function createBird() {
                if (birds.length >= maxBirds) return;
                
                const bird = BABYLON.MeshBuilder.CreateSphere("bird" + Date.now() + Math.random(), {diameter: 0.3}, scene);
                bird.position.x = Math.random() * 20 - 10;
                bird.position.y = Math.random() * 8 + 2;
                bird.position.z = Math.random() * 10 + 5;
                
                bird.material = new BABYLON.StandardMaterial("birdMat", scene);
                bird.material.diffuseColor = new BABYLON.Color3(Math.random(), Math.random(), Math.random());
                
                bird.speed = new BABYLON.Vector3(
                    (Math.random() - 0.5) * 0.05,
                    (Math.random() - 0.5) * 0.03,
                    (Math.random() - 0.5) * 0.05
                );
                
                birds.push(bird);
            }
            
            for (let i = 0; i < 5; i++) {
                createBird();
            }
            
            setInterval(() => {
                if (current3DGame === 'birds') {
                    createBird();
                }
            }, 2000);
            
            window.birdShootHandler = function(event) {
                if (current3DGame !== 'birds') return;
                
                const now = Date.now();
                if (now - lastShotTime < shotCooldown) return;
                lastShotTime = now;
                
                const pickResult = scene.pick(scene.pointerX, scene.pointerY);
                if (pickResult.hit && pickResult.pickedMesh && pickResult.pickedMesh.name.includes('bird')) {
                    const birdIndex = birds.indexOf(pickResult.pickedMesh);
                    if (birdIndex !== -1) {
                        birds.splice(birdIndex, 1);
                        pickResult.pickedMesh.dispose();
                        score += 10;
                        scoreText.text = "Очки: " + score;
                    }
                }
            };
            
            canvas.addEventListener('click', window.birdShootHandler);
            
            scene.onBeforeRenderObservable.add(() => {
                birds.forEach((bird, index) => {
                    bird.position.addInPlace(bird.speed);
                    
                    if (bird.position.x > 10 || bird.position.x < -10) bird.speed.x *= -1;
                    if (bird.position.y > 10 || bird.position.y < 1) bird.speed.y *= -1;
                    if (bird.position.z > 15 || bird.position.z < 0) bird.speed.z *= -1;
                });
            });
            
            controls3D.innerHTML = `
                <p style="color:#ffd966; font-size:14px;">Кликните по птице, чтобы выстрелить. За каждую птицу +10 очков.</p>
            `;
        }

        // ---------- Minecraft ----------
        function createMinecraftScene() {
            scene = new BABYLON.Scene(engine);
            scene.clearColor = new BABYLON.Color3(0.5, 0.7, 1.0);
            
            camera = new BABYLON.UniversalCamera("camera", new BABYLON.Vector3(5, 2, 5), scene);
            camera.setTarget(new BABYLON.Vector3(0, 2, 0));
            camera.attachControl(canvas, true);
            camera.speed = 0.3;
            camera.angularSensibility = 2000;
            
            camera.applyGravity = true;
            camera.ellipsoid = new BABYLON.Vector3(0.5, 1, 0.5);
            camera.checkCollisions = true;
            
            new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene);
            const dirLight = new BABYLON.DirectionalLight("dirLight", new BABYLON.Vector3(-1, -2, -1), scene);
            dirLight.position = new BABYLON.Vector3(10, 20, 10);
            
            const ground = BABYLON.MeshBuilder.CreateGround("ground", {width: 20, height: 20}, scene);
            ground.material = new BABYLON.StandardMaterial("groundMat", scene);
            ground.material.diffuseColor = new BABYLON.Color3(0.3, 0.6, 0.2);
            ground.material.diffuseTexture = new BABYLON.Texture("https://www.babylonjs.com/assets/ground.jpg", scene);
            ground.checkCollisions = true;
            
            const blockSize = 1;
            const blocks = [];
            
            function createBlock(x, y, z, type) {
                const block = BABYLON.MeshBuilder.CreateBox("block", {size: blockSize}, scene);
                block.position = new BABYLON.Vector3(x, y, z);
                
                const material = new BABYLON.StandardMaterial("blockMat", scene);
                
                switch(type) {
                    case 'grass':
                        material.diffuseColor = new BABYLON.Color3(0.2, 0.8, 0.2);
                        break;
                    case 'dirt':
                        material.diffuseColor = new BABYLON.Color3(0.6, 0.4, 0.2);
                        break;
                    case 'stone':
                        material.diffuseColor = new BABYLON.Color3(0.5, 0.5, 0.5);
                        break;
                    case 'wood':
                        material.diffuseColor = new BABYLON.Color3(0.6, 0.4, 0.1);
                        break;
                    case 'leaf':
                        material.diffuseColor = new BABYLON.Color3(0.1, 0.6, 0.1);
                        break;
                }
                
                block.material = material;
                block.checkCollisions = true;
                block.type = type;
                return block;
            }
            
            for (let x = -5; x <= 5; x++) {
                for (let z = -5; z <= 5; z++) {
                    blocks.push(createBlock(x, 0, z, 'grass'));
                    
                    for (let y = -1; y >= -3; y--) {
                        blocks.push(createBlock(x, y, z, 'dirt'));
                    }
                    
                    for (let y = -4; y >= -5; y--) {
                        blocks.push(createBlock(x, y, z, 'stone'));
                    }
                }
            }
            
            const treeX = 2;
            const treeZ = 2;
            for (let y = 1; y <= 4; y++) {
                blocks.push(createBlock(treeX, y, treeZ, 'wood'));
            }
            for (let dx = -1; dx <= 1; dx++) {
                for (let dz = -1; dz <= 1; dz++) {
                    for (let dy = 4; dy <= 5; dy++) {
                        if (Math.abs(dx) + Math.abs(dz) + Math.abs(dy-4) <= 3) {
                            blocks.push(createBlock(treeX + dx, dy, treeZ + dz, 'leaf'));
                        }
                    }
                }
            }
            
            controls3D.innerHTML = `
                <p style="color:#ffd966; font-size:14px;">
                    WASD — движение | Пробел — прыжок | Shift — присесть | Мышь — осмотр<br>
                    ЛКМ по блоку — сломать | ПКМ — поставить камень
                </p>
            `;
            
            canvas.addEventListener('mousedown', (event) => {
                if (current3DGame !== 'minecraft') return;
                
                const pickResult = scene.pick(scene.pointerX, scene.pointerY);
                if (pickResult.hit && pickResult.pickedMesh) {
                    const mesh = pickResult.pickedMesh;
                    
                    if (event.button === 0 && mesh.name !== 'ground') {
                        const index = blocks.indexOf(mesh);
                        if (index !== -1) {
                            blocks.splice(index, 1);
                            mesh.dispose();
                        }
                    }
                    
                    if (event.button === 2) {
                        event.preventDefault();
                        
                        const face = pickResult.faceId;
                        const point = pickResult.pickedPoint;
                        const normal = mesh.getFaceNormal(face);
                        
                        if (point && normal) {
                            const newPos = point.add(normal.scale(0.5));
                            newPos.x = Math.round(newPos.x);
                            newPos.y = Math.round(newPos.y);
                            newPos.z = Math.round(newPos.z);
                            
                            let exists = false;
                            blocks.forEach(block => {
                                if (block.position.x === newPos.x && 
                                    block.position.y === newPos.y && 
                                    block.position.z === newPos.z) {
                                    exists = true;
                                }
                            });
                            
                            if (!exists) {
                                const newBlock = createBlock(newPos.x, newPos.y, newPos.z, 'stone');
                                blocks.push(newBlock);
                            }
                        }
                    }
                }
            });
            
            canvas.addEventListener('contextmenu', (e) => e.preventDefault());
        }

        // ---------- НОВАЯ ИГРА: Гонки 3D (круговая трасса, исправленное управление) ----------
        function createRacingScene() {
            scene = new BABYLON.Scene(engine);
            scene.clearColor = new BABYLON.Color3(0.5, 0.7, 1.0);
            
            camera = new BABYLON.FollowCamera("camera", new BABYLON.Vector3(0, 5, -10), scene);
            camera.radius = 10;
            camera.heightOffset = 4;
            camera.rotationOffset = 0;
            camera.cameraAcceleration = 0.1;
            camera.maxCameraSpeed = 5;
            
            new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene);
            const dirLight = new BABYLON.DirectionalLight("dirLight", new BABYLON.Vector3(-1, -2, -1), scene);
            dirLight.position = new BABYLON.Vector3(10, 20, 10);
            
            const car = BABYLON.MeshBuilder.CreateBox("car", {width: 2, height: 1, depth: 4}, scene);
            car.position.y = 0.5;
            car.material = new BABYLON.StandardMaterial("carMat", scene);
            car.material.diffuseColor = new BABYLON.Color3(1, 0, 0);
            
            const wheelPositions = [
                [-1, 0.2, 1.5],
                [1, 0.2, 1.5],
                [-1, 0.2, -1.5],
                [1, 0.2, -1.5]
            ];
            wheelPositions.forEach(pos => {
                const wheel = BABYLON.MeshBuilder.CreateCylinder("wheel", {height: 0.5, diameter: 0.8}, scene);
                wheel.position = new BABYLON.Vector3(pos[0], pos[1], pos[2]);
                wheel.rotation.z = Math.PI / 2;
                wheel.material = new BABYLON.StandardMaterial("wheelMat", scene);
                wheel.material.diffuseColor = new BABYLON.Color3(0.2, 0.2, 0.2);
            });
            
            camera.lockedTarget = car;
            
            const trackRadius = 30;
            const trackWidth = 8;
            const segments = 64;
            
            const roadMaterial = new BABYLON.StandardMaterial("roadMat", scene);
            roadMaterial.diffuseColor = new BABYLON.Color3(0.3, 0.3, 0.3);
            
            const barrierMaterial = new BABYLON.StandardMaterial("barrierMat", scene);
            barrierMaterial.diffuseColor = new BABYLON.Color3(1, 1, 0);
            
            for (let i = 0; i < segments; i++) {
                const angle = (i / segments) * Math.PI * 2;
                const nextAngle = ((i + 1) / segments) * Math.PI * 2;
                
                const x1 = Math.cos(angle) * trackRadius;
                const z1 = Math.sin(angle) * trackRadius;
                const x2 = Math.cos(nextAngle) * trackRadius;
                const z2 = Math.sin(nextAngle) * trackRadius;
                
                const roadSegment = BABYLON.MeshBuilder.CreateGround("road" + i, {width: trackWidth, height: 2, subdivisions: 1}, scene);
                roadSegment.position = new BABYLON.Vector3((x1 + x2) / 2, 0, (z1 + z2) / 2);
                roadSegment.rotation.y = -angle;
                roadSegment.material = roadMaterial;
                
                const innerBarrier = BABYLON.MeshBuilder.CreateBox("innerBarrier" + i, {width: 0.5, height: 1, depth: 2}, scene);
                innerBarrier.position = new BABYLON.Vector3(
                    Math.cos(angle) * (trackRadius - trackWidth/2 - 0.5),
                    0.5,
                    Math.sin(angle) * (trackRadius - trackWidth/2 - 0.5)
                );
                innerBarrier.rotation.y = -angle;
                innerBarrier.material = barrierMaterial;
                
                const outerBarrier = BABYLON.MeshBuilder.CreateBox("outerBarrier" + i, {width: 0.5, height: 1, depth: 2}, scene);
                outerBarrier.position = new BABYLON.Vector3(
                    Math.cos(angle) * (trackRadius + trackWidth/2 + 0.5),
                    0.5,
                    Math.sin(angle) * (trackRadius + trackWidth/2 + 0.5)
                );
                outerBarrier.rotation.y = -angle;
                outerBarrier.material = barrierMaterial;
            }
            
            let speed = 0;
            const maxSpeed = 10;
            const acceleration = 0.2;
            const turnSpeed = 0.03;
            let nitro = 100;
            
            controls3D.innerHTML = `
                <p style="color:#ffd966; font-size:14px;">
                    ↑ — газ (вперёд), ↓ — тормоз/назад, ← → — поворот, Пробел — ускорение (нитро)
                </p>
                <p>Скорость: <span id="racing-speed">0</span> км/ч | Нитро: <span id="racing-nitro">100</span>%</p>
                <p>Дистанция: <span id="racing-distance">0</span> м | Круги: <span id="racing-laps">0</span></p>
            `;
            
            let distance = 0;
            let laps = 0;
            let lastAngle = 0;
            let leftPressed = false, rightPressed = false, upPressed = false, downPressed = false, spacePressed = false;
            
            window.racingKeyHandler = function(e) {
                const isDown = e.type === 'keydown';
                switch(e.key) {
                    case 'ArrowLeft': leftPressed = isDown; e.preventDefault(); break;
                    case 'ArrowRight': rightPressed = isDown; e.preventDefault(); break;
                    case 'ArrowUp': upPressed = isDown; e.preventDefault(); break;
                    case 'ArrowDown': downPressed = isDown; e.preventDefault(); break;
                    case ' ': spacePressed = isDown; e.preventDefault(); break;
                }
            };
            
            window.addEventListener('keydown', window.racingKeyHandler);
            window.addEventListener('keyup', window.racingKeyHandler);
            
            scene.onBeforeRenderObservable.add(() => {
                if (upPressed) speed = Math.min(speed + acceleration, maxSpeed);
                if (downPressed) speed = Math.max(speed - acceleration, -maxSpeed/2);
                if (spacePressed && nitro > 0) {
                    speed = Math.min(speed + acceleration * 2, maxSpeed * 1.5);
                    nitro = Math.max(nitro - 0.5, 0);
                }
                
                if (Math.abs(speed) > 0.1) {
                    if (leftPressed) car.rotation.y += turnSpeed * (speed / maxSpeed);
                    if (rightPressed) car.rotation.y -= turnSpeed * (speed / maxSpeed);
                }
                
                const forward = new BABYLON.Vector3(0, 0, 1);
                const direction = BABYLON.Vector3.TransformNormal(forward, car.getWorldMatrix());
                car.position.addInPlace(direction.scale(speed * 0.1));
                
                speed *= 0.98;
                if (Math.abs(speed) < 0.01) speed = 0;
                
                const carAngle = Math.atan2(car.position.z, car.position.x);
                distance += Math.abs(speed) * 0.1;
                
                if (lastAngle < -Math.PI/2 && carAngle > Math.PI/2) {
                    laps++;
                    document.getElementById('racing-laps').textContent = laps;
                }
                lastAngle = carAngle;
                
                document.getElementById('racing-speed').textContent = Math.abs(speed).toFixed(1);
                document.getElementById('racing-nitro').textContent = nitro.toFixed(0);
                document.getElementById('racing-distance').textContent = distance.toFixed(0);
                
                const distFromCenter = Math.sqrt(car.position.x * car.position.x + car.position.z * car.position.z);
                if (distFromCenter < trackRadius - trackWidth/2 - 1 || distFromCenter > trackRadius + trackWidth/2 + 1) {
                    alert('Вы вылетели с трассы! Игра окончена.');
                    updateAchievement('racingWin', false, distance);
                    scene.dispose();
                }
                
                if (distance >= 1000) {
                    updateAchievement('racingWin', false, distance);
                }
            });
        }

        // ================== УЛУЧШЕННЫЙ ИИ ==================
        const aiModal = document.getElementById('aiModal');
        const chatMessages = document.getElementById('chatMessages');
        const chatInput = document.getElementById('chatInput');

        function openAI() {
            aiModal.classList.add('active');
            updateAchievement('ai', true);
            if (chatMessages.children.length === 0) {
                chatMessages.innerHTML = '<div class="chat-message bot"><span>Привет! Я улучшенный ИИ-помощник. Спроси меня о чём угодно!</span></div>';
            }
        }

        function closeAI() {
            aiModal.classList.remove('active');
        }

        function sendMessage() {
            const text = chatInput.value.trim();
            if (!text) return;
            chatMessages.innerHTML += `<div class="chat-message user"><span>${escapeHTML(text)}</span></div>`;
            chatInput.value = '';
            setTimeout(() => {
                const reply = generateAIResponse(text);
                chatMessages.innerHTML += `<div class="chat-message bot"><span>${escapeHTML(reply)}</span></div>`;
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }, 500);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function generateAIResponse(question) {
            const q = question.toLowerCase().trim();

            if (q.match(/^(привет|здравствуй|хай|ку|прив|hello)/i)) {
                return randomChoice(['Привет! Чем могу помочь?', 'Здравствуй! Рад тебя видеть.', 'Хай! Задавай вопросы.', 'Приветствую! Как твои дела?']);
            }
            if (q.includes('как дела') || q.includes('как ты')) {
                return randomChoice(['У меня всё отлично, я же программа!', 'Хорошо, спасибо! А у тебя?', 'Нормально, работаю в фоне.', 'Лучше всех! Жду новых вопросов.']);
            }
            if (q.includes('как тебя зовут') || q.includes('твоё имя') || q.includes('имя')) {
                return 'Меня зовут R_52_X BETA AI, я ваш улучшенный помощник.';
            }
            if (q.includes('кто тебя создал') || q.includes('твой создатель')) {
                return 'Меня создала компания R_52_X в рамках тестирования новых технологий.';
            }
            if (q.includes('что ты умеешь') || q.includes('твои функции')) {
                return 'Я умею отвечать на вопросы, рассказывать новости (открой раздел "Новости"), шутить, поддерживать диалог. Ещё я могу сказать текущее время и дату.';
            }
            if (q.includes('который час') || q.includes('сколько времени') || q.includes('текущее время')) {
                return `Сейчас ${new Date().toLocaleTimeString('ru-RU')}.`;
            }
            if (q.includes('какая дата') || q.includes('сегодня число') || q.includes('какой сегодня день')) {
                return `Сегодня ${new Date().toLocaleDateString('ru-RU')}.`;
            }
            if (q.includes('погода') || q.includes('температура') || q.includes('на улице')) {
                return 'Я пока не умею получать реальную погоду, но могу сказать, что на нашем сайте всегда тепло и уютно 😊';
            }
            if (q.includes('шутка') || q.includes('анекдот') || q.includes('рассмеши')) {
                return randomChoice([
                    'Почему программисты путают Хэллоуин и Рождество? Потому что Oct 31 = Dec 25.',
                    'Входит мужик в бар, а там табличка: "Рекурсия", он заходит, а там табличка: "Рекурсия"...',
                    'Сколько программистов нужно, чтобы заменить лампочку? Ни одного, это проблема железа.',
                    'Чайник попросил у ноутбука пароль от Wi-Fi. Ноутбук: "Не скажу, вдруг ты мой пароль сольёшь в интернет!"'
                ]);
            }
            if (q.includes('ты классный') || q.includes('ты крутой') || q.includes('молодец')) {
                return 'Спасибо! Ты тоже!';
            }
            if (q.includes('пока') || q.includes('до свидания') || q.includes('увидимся')) {
                return 'Пока! Заходи ещё.';
            }
            if (q.includes('новости') || q.includes('что нового')) {
                return 'Свежие новости можно посмотреть в разделе "Новости" (кнопка в меню). Там загружаются реальные новости России.';
            }
            if (q.includes('игра') || q.includes('поиграть') || q.includes('электробус') || q.includes('rtrains') || q.includes('птиц') || q.includes('динозавр') || q.includes('шарик') || q.includes('minecraft') || q.includes('танчик') || q.includes('тетрис') || q.includes('гонк')) {
                return 'На сайте сейчас девять игр: четыре эксклюзивные ("Добеги до электробуса", "R-TRAINS", "Охота на птиц", "Minecraft") и пять классических ("Динозаврик", "Воздушный шарик", "Танчики 1985", "Тетрис", "Гонки 3D"). Заходи в раздел "Игры"!';
            }
            if (q.includes('достижени') || q.includes('ачивка')) {
                return 'У нас есть система достижений! Нажми на 🏆 Достижения в меню, чтобы посмотреть все достижения и свой прогресс.';
            }
            if (q.includes('тайный раздел') || q.includes('секрет')) {
                return 'Тайный раздел открывается кликом по нику R_52_X BETA в шапке сайта. Пароль: 52525267. Попробуй!';
            }

            return randomChoice([
                'Интересный вопрос. Я ещё учусь, но обязательно найду ответ в будущем!',
                'Хм, я не совсем понял. Можешь перефразировать?',
                'Забавно, но я пока не знаю, что ответить.',
                'Давай поговорим о чём-то другом?',
                'Я не уверен в ответе, но могу рассказать анекдот.'
            ]);
        }

        function randomChoice(arr) {
            return arr[Math.floor(Math.random() * arr.length)];
        }

        function escapeHTML(str) {
            return str.replace(/[&<>"]/g, function(m) {
                if (m === '&') return '&amp;';
                if (m === '<') return '&lt;';
                if (m === '>') return '&gt;';
                if (m === '"') return '&quot;';
                return m;
            });
        }

        // ================== НОВОСТИ ==================
        const newsModal = document.getElementById('newsModal');
        const newsContent = document.getElementById('newsContent');

        async function openNews() {
            newsModal.classList.add('active');
            updateAchievement('news', true);
            newsContent.innerHTML = '<p>Загрузка новостей...</p>';
            
            const rssUrls = [
                'https://lenta.ru/rss',
                'https://www.vedomosti.ru/rss/news',
                'https://rss.ria.ru/export/rss2/archive/index.xml'
            ];
            
            let success = false;
            for (const url of rssUrls) {
                try {
                    const response = await fetch(`https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(url)}`);
                    const data = await response.json();
                    if (data.items && data.items.length > 0) {
                        let html = '<ul class="news-list">';
                        data.items.slice(0, 10).forEach(item => {
                            const date = new Date(item.pubDate).toLocaleDateString('ru-RU');
                            html += `
                                <li class="news-item">
                                    <a href="${item.link}" target="_blank" class="news-title">${item.title}</a>
                                    <div class="news-description">${item.description || ''}</div>
                                    <div class="news-date">${date}</div>
                                </li>
                            `;
                        });
                        html += '</ul>';
                        newsContent.innerHTML = html;
                        success = true;
                        break;
                    }
                } catch (e) {
                    console.warn('Ошибка загрузки RSS:', url, e);
                }
            }
            
            if (!success) {
                newsContent.innerHTML = `
                    <p>Не удалось загрузить свежие новости. Проверьте подключение к интернету или попробуйте позже.</p>
                    <button class="game-btn" onclick="openNews()">Повторить</button>
                    <div style="margin-top:20px;">
                        <p>Примеры новостей (демо):</p>
                        <ul class="news-list">
                            <li class="news-item"><span class="news-title">Цифровые технологии в играх</span><div class="news-description">R_52_X представляет обновление платформы</div><div class="news-date">${new Date().toLocaleDateString('ru-RU')}</div></li>
                            <li class="news-item"><span class="news-title">Киберспортивный турнир</span><div class="news-description">В Москве прошёл турнир по новым дисциплинам</div><div class="news-date">${new Date().toLocaleDateString('ru-RU')}</div></li>
                            <li class="news-item"><span class="news-title">Разработка игр</span><div class="news-description">Студия R_52_X работает над секретным проектом</div><div class="news-date">${new Date().toLocaleDateString('ru-RU')}</div></li>
                        </ul>
                    </div>
                `;
            }
        }

        function closeNews() {
            newsModal.classList.remove('active');
        }

        // Инициализация при загрузке
        window.addEventListener('load', () => {
            checkAllGamesProgress();
        });

        // Плавная прокрутка
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                const href = this.getAttribute('href');
                if (href === '#') return;
                const target = document.querySelector(href);
                if (target) {
                    e.preventDefault();
                    target.scrollIntoView({ behavior: 'smooth' });
                }
            });
        });
    </script>
</body>
</html>
