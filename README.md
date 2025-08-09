# tic-tac-toe1
tic-tac-toe of KefiriyiTü
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Крестики-нолики от KefiriyiTü</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            /* Цвета для светлой темы */
            --light-primary: #ffffff;
            --light-secondary: #f5f5f5;
            --light-accent: #ff6b6b;
            --light-accent2: #4ecdc4;
            --light-text: #333333;
            --light-border: #e0e0e0;
            --light-shadow: rgba(0, 0, 0, 0.1);
            --light-bg-gradient: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
            
            /* Цвета для темной темы */
            --dark-primary: #121212;
            --dark-secondary: #1e1e1e;
            --dark-text: #f5f5f5;
            --dark-border: #333333;
            --dark-shadow: rgba(255, 255, 255, 0.05);
            
            /* Общие переменные */
            --transition: all 0.3s ease;
            --border-radius: 12px;
            --box-shadow: 0 4px 20px var(--light-shadow);
            --header-height: 60px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--light-primary);
            color: var(--light-text);
            transition: var(--transition);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        body.dark-theme {
            background-color: var(--dark-primary);
            color: var(--dark-text);
            --box-shadow: 0 4px 20px var(--dark-shadow);
        }

        /* Анимации */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes rainbow {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        @keyframes cellHover {
            from { transform: scale(0.9); opacity: 0.7; }
            to { transform: scale(1); opacity: 1; }
        }

        /* Хедер */
        .header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: var(--header-height);
            background-color: var(--light-secondary);
            box-shadow: var(--box-shadow);
            display: flex;
            justify-content: flex-end;
            align-items: center;
            padding: 0 20px;
            z-index: 1000;
            transition: var(--transition);
        }

        .dark-theme .header {
            background-color: var(--dark-secondary);
            border-bottom: 1px solid var(--dark-border);
        }

        .header-icons {
            display: flex;
            gap: 20px;
        }

        .header-icon {
            font-size: 1.5rem;
            color: var(--light-text);
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: transparent;
        }

        .dark-theme .header-icon {
            color: var(--dark-text);
        }

        .header-icon:hover {
            transform: translateY(-3px);
            color: var(--light-accent);
        }

        .dark-theme .header-icon:hover {
            color: var(--light-accent);
        }

        /* Основной контент */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: calc(var(--header-height) + 20px) 20px 80px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        /* Страница вступления */
        .intro-page {
            text-align: center;
            animation: fadeIn 0.8s ease forwards;
            max-width: 800px;
            padding: 40px;
            border-radius: var(--border-radius);
            background-color: var(--light-secondary);
            box-shadow: var(--box-shadow);
            transition: var(--transition);
        }

        .dark-theme .intro-page {
            background-color: var(--dark-secondary);
        }

        .intro-header {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 30px;
        }

        .kefir-logo {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 20px;
            animation: pulse 2s infinite;
        }

        .kefir-logo i {
            font-size: 3rem;
            color: white;
        }

        .intro-title {
            font-size: 3rem;
            font-weight: 700;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 10px;
        }

        .dark-theme .intro-title {
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .intro-subtitle {
            font-size: 1.2rem;
            margin-bottom: 30px;
            line-height: 1.6;
            color: var(--light-text);
            max-width: 600px;
            margin: 0 auto 30px;
        }

        .dark-theme .intro-subtitle {
            color: var(--dark-text);
        }

        .play-button {
            padding: 15px 50px;
            font-size: 1.2rem;
            font-weight: 600;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
            margin-top: 20px;
            animation: pulse 2s infinite;
        }

        .play-button:hover {
            transform: translateY(-5px);
            box-shadow: 0 7px 20px rgba(255, 107, 107, 0.4);
        }

        .copyright {
            position: absolute;
            bottom: 20px;
            font-size: 0.9rem;
            color: var(--light-text);
            opacity: 0.7;
        }

        .dark-theme .copyright {
            color: var(--dark-text);
        }

        /* Страница выбора режима */
        .mode-page {
            display: none;
            text-align: center;
            width: 100%;
            max-width: 800px;
            animation: fadeIn 0.8s ease forwards;
        }

        .page-title {
            font-size: 2.5rem;
            margin-bottom: 40px;
            color: var(--light-text);
            position: relative;
            display: inline-block;
        }

        .dark-theme .page-title {
            color: var(--dark-text);
        }

        .page-title::after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 80px;
            height: 4px;
            background: linear-gradient(to right, #ff6b6b, #4ecdc4);
            border-radius: 2px;
        }

        .mode-selection {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }

        .mode-option {
            background-color: var(--light-secondary);
            padding: 30px;
            border-radius: var(--border-radius);
            width: 280px;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: var(--box-shadow);
            border: 2px solid transparent;
        }

        .dark-theme .mode-option {
            background-color: var(--dark-secondary);
        }

        .mode-option:hover {
            transform: translateY(-10px);
        }

        .mode-option.selected {
            border-color: var(--light-accent);
            transform: translateY(-10px);
            box-shadow: 0 10px 25px rgba(255, 107, 107, 0.2);
        }

        .dark-theme .mode-option.selected {
            border-color: var(--light-accent);
        }

        .mode-icon {
            font-size: 3rem;
            margin-bottom: 20px;
            color: var(--light-accent);
        }

        .mode-title {
            font-size: 1.5rem;
            margin-bottom: 15px;
            color: var(--light-text);
        }

        .dark-theme .mode-title {
            color: var(--dark-text);
        }

        .mode-description {
            font-size: 1rem;
            color: var(--light-text);
            opacity: 0.8;
            line-height: 1.6;
        }

        .dark-theme .mode-description {
            color: var(--dark-text);
        }

        .player-names {
            display: none;
            background-color: var(--light-secondary);
            padding: 30px;
            border-radius: var(--border-radius);
            width: 100%;
            max-width: 500px;
            margin: 0 auto;
            box-shadow: var(--box-shadow);
            transition: var(--transition);
            animation: fadeIn 0.5s ease forwards;
        }

        .dark-theme .player-names {
            background-color: var(--dark-secondary);
        }

        .name-input-group {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin-bottom: 30px;
        }

        .input-row {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .player-label {
            width: 100px;
            text-align: right;
            font-weight: 600;
            color: var(--light-text);
        }

        .dark-theme .player-label {
            color: var(--dark-text);
        }

        .name-input {
            flex: 1;
            padding: 12px 20px;
            border: 2px solid var(--light-border);
            border-radius: 8px;
            font-size: 1rem;
            transition: var(--transition);
            background-color: var(--light-primary);
            color: var(--light-text);
        }

        .dark-theme .name-input {
            background-color: var(--dark-primary);
            border-color: var(--dark-border);
            color: var(--dark-text);
        }

        .name-input:focus {
            border-color: var(--light-accent);
            outline: none;
        }

        .start-game-btn {
            padding: 12px 40px;
            font-size: 1.1rem;
            font-weight: 600;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            color: white;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .start-game-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(255, 107, 107, 0.4);
        }

        .back-button {
            background: none;
            border: none;
            color: var(--light-text);
            cursor: pointer;
            font-size: 1rem;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-top: 30px;
            transition: var(--transition);
            padding: 8px 15px;
            border-radius: 8px;
        }

        .dark-theme .back-button {
            color: var(--dark-text);
        }

        .back-button:hover {
            background-color: rgba(255, 107, 107, 0.1);
        }

        /* Страница игры */
        .game-page {
            display: none;
            width: 100%;
            max-width: 800px;
            animation: fadeIn 0.8s ease forwards;
        }

        .game-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--light-border);
        }

        .dark-theme .game-header {
            border-bottom-color: var(--dark-border);
        }

        .game-title {
            font-size: 2.2rem;
            color: var(--light-text);
        }

        .dark-theme .game-title {
            color: var(--dark-text);
        }

        .turn-indicator {
            font-size: 1.2rem;
            font-weight: 600;
            padding: 8px 20px;
            border-radius: 30px;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            color: white;
            box-shadow: 0 4px 10px rgba(255, 107, 107, 0.3);
            transition: var(--transition);
        }

        .game-board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-gap: 15px;
            max-width: 500px;
            width: 100%;
            margin: 0 auto 40px;
            aspect-ratio: 1/1;
        }

        .cell {
            background-color: var(--light-secondary);
            border-radius: var(--border-radius);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4rem;
            font-weight: bold;
            cursor: pointer;
            transition: var(--transition);
            box-shadow: var(--box-shadow);
            position: relative;
            overflow: hidden;
        }

        .dark-theme .cell {
            background-color: var(--dark-secondary);
        }

        .cell:hover {
            animation: cellHover 0.3s ease forwards;
        }

        .cell.x::before, .cell.x::after {
            content: '';
            position: absolute;
            width: 80%;
            height: 10px;
            background-color: var(--light-accent);
            border-radius: 5px;
        }

        .cell.x::before {
            transform: rotate(45deg);
        }

        .cell.x::after {
            transform: rotate(-45deg);
        }

        .cell.o::before {
            content: '';
            position: absolute;
            width: 70%;
            height: 70%;
            border-radius: 50%;
            border: 10px solid var(--light-accent2);
        }

        .game-controls {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
        }

        .control-btn {
            padding: 12px 30px;
            font-size: 1rem;
            font-weight: 600;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            transition: var(--transition);
        }

        .restart-btn {
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            color: white;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .restart-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 7px 20px rgba(255, 107, 107, 0.4);
        }

        .menu-btn {
            background-color: var(--light-secondary);
            color: var(--light-text);
            border: 2px solid var(--light-border);
        }

        .dark-theme .menu-btn {
            background-color: var(--dark-secondary);
            color: var(--dark-text);
            border-color: var(--dark-border);
        }

        .menu-btn:hover {
            background-color: rgba(255, 107, 107, 0.1);
        }

        /* Модальные окна */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: var(--transition);
        }

        .modal.active {
            opacity: 1;
            visibility: visible;
        }

        .modal-content {
            background-color: var(--light-primary);
            border-radius: var(--border-radius);
            width: 90%;
            max-width: 500px;
            max-height: 90vh;
            overflow-y: auto;
            transform: translateY(-30px);
            transition: var(--transition);
            position: relative;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
        }

        .dark-theme .modal-content {
            background-color: var(--dark-secondary);
        }

        .modal.active .modal-content {
            transform: translateY(0);
        }

        .modal-header {
            padding: 20px;
            border-bottom: 1px solid var(--light-border);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .dark-theme .modal-header {
            border-bottom-color: var(--dark-border);
        }

        .modal-title {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--light-text);
        }

        .dark-theme .modal-title {
            color: var(--dark-text);
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--light-text);
            transition: var(--transition);
        }

        .dark-theme .close-modal {
            color: var(--dark-text);
        }

        .close-modal:hover {
            color: var(--light-accent);
        }

        .modal-body {
            padding: 30px;
        }

        /* Настройки */
        .settings-item {
            margin-bottom: 25px;
        }

        .settings-label {
            display: block;
            margin-bottom: 10px;
            font-weight: 600;
            color: var(--light-text);
        }

        .dark-theme .settings-label {
            color: var(--dark-text);
        }

        .theme-switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 30px;
        }

        .theme-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: var(--transition);
            border-radius: 30px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 22px;
            width: 22px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: var(--transition);
            border-radius: 50%;
        }

        input:checked + .slider {
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
        }

        input:checked + .slider:before {
            transform: translateX(30px);
        }

        .language-selector {
            margin-top: 10px;
        }

        .languages-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 10px;
            margin-top: 15px;
        }

        .language-option {
            padding: 10px;
            border-radius: 8px;
            background-color: var(--light-secondary);
            text-align: center;
            cursor: pointer;
            transition: var(--transition);
            border: 2px solid transparent;
        }

        .dark-theme .language-option {
            background-color: var(--dark-secondary);
        }

        .language-option:hover, .language-option.selected {
            border-color: var(--light-accent);
            transform: translateY(-3px);
        }

        /* Статистика */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-top: 20px;
        }

        .stat-card {
            background-color: var(--light-secondary);
            padding: 20px;
            border-radius: var(--border-radius);
            text-align: center;
            box-shadow: var(--box-shadow);
            transition: var(--transition);
        }

        .dark-theme .stat-card {
            background-color: var(--dark-secondary);
        }

        .stat-value {
            font-size: 2.5rem;
            font-weight: 700;
            margin: 10px 0;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .stat-label {
            font-size: 1rem;
            color: var(--light-text);
            opacity: 0.8;
        }

        .dark-theme .stat-label {
            color: var(--dark-text);
        }

        /* Адаптивность */
        @media (max-width: 768px) {
            .intro-title {
                font-size: 2.2rem;
            }
            
            .kefir-logo {
                width: 80px;
                height: 80px;
            }
            
            .mode-selection {
                flex-direction: column;
                align-items: center;
            }
            
            .game-board {
                max-width: 90vw;
            }
            
            .cell {
                font-size: 3rem;
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
            }
        }

        @media (max-width: 480px) {
            .intro-title {
                font-size: 1.8rem;
            }
            
            .page-title {
                font-size: 2rem;
            }
            
            .game-title {
                font-size: 1.8rem;
            }
            
            .turn-indicator {
                font-size: 1rem;
                padding: 6px 15px;
            }
            
            .input-row {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .player-label {
                text-align: left;
            }
        }

        /* Светлая тема с цветами */
        .light-theme-colorful {
            --light-primary: #f0f8ff;
            --light-secondary: #ffffff;
            --light-accent: #ff6b6b;
            --light-accent2: #4ecdc4;
            --light-text: #2c3e50;
            --light-border: #e0e0e0;
            --light-shadow: rgba(0, 0, 0, 0.1);
            --light-bg-gradient: linear-gradient(135deg, #ff9a9e 0%, #fad0c4 100%);
        }

        .light-theme-colorful .intro-page,
        .light-theme-colorful .mode-option,
        .light-theme-colorful .player-names,
        .light-theme-colorful .stat-card,
        .light-theme-colorful .cell {
            background: var(--light-bg-gradient);
            border: 2px solid rgba(255, 255, 255, 0.3);
        }

        .light-theme-colorful .header {
            background: linear-gradient(90deg, #ff6b6b, #4ecdc4);
        }

        .light-theme-colorful .header-icon {
            color: white;
        }

        .light-theme-colorful .header-icon:hover {
            color: #2c3e50;
        }

        .light-theme-colorful .page-title,
        .light-theme-colorful .game-title,
        .light-theme-colorful .mode-title,
        .light-theme-colorful .player-label {
            color: #2c3e50;
        }

        .light-theme-colorful .intro-subtitle,
        .light-theme-colorful .mode-description {
            color: #34495e;
        }

        .light-theme-colorful .copyright {
            color: #2c3e50;
        }

        .light-theme-colorful .game-header {
            border-bottom: 2px solid rgba(255, 255, 255, 0.3);
        }

        .light-theme-colorful .back-button,
        .light-theme-colorful .menu-btn {
            background: rgba(255, 255, 255, 0.5);
        }

        .light-theme-colorful .back-button:hover,
        .light-theme-colorful .menu-btn:hover {
            background: rgba(255, 255, 255, 0.8);
        }

        .rainbow-text {
            background: linear-gradient(90deg, #ff6b6b, #ffd166, #06d6a0, #118ab2, #073b4c);
            background-size: 300% 300%;
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            animation: rainbow 8s ease infinite;
        }
    </style>
</head>
<body>
    <!-- Верхняя панель с иконками -->
    <header class="header">
        <div class="header-icons">
            <div class="header-icon" id="telegram-btn">
                <i class="fab fa-telegram"></i>
            </div>
            <div class="header-icon" id="settings-btn">
                <i class="fas fa-cog"></i>
            </div>
            <div class="header-icon" id="stats-btn">
                <i class="fas fa-chart-bar"></i>
            </div>
        </div>
    </header>

    <!-- Основной контейнер -->
    <div class="container">
        <!-- Вступительная страница -->
        <div class="intro-page" id="intro-page">
            <div class="intro-header">
                <div class="kefir-logo">
                    <i class="fas fa-crown"></i>
                </div>
                <h1 class="intro-title">KefiriyiTü</h1>
            </div>
            <p class="intro-subtitle" data-lang="intro">Kefir - талантливый программист с уникальным видением цифрового мира. Его проекты сочетают в себе элегантность, функциональность и инновации. Каждая строка кода — это шаг к совершенству, каждая программа — произведение искусства.</p>
            <button class="play-button" id="play-btn" data-lang="play">Играть</button>
            <div class="copyright">© 2025 KefiriyiTü Games. Все права защищены.</div>
        </div>

        <!-- Страница выбора режима -->
        <div class="mode-page" id="mode-page">
            <h2 class="page-title" data-lang="game-mode">Режим игры</h2>
            <div class="mode-selection">
                <div class="mode-option" data-mode="bot">
                    <div class="mode-icon">
                        <i class="fas fa-robot"></i>
                    </div>
                    <h3 class="mode-title" data-lang="vs-bot">Против бота</h3>
                    <p class="mode-description" data-lang="bot-desc">Сразитесь с нашим искусственным интеллектом. Бот использует продвинутые алгоритмы для принятия решений.</p>
                </div>
                <div class="mode-option" data-mode="friend">
                    <div class="mode-icon">
                        <i class="fas fa-user-friends"></i>
                    </div>
                    <h3 class="mode-title" data-lang="vs-friend">Против друга</h3>
                    <p class="mode-description" data-lang="friend-desc">Пригласите друга и сразитесь друг с другом на одном устройстве. Идеально для вечеринок!</p>
                </div>
            </div>
            
            <div class="player-names" id="player-names">
                <div class="name-input-group">
                    <div class="input-row">
                        <span class="player-label" data-lang="player1">Игрок 1 (X):</span>
                        <input type="text" class="name-input" id="player1-name" value="Первый" maxlength="15">
                    </div>
                    <div class="input-row">
                        <span class="player-label" data-lang="player2">Игрок 2 (O):</span>
                        <input type="text" class="name-input" id="player2-name" value="Второй" maxlength="15">
                    </div>
                </div>
            </div>
            
            <!-- Вынесенная кнопка начала игры -->
            <button class="start-game-btn" id="start-game-btn" data-lang="start-game" style="display: none;">Начать игру</button>
            
            <button class="back-button" id="mode-back-btn">
                <i class="fas fa-arrow-left"></i>
                <span data-lang="back">Назад</span>
            </button>
        </div>

        <!-- Страница игры -->
        <div class="game-page" id="game-page">
            <div class="game-header">
                <h2 class="game-title" data-lang="tic-tac-toe">Крестики-нолики</h2>
                <div class="turn-indicator" id="turn-indicator">Твой ход</div>
            </div>
            
            <div class="game-board" id="game-board">
                <div class="cell" data-index="0"></div>
                <div class="cell" data-index="1"></div>
                <div class="cell" data-index="2"></div>
                <div class="cell" data-index="3"></div>
                <div class="cell" data-index="4"></div>
                <div class="cell" data-index="5"></div>
                <div class="cell" data-index="6"></div>
                <div class="cell" data-index="7"></div>
                <div class="cell" data-index="8"></div>
            </div>
            
            <div class="game-controls">
                <button class="control-btn restart-btn" id="restart-btn" data-lang="restart">Новая игра</button>
                <button class="control-btn menu-btn" id="game-menu-btn" data-lang="to-menu">В меню</button>
            </div>
        </div>
    </div>

    <!-- Модальное окно настроек -->
    <div class="modal" id="settings-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title" data-lang="settings">Настройки</h3>
                <button class="close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <div class="settings-item">
                    <span class="settings-label" data-lang="theme">Тема:</span>
                    <label class="theme-switch">
                        <input type="checkbox" id="theme-toggle">
                        <span class="slider"></span>
                    </label>
                    <span id="theme-status" data-lang="light">Светлая</span>
                </div>
                
                <div class="settings-item">
                    <span class="settings-label" data-lang="language">Язык:</span>
                    <div class="language-selector">
                        <div class="languages-grid" id="languages-grid">
                            <!-- Языки будут добавлены через JS -->
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Модальное окно статистики -->
    <div class="modal" id="stats-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title" data-lang="statistics">Статистика</h3>
                <button class="close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <div class="stats-grid" id="stats-grid">
                    <!-- Статистика будет добавлена через JS -->
                </div>
            </div>
        </div>
    </div>

    <!-- Модальное окно результатов игры -->
    <div class="modal" id="result-modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3 class="modal-title" id="result-title">Результат игры</h3>
                <button class="close-modal">&times;</button>
            </div>
            <div class="modal-body">
                <p id="result-message" style="text-align: center; font-size: 1.2rem; margin: 20px 0;"></p>
                <div style="text-align: center; margin-top: 30px;">
                    <button class="control-btn restart-btn" id="modal-restart-btn" style="margin-right: 10px;" data-lang="play-again">Играть снова</button>
                    <button class="control-btn menu-btn" id="modal-menu-btn" data-lang="to-menu">В меню</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Состояние приложения
        const state = {
            currentPage: 'intro',
            gameMode: null,
            currentPlayer: 'X',
            gameBoard: Array(9).fill(''),
            gameActive: true,
            playerNames: {
                player1: 'Первый',
                player2: 'Второй'
            },
            botStrategy: 'random',
            botMovesCount: 0,
            stats: {
                gamesPlayed: 0,
                winsX: 0,
                winsO: 0,
                draws: 0
            },
            theme: 'dark',
            language: 'ru'
        };

        // Поддерживаемые языки
        const languages = {
            ru: { name: "Русский", flag: "🇷🇺" },
            en: { name: "English", flag: "🇺🇸" },
            es: { name: "Español", flag: "🇪🇸" },
            fr: { name: "Français", flag: "🇫🇷" },
            de: { name: "Deutsch", flag: "🇩🇪" },
            zh: { name: "中文", flag: "🇨🇳" },
            ja: { name: "日本語", flag: "🇯🇵" },
            ko: { name: "한국어", flag: "🇰🇷" },
            ar: { name: "العربية", flag: "🇸🇦" },
            pt: { name: "Português", flag: "🇵🇹" },
            it: { name: "Italiano", flag: "🇮🇹" },
            nl: { name: "Nederlands", flag: "🇳🇱" },
            tr: { name: "Türkçe", flag: "🇹🇷" },
            pl: { name: "Polski", flag: "🇵🇱" },
            uk: { name: "Українська", flag: "🇺🇦" },
            hi: { name: "हिन्दी", flag: "🇮🇳" },
            id: { name: "Bahasa Indonesia", flag: "🇮🇩" },
            vi: { name: "Tiếng Việt", flag: "🇻🇳" },
            th: { name: "ไทย", flag: "🇹🇭" },
            sv: { name: "Svenska", flag: "🇸🇪" },
            no: { name: "Norsk", flag: "🇳🇴" },
            da: { name: "Dansk", flag: "🇩🇰" },
            fi: { name: "Suomi", flag: "🇫🇮" },
            el: { name: "Ελληνικά", flag: "🇬🇷" },
            he: { name: "עברית", flag: "🇮🇱" },
            hu: { name: "Magyar", flag: "🇭🇺" },
            cs: { name: "Čeština", flag: "🇨🇿" },
            ro: { name: "Română", flag: "🇷🇴" },
            bg: { name: "Български", flag: "🇧🇬" },
            sr: { name: "Српски", flag: "🇷🇸" }
        };

        // Локализация
        const translations = {
            // Русский
            ru: {
                "intro": "Kefir - талантливый программист с уникальным видением цифрового мира. Его проекты сочетают в себе элегантность, функциональность и инновации. Каждая строка кода — это шаг к совершенству, каждая программа — произведение искусства.",
                "play": "Играть",
                "game-mode": "Режим игры",
                "vs-bot": "Против бота",
                "bot-desc": "Сразитесь с нашим искусственным интеллектом. Бот использует продвинутые алгоритмы для принятия решений.",
                "vs-friend": "Против друга",
                "friend-desc": "Пригласите друга и сразитесь друг с другом на одном устройстве. Идеально для вечеринок!",
                "player1": "Игрок 1 (X):",
                "player2": "Игрок 2 (O):",
                "start-game": "Начать игру",
                "back": "Назад",
                "tic-tac-toe": "Крестики-нолики",
                "restart": "Новая игра",
                "to-menu": "В меню",
                "settings": "Настройки",
                "theme": "Тема:",
                "light": "Светлая",
                "dark": "Тёмная",
                "language": "Язык:",
                "statistics": "Статистика",
                "games-played": "Игр сыграно",
                "wins-x": "Побед X",
                "wins-o": "Побед O",
                "draws": "Ничьих",
                "your-turn": "Твой ход",
                "bot-turn": "Ход бота",
                "player-turn": "Ход игрока",
                "win-x": "Победил X!",
                "win-o": "Победил O!",
                "draw": "Ничья!",
                "play-again": "Играть снова"
            },
            // Английский
            en: {
                "intro": "Kefir is a talented programmer with a unique vision of the digital world. His projects combine elegance, functionality, and innovation. Each line of code is a step towards perfection, each program is a work of art.",
                "play": "Play",
                "game-mode": "Game Mode",
                "vs-bot": "VS Bot",
                "bot-desc": "Challenge our artificial intelligence. The bot uses advanced algorithms for decision making.",
                "vs-friend": "VS Friend",
                "friend-desc": "Invite a friend and compete on the same device. Perfect for parties!",
                "player1": "Player 1 (X):",
                "player2": "Player 2 (O):",
                "start-game": "Start Game",
                "back": "Back",
                "tic-tac-toe": "Tic Tac Toe",
                "restart": "New Game",
                "to-menu": "To Menu",
                "settings": "Settings",
                "theme": "Theme:",
                "light": "Light",
                "dark": "Dark",
                "language": "Language:",
                "statistics": "Statistics",
                "games-played": "Games Played",
                "wins-x": "X Wins",
                "wins-o": "O Wins",
                "draws": "Draws",
                "your-turn": "Your Turn",
                "bot-turn": "Bot's Turn",
                "player-turn": "Player's Turn",
                "win-x": "X Wins!",
                "win-o": "O Wins!",
                "draw": "It's a Draw!",
                "play-again": "Play Again"
            },
            // Испанский
            es: {
                "intro": "Kefir es un programador talentoso con una visión única del mundo digital. Sus proyectos combinan elegancia, funcionalidad e innovación. Cada línea de código es un paso hacia la perfección, cada programa es una obra de arte.",
                "play": "Jugar",
                "game-mode": "Modo de Juego",
                "vs-bot": "Contra Bot",
                "bot-desc": "Desafía a nuestra inteligencia artificial. El bot utiliza algoritmos avanzados para la toma de decisiones.",
                "vs-friend": "Contra Amigo",
                "friend-desc": "Invita a un amigo y compite en el mismo dispositivo. ¡Perfecto para fiestas!",
                "player1": "Jugador 1 (X):",
                "player2": "Jugador 2 (O):",
                "start-game": "Comenzar Juego",
                "back": "Atrás",
                "tic-tac-toe": "Tres en Raya",
                "restart": "Nuevo Juego",
                "to-menu": "Al Menú",
                "settings": "Ajustes",
                "theme": "Tema:",
                "light": "Claro",
                "dark": "Oscuro",
                "language": "Idioma:",
                "statistics": "Estadísticas",
                "games-played": "Juegos Jugados",
                "wins-x": "Victorias X",
                "wins-o": "Victorias O",
                "draws": "Empates",
                "your-turn": "Tu Turno",
                "bot-turn": "Turno del Bot",
                "player-turn": "Turno del Jugador",
                "win-x": "¡X Gana!",
                "win-o": "¡O Gana!",
                "draw": "¡Empate!",
                "play-again": "Jugar de Nuevo"
            },
            // Французский
            fr: {
                "intro": "Kefir est un programmeur talentueux avec une vision unique du monde numérique. Ses projets combinent élégance, fonctionnalité et innovation. Chaque ligne de code est un pas vers la perfection, chaque programme est une œuvre d'art.",
                "play": "Jouer",
                "game-mode": "Mode de Jeu",
                "vs-bot": "Contre le Bot",
                "bot-desc": "Défiez notre intelligence artificielle. Le bot utilise des algorithmes avancés pour prendre des décisions.",
                "vs-friend": "Contre un Ami",
                "friend-desc": "Invitez un ami et affrontez-vous sur le même appareil. Parfait pour les fêtes !",
                "player1": "Joueur 1 (X):",
                "player2": "Joueur 2 (O):",
                "start-game": "Commencer le Jeu",
                "back": "Retour",
                "tic-tac-toe": "Morpion",
                "restart": "Nouveau Jeu",
                "to-menu": "Au Menu",
                "settings": "Paramètres",
                "theme": "Thème:",
                "light": "Clair",
                "dark": "Sombre",
                "language": "Langue:",
                "statistics": "Statistiques",
                "games-played": "Parties Jouées",
                "wins-x": "Victoires X",
                "wins-o": "Victoires O",
                "draws": "Égalités",
                "your-turn": "Votre Tour",
                "bot-turn": "Tour du Bot",
                "player-turn": "Tour du Joueur",
                "win-x": "X Gagne !",
                "win-o": "O Gagne !",
                "draw": "Égalité !",
                "play-again": "Rejouer"
            },
            // Немецкий
            de: {
                "intro": "Kefir ist ein talentierter Programmierer mit einer einzigartigen Vision der digitalen Welt. Seine Projekte vereinen Eleganz, Funktionalität und Innovation. Jede Codezeile ist ein Schritt zur Perfektion, jedes Programm ist ein Kunstwerk.",
                "play": "Spielen",
                "game-mode": "Spielmodus",
                "vs-bot": "Gegen Bot",
                "bot-desc": "Fordern Sie unsere künstliche Intelligenz heraus. Der Bot verwendet fortschrittliche Algorithmen zur Entscheidungsfindung.",
                "vs-friend": "Gegen Freund",
                "friend-desc": "Laden Sie einen Freund ein und spielen Sie auf demselben Gerät. Perfekt für Partys!",
                "player1": "Spieler 1 (X):",
                "player2": "Spieler 2 (O):",
                "start-game": "Spiel Starten",
                "back": "Zurück",
                "tic-tac-toe": "Tic Tac Toe",
                "restart": "Neues Spiel",
                "to-menu": "Zum Menü",
                "settings": "Einstellungen",
                "theme": "Thema:",
                "light": "Hell",
                "dark": "Dunkel",
                "language": "Sprache:",
                "statistics": "Statistiken",
                "games-played": "Gespielte Spiele",
                "wins-x": "X-Siege",
                "wins-o": "O-Siege",
                "draws": "Unentschieden",
                "your-turn": "Du bist dran",
                "bot-turn": "Bot ist dran",
                "player-turn": "Spieler ist dran",
                "win-x": "X gewinnt!",
                "win-o": "O gewinnt!",
                "draw": "Unentschieden!",
                "play-again": "Nochmal spielen"
            },
            // Остальные языки
            zh: {
                "intro": "Kefir是一位才华横溢的程序员，对数字世界有着独特的愿景。他的项目结合了优雅、功能和创新。每一行代码都是迈向完美的步伐，每个程序都是一件艺术品。",
                "play": "玩",
                "game-mode": "游戏模式",
                "vs-bot": "对战机器人",
                "bot-desc": "挑战我们的人工智能。机器人使用先进的算法进行决策。",
                "vs-friend": "对战朋友",
                "friend-desc": "邀请朋友在同一设备上对战。非常适合聚会！",
                "player1": "玩家1 (X):",
                "player2": "玩家2 (O):",
                "start-game": "开始游戏",
                "back": "返回",
                "tic-tac-toe": "井字棋",
                "restart": "新游戏",
                "to-menu": "返回菜单",
                "settings": "设置",
                "theme": "主题:",
                "light": "明亮",
                "dark": "暗黑",
                "language": "语言:",
                "statistics": "统计",
                "games-played": "已玩游戏",
                "wins-x": "X胜利",
                "wins-o": "O胜利",
                "draws": "平局",
                "your-turn": "你的回合",
                "bot-turn": "机器人回合",
                "player-turn": "玩家回合",
                "win-x": "X胜利！",
                "win-o": "O胜利！",
                "draw": "平局！",
                "play-again": "再玩一次"
            },
            ja: {
                "intro": "Kefirはデジタル世界に対する独自のビジョンを持つ才能あるプログラマーです。彼のプロジェクトは優雅さ、機能性、革新性を兼ね備えています。コードの各行は完璧への一歩であり、各プログラムは芸術作品です。",
                "play": "プレイ",
                "game-mode": "ゲームモード",
                "vs-bot": "ボット対戦",
                "bot-desc": "人工知能に挑戦しましょう。ボットは意思決定のために高度なアルゴリズムを使用します。",
                "vs-friend": "フレンド対戦",
                "friend-desc": "友達を招待して同じデバイスで対戦しましょう。パーティーに最適です！",
                "player1": "プレイヤー1 (X):",
                "player2": "プレイヤー2 (O):",
                "start-game": "ゲーム開始",
                "back": "戻る",
                "tic-tac-toe": "三目並べ",
                "restart": "新しいゲーム",
                "to-menu": "メニューへ",
                "settings": "設定",
                "theme": "テーマ:",
                "light": "ライト",
                "dark": "ダーク",
                "language": "言語:",
                "statistics": "統計",
                "games-played": "プレイしたゲーム",
                "wins-x": "Xの勝利",
                "wins-o": "Oの勝利",
                "draws": "引き分け",
                "your-turn": "あなたのターン",
                "bot-turn": "ボットのターン",
                "player-turn": "プレイヤーのターン",
                "win-x": "Xの勝利！",
                "win-o": "Oの勝利！",
                "draw": "引き分け！",
                "play-again": "もう一度遊ぶ"
            },
            ko: {
                "intro": "Kefir는 디지털 세계에 대한 독특한 비전을 가진 재능 있는 프로그래머입니다. 그의 프로젝트는 우아함, 기능성 및 혁신을 결합합니다. 각 코드 줄은 완벽을 향한 한 걸음이며, 각 프로그램은 예술 작품입니다.",
                "play": "플레이",
                "game-mode": "게임 모드",
                "vs-bot": "봇 대전",
                "bot-desc": "우리의 인공 지능에 도전하세요. 봇은 의사 결정을 위해 고급 알고리즘을 사용합니다.",
                "vs-friend": "친구 대전",
                "friend-desc": "친구를 초대하여 같은 기기에서 대전하세요. 파티에 완벽합니다!",
                "player1": "플레이어 1 (X):",
                "player2": "플레이어 2 (O):",
                "start-game": "게임 시작",
                "back": "뒤로",
                "tic-tac-toe": "틱택토",
                "restart": "새 게임",
                "to-menu": "메뉴로",
                "settings": "설정",
                "theme": "테마:",
                "light": "라이트",
                "dark": "다크",
                "language": "언어:",
                "statistics": "통계",
                "games-played": "플레이한 게ーム",
                "wins-x": "X 승리",
                "wins-o": "O 승리",
                "draws": "무승부",
                "your-turn": "당신의 차례",
                "bot-turn": "봇의 차례",
                "player-turn": "플레이어의 차례",
                "win-x": "X 승리!",
                "win-o": "O 승리!",
                "draw": "무승부!",
                "play-again": "다시 플레이"
            },
            ar: {
                "intro": "كفير هو مبرمج موهوب برؤية فريدة للعالم الرقمي. تجمع مشاريعه بين الأناقة والوظائف والابتكار. كل سطر من التعليمات البرمجية هو خطوة نحو الكمال، وكل برنامج هو عمل فني.",
                "play": "لعب",
                "game-mode": "وضع اللعبة",
                "vs-bot": "ضد البوت",
                "bot-desc": "تحدى الذكاء الاصطناعي الخاص بنا. يستخدم البوت خوارزميات متقدمة لاتخاذ القرارات.",
                "vs-friend": "ضد صديق",
                "friend-desc": "ادعُ صديقًا وتنافس على نفس الجهاز. مثالي للحفلات!",
                "player1": "اللاعب 1 (X):",
                "player2": "اللاعب 2 (O):",
                "start-game": "بدء اللعبة",
                "back": "عودة",
                "tic-tac-toe": "تيك تاك تو",
                "restart": "لعبة جديدة",
                "to-menu": "إلى القائمة",
                "settings": "الإعدادات",
                "theme": "السمة:",
                "light": "فاتح",
                "dark": "داكن",
                "language": "اللغة:",
                "statistics": "الإحصائيات",
                "games-played": "الألعاب الملعوبة",
                "wins-x": "انتصارات X",
                "wins-o": "انتصارات O",
                "draws": "التعادل",
                "your-turn": "دورك",
                "bot-turn": "دور البوت",
                "player-turn": "دور اللاعب",
                "win-x": "فاز X!",
                "win-o": "فاز O!",
                "draw": "تعادل!",
                "play-again": "العب مرة أخرى"
            },
            // Остальные языки заполнены английским по умолчанию
        };

        // Заполняем отсутствующие переводы английскими версиями
        for (const lang of Object.keys(languages)) {
            if (!translations[lang]) {
                translations[lang] = translations['en'];
            }
        }

        // DOM элементы
        const elements = {
            // Страницы
            introPage: document.getElementById('intro-page'),
            modePage: document.getElementById('mode-page'),
            gamePage: document.getElementById('game-page'),
            playerNames: document.getElementById('player-names'),
            
            // Кнопки
            playBtn: document.getElementById('play-btn'),
            modeOptions: document.querySelectorAll('.mode-option'),
            startGameBtn: document.getElementById('start-game-btn'),
            modeBackBtn: document.getElementById('mode-back-btn'),
            restartBtn: document.getElementById('restart-btn'),
            gameMenuBtn: document.getElementById('game-menu-btn'),
            modalRestartBtn: document.getElementById('modal-restart-btn'),
            modalMenuBtn: document.getElementById('modal-menu-btn'),
            
            // Игровое поле
            gameBoard: document.getElementById('game-board'),
            cells: document.querySelectorAll('.cell'),
            turnIndicator: document.getElementById('turn-indicator'),
            
            // Настройки
            themeToggle: document.getElementById('theme-toggle'),
            themeStatus: document.getElementById('theme-status'),
            languagesGrid: document.getElementById('languages-grid'),
            
            // Модальные окна
            settingsModal: document.getElementById('settings-modal'),
            statsModal: document.getElementById('stats-modal'),
            resultModal: document.getElementById('result-modal'),
            closeModals: document.querySelectorAll('.close-modal'),
            telegramBtn: document.getElementById('telegram-btn'),
            settingsBtn: document.getElementById('settings-btn'),
            statsBtn: document.getElementById('stats-btn'),
            
            // Статистика
            statsGrid: document.getElementById('stats-grid'),
            
            // Имена игроков
            player1Name: document.getElementById('player1-name'),
            player2Name: document.getElementById('player2-name'),
            
            // Результаты
            resultTitle: document.getElementById('result-title'),
            resultMessage: document.getElementById('result-message')
        };

        // Инициализация приложения
        function initApp() {
            // Загрузка состояния из localStorage
            loadState();
            
            // Установка темы
            setTheme(state.theme);
            
            // Установка языка
            setLanguage(state.language);
            
            // Генерация языков
            generateLanguages();
            
            // Обновление статистики
            updateStats();
            
            // Назначение обработчиков событий
            setupEventListeners();
        }

        // Назначение обработчиков событий
        function setupEventListeners() {
            // Навигация
            elements.playBtn.addEventListener('click', () => showPage('mode'));
            elements.modeBackBtn.addEventListener('click', () => showPage('intro'));
            elements.gameMenuBtn.addEventListener('click', () => showPage('mode'));
            elements.modalMenuBtn.addEventListener('click', () => {
                elements.resultModal.classList.remove('active');
                showPage('mode');
            });
            
            // Выбор режима игры
            elements.modeOptions.forEach(option => {
                option.addEventListener('click', () => {
                    // Снять выделение со всех опций
                    elements.modeOptions.forEach(opt => opt.classList.remove('selected'));
                    // Выделить выбранную опцию
                    option.classList.add('selected');
                    // Сохранить выбранный режим
                    state.gameMode = option.dataset.mode;
                    
                    // Показать кнопку "Начать игру"
                    elements.startGameBtn.style.display = 'block';
                    
                    // Показать поля для ввода имен, если выбран режим с другом
                    if (state.gameMode === 'friend') {
                        elements.playerNames.style.display = 'block';
                    } else {
                        elements.playerNames.style.display = 'none';
                    }
                });
            });
            
            // Кнопка начала игры
            elements.startGameBtn.addEventListener('click', startGame);
            elements.modalRestartBtn.addEventListener('click', startGame);
            elements.restartBtn.addEventListener('click', startGame);
            
            // Ячейки игрового поля
            elements.cells.forEach(cell => {
                cell.addEventListener('click', () => handleCellClick(cell));
            });
            
            // Сохранение имен игроков
            elements.player1Name.addEventListener('change', updatePlayerNames);
            elements.player2Name.addEventListener('change', updatePlayerNames);
            
            // Переключение темы
            elements.themeToggle.addEventListener('change', toggleTheme);
            
            // Модальные окна
            elements.telegramBtn.addEventListener('click', () => {
                window.open('https://t.me/historicalpubertat', '_blank');
            });
            
            elements.settingsBtn.addEventListener('click', () => {
                elements.settingsModal.classList.add('active');
            });
            
            elements.statsBtn.addEventListener('click', () => {
                elements.statsModal.classList.add('active');
            });
            
            elements.closeModals.forEach(btn => {
                btn.addEventListener('click', () => {
                    document.querySelectorAll('.modal').forEach(modal => {
                        modal.classList.remove('active');
                    });
                });
            });
            
            // Закрытие модальных окон при клике вне контента
            document.querySelectorAll('.modal').forEach(modal => {
                modal.addEventListener('click', (e) => {
                    if (e.target === modal) {
                        modal.classList.remove('active');
                    }
                });
            });
        }

        // Показать страницу
        function showPage(page) {
            // Скрыть все страницы
            elements.introPage.style.display = 'none';
            elements.modePage.style.display = 'none';
            elements.gamePage.style.display = 'none';
            
            // Скрыть кнопку "Начать игру" при переходе на страницу
            elements.startGameBtn.style.display = 'none';
            elements.playerNames.style.display = 'none';
            
            // Показать нужную страницу
            if (page === 'intro') {
                elements.introPage.style.display = 'block';
                state.currentPage = 'intro';
            } else if (page === 'mode') {
                elements.modePage.style.display = 'block';
                state.currentPage = 'mode';
                // Сбросить выбор режима
                elements.modeOptions.forEach(opt => opt.classList.remove('selected'));
                state.gameMode = null;
            } else if (page === 'game') {
                elements.gamePage.style.display = 'block';
                state.currentPage = 'game';
            }
        }

        // Обновить имена игроков
        function updatePlayerNames() {
            state.playerNames.player1 = elements.player1Name.value || 'Первый';
            state.playerNames.player2 = elements.player2Name.value || 'Второй';
        }

        // Начать игру
        function startGame() {
            // Скрыть модальное окно результатов, если оно открыто
            elements.resultModal.classList.remove('active');
            
            // Сбросить игровое поле
            resetGame();
            
            // Показать страницу игры
            showPage('game');
            
            // Обновить индикатор хода
            updateTurnIndicator();
            
            // Если игра с ботом и бот ходит первым
            if (state.gameMode === 'bot' && state.currentPlayer === 'O') {
                setTimeout(makeBotMove, 800);
            }
        }

        // Сбросить игру
        function resetGame() {
            state.gameBoard = Array(9).fill('');
            state.gameActive = true;
            state.currentPlayer = 'X';
            state.botMovesCount = 0;
            
            // Очистить игровое поле
            elements.cells.forEach(cell => {
                cell.classList.remove('x', 'o');
            });
        }

        // Обработка клика по ячейке
        function handleCellClick(cell) {
            if (!state.gameActive) return;
            
            const index = parseInt(cell.dataset.index);
            
            // Если ячейка уже занята, ничего не делать
            if (state.gameBoard[index] !== '') return;
            
            // Сделать ход
            makeMove(index, state.currentPlayer);
            
            // Проверить результат игры
            const result = checkGameResult();
            
            if (result) {
                // Игра закончена
                handleGameEnd(result);
            } else if (state.gameMode === 'bot') {
                // Ход бота
                setTimeout(makeBotMove, 800);
            }
        }

        // Сделать ход
        function makeMove(index, player) {
            // Обновить состояние игры
            state.gameBoard[index] = player;
            
            // Обновить отображение
            const cell = elements.cells[index];
            cell.classList.add(player.toLowerCase());
            
            // Сменить игрока
            state.currentPlayer = player === 'X' ? 'O' : 'X';
            
            // Обновить индикатор хода
            updateTurnIndicator();
        }

        // Стратегии бота
        function findRandomMove() {
            const emptyCells = state.gameBoard
                .map((cell, index) => cell === '' ? index : -1)
                .filter(index => index !== -1);
            if (emptyCells.length > 0) {
                return emptyCells[Math.floor(Math.random() * emptyCells.length)];
            }
            return -1;
        }

        function findWinningMove(player) {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Горизонтали
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Вертикали
                [0, 4, 8], [2, 4, 6]             // Диагонали
            ];
            
            for (const pattern of winPatterns) {
                const [a, b, c] = pattern;
                
                // Если два поля заняты игроком, а третье пустое
                if (
                    state.gameBoard[a] === player && 
                    state.gameBoard[b] === player && 
                    state.gameBoard[c] === ''
                ) {
                    return c;
                }
                
                if (
                    state.gameBoard[a] === player && 
                    state.gameBoard[c] === player && 
                    state.gameBoard[b] === ''
                ) {
                    return b;
                }
                
                if (
                    state.gameBoard[b] === player && 
                    state.gameBoard[c] === player && 
                    state.gameBoard[a] === ''
                ) {
                    return a;
                }
            }
            
            return -1;
        }

        function aggressiveStrategy() {
            // Попытаться выиграть
            const winMove = findWinningMove('O');
            if (winMove !== -1) return winMove;
            
            // Попытаться заблокировать игрока
            const blockMove = findWinningMove('X');
            if (blockMove !== -1) return blockMove;
            
            // Центр
            if (state.gameBoard[4] === '') return 4;
            
            // Случайный ход
            return findRandomMove();
        }

        function defensiveStrategy() {
            // Попытаться заблокировать игрока
            const blockMove = findWinningMove('X');
            if (blockMove !== -1) return blockMove;
            
            // Попытаться выиграть
            const winMove = findWinningMove('O');
            if (winMove !== -1) return winMove;
            
            // Центр
            if (state.gameBoard[4] === '') return 4;
            
            // Случайный ход
            return findRandomMove();
        }

        function centerStrategy() {
            // Центр
            if (state.gameBoard[4] === '') return 4;
            
            // Попытаться выиграть
            const winMove = findWinningMove('O');
            if (winMove !== -1) return winMove;
            
            // Попытаться заблокировать игрока
            const blockMove = findWinningMove('X');
            if (blockMove !== -1) return blockMove;
            
            // Случайный ход
            return findRandomMove();
        }

        function cornerStrategy() {
            // Углы
            const corners = [0, 2, 6, 8];
            const availableCorners = corners.filter(index => state.gameBoard[index] === '');
            if (availableCorners.length > 0) {
                return availableCorners[Math.floor(Math.random() * availableCorners.length)];
            }
            
            // Центр
            if (state.gameBoard[4] === '') return 4;
            
            // Попытаться выиграть
            const winMove = findWinningMove('O');
            if (winMove !== -1) return winMove;
            
            // Попытаться заблокировать игрока
            const blockMove = findWinningMove('X');
            if (blockMove !== -1) return blockMove;
            
            // Случайный ход
            return findRandomMove();
        }

        // Ход бота
        function makeBotMove() {
            if (!state.gameActive) return;
            
            let move;
            
            // Выбор стратегии в зависимости от количества сделанных ходов
            const strategyIndex = state.botMovesCount % 4;
            
            switch(strategyIndex) {
                case 0:
                    move = aggressiveStrategy();
                    break;
                case 1:
                    move = defensiveStrategy();
                    break;
                case 2:
                    move = centerStrategy();
                    break;
                case 3:
                    move = cornerStrategy();
                    break;
                default:
                    move = findRandomMove();
            }
            
            // Если стратегия не дала результат, случайный ход
            if (move === -1 || state.gameBoard[move] !== '') {
                move = findRandomMove();
            }
            
            if (move !== -1) {
                makeMove(move, 'O');
                state.botMovesCount++;
                
                // Проверить результат игры
                const result = checkGameResult();
                if (result) {
                    handleGameEnd(result);
                }
            }
        }

        // Проверить результат игры
        function checkGameResult() {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Горизонтали
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Вертикали
                [0, 4, 8], [2, 4, 6]             // Диагонали
            ];
            
            // Проверить победу
            for (const pattern of winPatterns) {
                const [a, b, c] = pattern;
                if (
                    state.gameBoard[a] !== '' &&
                    state.gameBoard[a] === state.gameBoard[b] &&
                    state.gameBoard[a] === state.gameBoard[c]
                ) {
                    return state.gameBoard[a]; // 'X' или 'O'
                }
            }
            
            // Проверить ничью
            if (!state.gameBoard.includes('')) {
                return 'draw';
            }
            
            // Игра продолжается
            return null;
        }

        // Обработать окончание игры
        function handleGameEnd(result) {
            state.gameActive = false;
            
            // Обновить статистику
            updateStatistics(result);
            
            // Показать результат
            showGameResult(result);
        }

        // Обновить статистику
        function updateStatistics(result) {
            state.stats.gamesPlayed++;
            
            if (result === 'X') {
                state.stats.winsX++;
            } else if (result === 'O') {
                state.stats.winsO++;
            } else if (result === 'draw') {
                state.stats.draws++;
            }
            
            // Сохранить в localStorage
            saveStats();
            
            // Обновить отображение статистики
            updateStats();
        }

        // Показать результат игры
        function showGameResult(result) {
            let title, message;
            
            if (result === 'X') {
                title = getTranslation('win-x');
                if (state.gameMode === 'bot') {
                    message = getTranslation('win-x');
                } else {
                    message = `${state.playerNames.player1} ${getTranslation('win-x')}`;
                }
            } else if (result === 'O') {
                title = getTranslation('win-o');
                if (state.gameMode === 'bot') {
                    message = getTranslation('win-o');
                } else {
                    message = `${state.playerNames.player2} ${getTranslation('win-o')}`;
                }
            } else {
                title = getTranslation('draw');
                message = getTranslation('draw');
            }
            
            elements.resultTitle.textContent = title;
            elements.resultMessage.textContent = message;
            
            // Показать модальное окно
            setTimeout(() => {
                elements.resultModal.classList.add('active');
            }, 800);
        }

        // Обновить индикатор хода
        function updateTurnIndicator() {
            if (!state.gameActive) return;
            
            let text;
            
            if (state.gameMode === 'bot') {
                text = state.currentPlayer === 'X' ? 
                    getTranslation('your-turn') : 
                    getTranslation('bot-turn');
            } else {
                const playerName = state.currentPlayer === 'X' ? 
                    state.playerNames.player1 : 
                    state.playerNames.player2;
                text = `${playerName} ${getTranslation('player-turn')}`;
            }
            
            elements.turnIndicator.textContent = text;
        }

        // Переключение темы
        function toggleTheme() {
            state.theme = state.theme === 'dark' ? 'light' : 'dark';
            setTheme(state.theme);
            saveState();
        }

        // Установка темы
        function setTheme(theme) {
            // Удалить все классы тем
            document.body.classList.remove('dark-theme', 'light-theme-colorful');
            
            if (theme === 'dark') {
                document.body.classList.add('dark-theme');
                elements.themeStatus.textContent = getTranslation('dark');
                elements.themeToggle.checked = false;
            } else {
                document.body.classList.add('light-theme-colorful');
                elements.themeStatus.textContent = getTranslation('light');
                elements.themeToggle.checked = true;
            }
        }

        // Генерация языков
        function generateLanguages() {
            elements.languagesGrid.innerHTML = '';
            
            for (const [code, lang] of Object.entries(languages)) {
                const langElement = document.createElement('div');
                langElement.className = `language-option ${state.language === code ? 'selected' : ''}`;
                langElement.dataset.lang = code;
                langElement.innerHTML = `${lang.flag} ${lang.name}`;
                
                langElement.addEventListener('click', () => {
                    setLanguage(code);
                    // Снять выделение
                    document.querySelectorAll('.language-option').forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    // Выделить выбранный
                    langElement.classList.add('selected');
                });
                
                elements.languagesGrid.appendChild(langElement);
            }
        }

        // Установка языка
        function setLanguage(lang) {
            state.language = lang;
            
            // Обновить все элементы с атрибутом data-lang
            document.querySelectorAll('[data-lang]').forEach(element => {
                const key = element.dataset.lang;
                if (translations[lang] && translations[lang][key]) {
                    element.textContent = translations[lang][key];
                }
            });
            
            // Обновить индикатор хода
            if (state.currentPage === 'game') {
                updateTurnIndicator();
            }
            
            // Сохранить настройки
            saveState();
        }

        // Обновить статистику
        function updateStats() {
            if (!elements.statsGrid) return;
            
            elements.statsGrid.innerHTML = `
                <div class="stat-card">
                    <div class="stat-value">${state.stats.gamesPlayed}</div>
                    <div class="stat-label">${getTranslation('games-played')}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${state.stats.winsX}</div>
                    <div class="stat-label">${getTranslation('wins-x')}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${state.stats.winsO}</div>
                    <div class="stat-label">${getTranslation('wins-o')}</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">${state.stats.draws}</div>
                    <div class="stat-label">${getTranslation('draws')}</div>
                </div>
            `;
        }

        // Получить перевод
        function getTranslation(key) {
            if (translations[state.language] && translations[state.language][key]) {
                return translations[state.language][key];
            }
            return key; // Вернуть ключ, если перевод не найден
        }

        // Сохранить состояние
        function saveState() {
            localStorage.setItem('ticTacToeState', JSON.stringify({
                theme: state.theme,
                language: state.language,
                stats: state.stats
            }));
        }

        // Загрузить состояние
        function loadState() {
            const savedState = localStorage.getItem('ticTacToeState');
            if (savedState) {
                const parsedState = JSON.parse(savedState);
                state.theme = parsedState.theme || 'dark';
                state.language = parsedState.language || 'ru';
                state.stats = parsedState.stats || state.stats;
            }
        }

        // Сохранить статистику
        function saveStats() {
            saveState(); // Статистика сохраняется как часть общего состояния
        }

        // Инициализировать приложение после загрузки DOM
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
