# GROM-RUSSIA-
Игра для веселья и чего нужно
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Black Russia Mobile · концепт</title>
    <!-- Иконки Font Awesome 6 (бесплатно) -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, system-ui, -apple-system, sans-serif;
        }

        body {
            background: #0b0e16;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 8px;
            touch-action: manipulation; /* отключает двойной зум на тапах */
        }

        /* главный контейнер — как мобильное приложение */
        .mobile-game {
            max-width: 450px;  /* ширина как у телефона */
            width: 100%;
            background: #121824;
            border-radius: 48px 48px 32px 32px;
            box-shadow: 0 25px 40px rgba(0,0,0,0.9), 0 0 0 3px #3f4d7a;
            overflow: hidden;
            border: 1px solid #5d6ea0;
        }

        /* верхний статус-бар (монеты, донат, энергия) */
        .status-bar {
            background: #1f2842;
            padding: 18px 20px 12px;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            border-bottom: 3px solid #37447a;
            gap: 10px;
        }

        .nick-avatar {
            display: flex;
            align-items: center;
            gap: 8px;
            background: #0d1221;
            padding: 5px 15px 5px 8px;
            border-radius: 50px;
            border: 2px solid #6a7bcb;
        }
        .avatar {
            width: 40px;
            height: 40px;
            background: linear-gradient(145deg, #f5b042, #e06917);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 22px;
            color: white;
            border: 2px solid #ffcf8a;
        }
        .nick {
            font-weight: 700;
            color: white;
            font-size: 18px;
        }
        .level-badge {
            background: #37467c;
            border-radius: 30px;
            padding: 6px 12px;
            color: #ffd966;
            font-weight: 800;
            font-size: 15px;
            border: 1px solid #a1b2ff;
        }

        .currency-row {
            display: flex;
            gap: 12px;
        }
        .money {
            display: flex;
            align-items: center;
            background: #0d1a1f;
            padding: 6px 18px;
            border-radius: 40px;
            border: 2px solid #b88637;
            color: #ffbf69;
            font-weight: 800;
            font-size: 18px;
            gap: 6px;
        }
        .gold {
            border-color: #d4af37;
            background: #1f1920;
            color: #ffd966;
        }

        /* индикатор энергии (как в black Russia) */
        .energy-bar {
            background: #262f52;
            border-radius: 30px;
            padding: 12px 16px;
            margin: 12px 16px;
            display: flex;
            align-items: center;
            gap: 12px;
            border: 2px solid #4e6198;
            box-shadow: inset 0 4px 0 #0f1425;
        }
        .energy-icon {
            color: #5effb2;
            font-size: 28px;
            width: 40px;
            text-align: center;
        }
        .bar-bg {
            flex: 1;
            height: 20px;
            background: #2d3557;
            border-radius: 40px;
            border: 2px solid #606fb0;
            overflow: hidden;
        }
        .bar-fill {
            width: 70%; /* текущая энергия */
            height: 100%;
            background: linear-gradient(90deg, #a2f5a2, #5ed15e);
            border-radius: 40px;
        }
        .energy-text {
            color: #bed0ff;
            font-weight: 700;
            font-size: 18px;
        }

        /* основная карта / локации — сетка 2x2 для мобильного */
        .map-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
            padding: 8px 16px 20px;
        }

        .location-card {
            background: #1e2643;
            border-radius: 28px;
            padding: 20px 6px 16px;
            text-align: center;
            border: 3px solid #3b467a;
            box-shadow: 0 9px 0 #0b0f1e;
            transition: 0.07s ease;
            touch-action: manipulation;
            cursor: pointer;
            user-select: none;
        }
        .location-card:active {
            transform: translateY(5px);
            box-shadow: 0 4px 0 #0b0f1e;
        }
        .location-icon {
            font-size: 42px;
            color: #ffb347;
            text-shadow: 0 4px 0 #9f5f20;
            margin-bottom: 8px;
        }
        .location-title {
            font-size: 20px;
            font-weight: 800;
            color: #f0e9cc;
            letter-spacing: 0.5px;
        }
        .location-desc {
            font-size: 14px;
            color: #99a9e6;
            font-weight: 600;
            margin: 6px 0 4px;
        }
        .profit {
            background: #2c3560;
            display: inline-block;
            padding: 6px 18px;
            border-radius: 50px;
            font-weight: 700;
            color: #b3ffaa;
            border: 2px solid #7979ff;
            font-size: 16px;
            margin-top: 6px;
        }

        /* БЛОК ЗАДАНИЙ И АКТИВНОСТЕЙ */
        .activities {
            background: #171f38;
            margin: 8px 16px 20px;
            border-radius: 40px;
            padding: 16px 10px;
            border: 2px solid #43528b;
        }
        .section-title {
            color: #ffdcaa;
            font-size: 22px;
            font-weight: 800;
            margin-left: 12px;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        .job-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .job-item {
            background: #222d51;
            border-radius: 30px;
            padding: 12px 18px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border: 2px solid #5e70b5;
            box-shadow: 0 5px 0 #0c1122;
            transition: 0.05s ease;
            cursor: pointer;
            touch-action: manipulation;
        }
        .job-item:active {
            transform: translateY(4px);
            box-shadow: 0 1px 0 #0c1122;
        }
        .job-name {
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 20px;
            font-weight: 600;
            color: #f0f2d7;
        }
        .job-reward {
            background: #1c361f;
            padding: 6px 15px;
            border-radius: 30px;
            color: #b5ffb5;
            font-weight: 700;
            border: 2px solid #7eb87e;
        }

        /* нижняя навигация (как в мобильной игре) */
        .bottom-nav {
            display: flex;
            background: #1b2340;
            padding: 14px 12px 20px;
            justify-content: space-around;
            border-top: 4px solid #38477b;
            margin-top: 10px;
        }
        .nav-btn {
            display: flex;
            flex-direction: column;
            align-items: center;
            color: #9aabdf;
            font-size: 14px;
            font-weight: 600;
            gap: 5px;
            transition: 0.1s;
            cursor: pointer;
            touch-action: manipulation;
            padding: 6px 16px;
            border-radius: 40px;
        }
        .nav-btn i {
            font-size: 28px;
        }
        .nav-btn.active {
            background: #2d3769;
            color: #ffe694;
            box-shadow: inset 0 3px 0 #5d6db3;
        }

        /* модальное окно (имитация) */
        .modal-preview {
            background: #121b34;
            border-radius: 48px;
            margin: 16px;
            padding: 24px;
            border: 4px solid #566bb3;
            box-shadow: 0 20px 30px black;
        }
        .modal-preview p {
            color: white;
            font-size: 18px;
            margin-bottom: 20px;
        }
        .close-btn {
            background: #a14a4a;
            padding: 14px;
            border-radius: 60px;
            text-align: center;
            font-weight: 800;
            color: white;
            border: 3px solid #ffaeae;
        }

        /* экран авторизации (для начала) */
        .auth-screen {
            background: #0c1126;
            border-radius: 60px;
            padding: 40px 20px;
            text-align: center;
        }
        .auth-logo {
            font-size: 70px;
            color: #ffaa33;
            text-shadow: 0 8px 0 #a75800;
        }
        .auth-btn {
            background: #5e7d2e;
            padding: 18px;
            border-radius: 60px;
            font-weight: 800;
            color: white;
            border: 4px solid #b5ff6b;
            margin: 20px 0;
            font-size: 24px;
        }

        /* скрытые экраны (логика простейшая) */
        .hidden {
            display: none;
        }

        /* сообщение об энергии */
        .toast-message {
            background: #c94f4f;
            color: white;
            padding: 12px;
            border-radius: 60px;
            text-align: center;
            margin: 12px;
            font-weight: 700;
        }
    </style>
</head>
<body>

<div class="mobile-game" id="gameContainer">
    <!-- Экран входа (быстрый старт) -->
    <div id="authScreen" class="auth-screen">
        <div class="auth-logo">
            <i class="fas fa-city"></i>
        </div>
        <div style="color:white; font-size: 38px; font-weight: 800; margin: 20px 0;">BLACK RUSSIA</div>
        <div style="color:#b0b9f0; margin-bottom: 40px;">mobile · концепт</div>
        <div class="auth-btn" id="enterGameBtn">
            <i class="fas fa-play"></i> Войти через Telegram
        </div>
        <div style="color:#6c7bbd;">нажми чтобы начать</div>
    </div>

    <!-- Основной интерфейс игры (изначально скрыт) -->
    <div id="mainGame" class="hidden">
        <!-- Статус бар -->
        <div class="status-bar">
            <div class="nick-avatar">
                <div class="avatar"><i class="fas fa-user"></i></div>
                <span class="nick">Пахан_93</span>
                <span class="level-badge"><i class="fas fa-crown" style="color:gold;"></i> lvl 12</span>
            </div>
            <div class="currency-row">
                <div class="money"><i class="fas fa-coins"></i> 1,420</div>
                <div class="money gold"><i class="fas fa-gem"></i> 84</div>
            </div>
        </div>

        <!-- Энергия (интерактивная) -->
        <div class="energy-bar" id="energyBar">
            <div class="energy-icon"><i class="fas fa-bolt"></i></div>
            <div class="bar-bg">
                <div class="bar-fill" id="energyFill" style="width: 70%;"></div>
            </div>
            <div class="energy-text" id="energyText">70/100</div>
        </div>

        <!-- Карта/районы (4 шт как пример) -->
        <div class="map-grid">
            <div class="location-card" data-loc="port" data-energy="15">
                <div class="location-icon"><i class="fas fa-ship"></i></div>
                <div class="location-title">ПОРТ</div>
                <div class="location-desc">работа + криминал</div>
                <div class="profit">+150💰</div>
            </div>
            <div class="location-card" data-loc="center" data-energy="10">
                <div class="location-icon"><i class="fas fa-building"></i></div>
                <div class="location-title">ЦЕНТР</div>
                <div class="location-desc">офисы, магазины</div>
                <div class="profit">+90💰</div>
            </div>
            <div class="location-card" data-loc="ghetto" data-energy="20">
                <div class="location-icon"><i class="fas fa-campground"></i></div>
                <div class="location-title">ЗАСТРОЙКА</div>
                <div class="location-desc">рискованные дела</div>
                <div class="profit">+270💰</div>
            </div>
            <div class="location-card" data-loc="mafia" data-energy="25">
                <div class="location-icon"><i class="fas fa-skull"></i></div>
                <div class="location-title">МАФИЯ</div>
                <div class="location-desc">крыша, заказы</div>
                <div class="profit">+400💰</div>
            </div>
        </div>

        <!-- Ежедневные задания / активности -->
        <div class="activities">
            <div class="section-title"><i class="fas fa-clipboard-list"></i> ЗАДАНИЯ ДНЯ</div>
            <div class="job-list">
                <div class="job-item" data-job="1" data-energy="5">
                    <span class="job-name"><i class="fas fa-dump-truck"></i> Разгрузить фуру</span>
                    <span class="job-reward">+80💰</span>
                </div>
                <div class="job-item" data-job="2" data-energy="8">
                    <span class="job-name"><i class="fas fa-hand-holding-usd"></i> Собрать дань</span>
                    <span class="job-reward">+150💰</span>
                </div>
                <div class="job-item" data-job="3" data-energy="12">
                    <span class="job-name"><i class="fas fa-car-crash"></i> Угон авто</span>
                    <span class="job-reward">+300💰</span>
                </div>
            </div>
        </div>

        <!-- Нижнее меню -->
        <div class="bottom-nav">
            <div class="nav-btn active" id="navMap"><i class="fas fa-map"></i><span>Карта</span></div>
            <div class="nav-btn" id="navInventory"><i class="fas fa-box"></i><span>Склад</span></div>
            <div class="nav-btn" id="navClan"><i class="fas fa-users"></i><span>Банда</span></div>
            <div class="nav-btn" id="navShop"><i class="fas fa-cart-shopping"></i><span>Магазин</span></div>
        </div>
    </div>

    <!-- Всплывашка для уведомлений (тост) -->
    <div id="toast" class="toast-message hidden">Недостаточно энергии</div>
</div>

<script>
    (function() {
        // Энергия (глобально для демо)
        let currentEnergy = 70;
        const maxEnergy = 100;
        const energyFill = document.getElementById('energyFill');
        const energyText = document.getElementById('energyText');
        const toast = document.getElementById('toast');

        // Монеты (пример)
        let balance = 1420;  // можно увеличивать

        // Функция обновления энергии
        function updateEnergyUI() {
            if (energyFill && energyText) {
                let percent = (currentEnergy / maxEnergy) * 100;
                energyFill.style.width = percent + '%';
                energyText.innerText = currentEnergy + '/' + maxEnergy;
            }
        }

        // Показать тост с сообщением на 1.5 сек
        function showToast(msg) {
            toast.innerText = msg;
            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 1500);
        }

        // Трата энергии с проверкой
        function spendEnergy(amount, reward = 0, locName = '') {
            if (currentEnergy >= amount) {
                currentEnergy -= amount;
                // увеличиваем баланс (монеты)
                balance += reward;
                updateEnergyUI();

                // показываем сообщение об успехе
                showToast(`✅ Заработано +${reward}💰 | -${amount}⚡`);
                // обновим отображение монет в двух местах
                updateMoneyUI();
                return true;
            } else {
                showToast('❌ Не хватает энергии! Отдыхай');
                return false;
            }
        }

        // Обновить деньги на экране
        function updateMoneyUI() {
            let moneySpans = document.querySelectorAll('.money');
            if (moneySpans.length >= 2) {
                moneySpans[0].innerHTML = `<i class="fas fa-coins"></i> ${balance.toLocaleString()}`;
            }
        }

        // Переключение экрана авторизации
        const authScreen = document.getElementById('authScreen');
        const mainGame = document.getElementById('mainGame');
        const enterBtn = document.getElementById('enterGameBtn');

        enterBtn.addEventListener('click', (e) => {
            e.preventDefault();
            authScreen.classList.add('hidden');
            mainGame.classList.remove('hidden');
            // синхронизация энергии при старте
            updateEnergyUI();
        });

        // ЗАПУСК СОБЫТИЙ ПОСЛЕ ЗАГРУЗКИ DOM
        document.addEventListener('DOMContentLoaded', function() {
            updateEnergyUI();

            // Клики по локациям (карточки районов)
            const locationCards = document.querySelectorAll('.location-card');
            locationCards.forEach(card => {
                card.addEventListener('click', (e) => {
                    e.preventDefault();
                    // Получаем энергию из data-energy
                    let energyCost = parseInt(card.getAttribute('data-energy')) || 10;
                    // получаем прибыль (можно вытащить из текста profit, но проще задать в дата)
                    let profitMap = {
                        'port': 150,
                        'center': 90,
                        'ghetto': 270,
                        'mafia': 400
                    };
                    let loc = card.getAttribute('data-loc');
                    let reward = profitMap[loc] || 100;

                    spendEnergy(energyCost, reward, loc);
                });
            });

            // Задания (job-item)
            const jobItems = document.querySelectorAll('.job-item');
            jobItems.forEach(job => {
                job.addEventListener('click', (e) => {
                    let energyCost = parseInt(job.getAttribute('data-energy')) || 5;
                    let reward = 0;
                    let jobId = job.getAttribute('data-job');
                    if (jobId === '1') reward = 80;
                    else if (jobId === '2') reward = 150;
                    else if (jobId === '3') reward = 300;

                    spendEnergy(energyCost, reward, 'job');
                });
            });

            // навигация (для демо просто подсвечиваем)
            const navMap = document.getElementById('navMap');
            const navInv = document.getElementById('navInventory');
            const navClan = document.getElementById('navClan');
            const navShop = document.getElementById('navShop');

            function resetNav() {
                [navMap, navInv, navClan, navShop].forEach(b => b.classList.remove('active'));
            }

            navMap.addEventListener('click', () => {
                resetNav();
                navMap.classList.add('active');
                showToast('📍 Карта района');
            });
            navInv.addEventListener('click', () => {
                resetNav();
                navInv.classList.add('active');
                showToast('📦 Инвентарь: пусто');
            });
            navClan.addEventListener('click', () => {
                resetNav();
                navClan.classList.add('active');
                showToast('🤝 Банда "Северные"');
            });
            navShop.addEventListener('click', () => {
