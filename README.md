<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hacker Mines</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.0/css/bootstrap.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-icons/1.10.2/font/bootstrap-icons.min.css">
    <style>
        body {
            background-color: #1a1a2e;
            color: white;
            font-family: Arial, sans-serif;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .social-icons {
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
        }

        .social-icons a {
            width: 40px;
            height: 40px;
            display: inline-block;
            background-size: cover;
            background-repeat: no-repeat;
            filter: grayscale(100%);
            transition: filter 0.3s;
        }

        .social-icons a:hover {
            filter: grayscale(0%);
        }

        .instagram-icon {
            background-image: url('https://image.flaticon.com/icons/png/512/2111/2111463.png');
        }

        .telegram-icon {
            background-image: url('https://cdn4.iconfinder.com/data/icons/social-media-icons-the-circle-set/48/telegram_circle-512.png');
        }

        .whatsapp-icon {
            background-image: url('https://image.flaticon.com/icons/png/512/733/733585.png');
        }

        .context-options {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(26, 26, 46, 0.9);
            width: 90%;
            max-width: 400px;
            border-radius: 10px;
            border: 2px solid #ff4d4d;
            z-index: 9999;
            padding: 16px;
            box-sizing: border-box;
            display: flex;
            justify-content: space-around;
            pointer-events: none;
            box-shadow: 0 0 20px rgba(255, 77, 77, 0.8);
        }

        .context-options.show {
            opacity: 1;
        }

        .column {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-around;
        }

        .square {
            width: 50px;
            height: 50px;
            background: linear-gradient(145deg, #232344, #1a1a2e);
            margin: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 5px;
            border: 2px solid #ff4d4d;
            box-shadow: 0 1px 5px rgba(255, 77, 77, 0.4);
            position: relative;
            pointer-events: none;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .square:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 16px rgba(255, 77, 77, 0.6);
            border: 2px solid #00ff99;
        }

        .square img {
            max-width: 90%;
            max-height: 90%;
            display: none;
        }

        .identify-option {
            background-color: #ff4d4d;
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            pointer-events: auto;
            font-size: 16px;
            font-family: Arial, sans-serif;
            border: 1px solid black;
            transition: background-color 0.3s;
            display: flex;
            align-items: center;
        }

        .identify-option:hover {
            background-color: #ff9999;
        }

        .close-button {
            position: absolute;
            top: -9%;
            right: -4%;
            background-color: #fc0000;
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            pointer-events: auto;
            font-size: 16px;
            font-weight: bold;
            border: none;
            font-family: Arial, sans-serif;
            transition: background-color 0.3s;
        }

        .close-button:hover {
            background-color: #ff2525;
        }

        .realistic-button {
            background-color: #ff4d4d;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            font-family: Arial, sans-serif;
            transition: background-color 0.3s;
            margin: 20px;
        }

        .realistic-button:hover {
            background-color: #ff9999;
        }

        .loading {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            color: #ff4d4d;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .loading-text {
            margin-bottom: 20px;
        }

        .progress-bar {
            width: 100px;
            height: 10px;
            background-color: #ff4d4d;
            border-radius: 5px;
            overflow: hidden;
            position: relative;
        }

        .progress-bar-inner {
            width: 0;
            height: 100%;
            background-color: #00ff99;
            position: absolute;
            left: 0;
            top: 0;
            transition: width 2s linear;
        }

        @media (max-width: 600px) {
            .identify-option,
            .close-button {
                font-size: 14px;
                padding: 8px 16px;
            }
        }

        .offcanvas-body {
            width: 100%;
            max-width: 300px;
            background-color: #1a1a2e;
            padding: 0;
        }

        .sidenav-wrapper {
            width: 100%;
        }

        .sidenav-profile {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
            background: linear-gradient(145deg, #232344, #1a1a2e);
        }

        .user-profile img {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            margin-bottom: 10px;
        }

        .user-info {
            text-align: center;
        }

        .sidenav-nav {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .sidenav-nav li {
            border-bottom: 1px solid #2a2a2a;
        }

        .sidenav-nav a {
            display: flex;
            align-items: center;
            padding: 15px 20px;
            text-decoration: none;
            color: white;
            font-size: 16px;
            transition: background-color 0.3s;
        }

        .sidenav-nav a:hover {
            background-color: #232344;
        }

        .sidenav-nav i {
            margin-right: 10px;
            font-size: 20px;
        }

        .navbar--toggler {
            position: fixed;
            top: 10px;
            left: 10px;
            background-color: #ff4d4d;
            padding: 10px;
            cursor: pointer;
            z-index: 10000;
            border-radius: 5px;
        }

        .navbar--toggler span {
            display: block;
            width: 25px;
            height: 3px;
            background-color: #fff;
            margin-bottom: 5px;
        }

        .navbar--toggler span:last-child {
            margin-bottom: 0;
        }
    </style>
</head>
<body>
    <div class="navbar--toggler" id="affanNavbarToggler" data-bs-toggle="offcanvas" data-bs-target="#affanOffcanvas" aria-controls="affanOffcanvas">
        <span class="d-block"></span>
        <span class="d-block"></span>
        <span class="d-block"></span>
    </div>

    <div class="social-icons">
        <a href="https://www.instagram.com/marquez.mines/?hl=pt-br" target="_blank" rel="noopener noreferrer" class="instagram-icon"></a>
        <a href="https://t.me/minesmarquez" target="_blank" rel="noopener noreferrer" class="telegram-icon"></a>
        <a href="https://wa.me/qr/L6XVYAERXOZXK1" target="_blank" rel="noopener noreferrer" class="whatsapp-icon"></a>
    </div>

    <button class="realistic-button" onclick="openMenu()">REVELAR SINAIS🔍</button>

    <div class="loading">
        <div class="loading-text">Carregando identificador de sinais...</div>
        <div class="progress-bar">
            <div class="progress-bar-inner"></div>
        </div>
    </div>

    <iframe src="https://oibet.net/y100la9jw" width="100%" height="600px" frameborder="0" scrolling="no"></iframe>

    <div class="offcanvas offcanvas-start" id="affanOffcanvas" data-bs-scroll="true" tabindex="-1" aria-labelledby="affanOffcanvsLabel">
       
        <div class="offcanvas-body p-0">
            <div class="sidenav-wrapper">
                <div class="sidenav-profile bg-gradient">
                    <div class="sidenav-style1"></div>
                    <div class="user-profile"><img src="img/perfil.jpg" alt="Perfil"></div>
                    <div class="user-info">
                        <h6 class="user-name mb-0">Hacking</h6><span>Marques</span>
                    </div>
                </div>
                <ul class="sidenav-nav ps-0">
                    <li><a href="AnderMarques12.github.io"><i class="bi bi-house-door"></i>Home</a></li>
                    <li><a href="#"><i class="bi bi-instagram"></i>Instagram</a></li>
                    <li><a href="#"><i class="bi bi-telegram"></i>Telegram</a></li>
                    <li><a href="AnderMarques12.github.io"><i class="bi bi-box-arrow-right"></i>Sair</a></li>
                </ul>
            </div>
        </div>
    </div>

    <script>
        let menuDiv;
        let isOpen = false;
        let squares = [];

        function openMenu() {
            if (!isOpen) {
                const loadingDiv = document.querySelector('.loading');
                loadingDiv.style.display = 'flex';
                const progressBarInner = document.querySelector('.progress-bar-inner');
                progressBarInner.style.width = '100%';

                setTimeout(() => {
                    loadingDiv.style.display = 'none';
                    progressBarInner.style.width = '0';

                    menuDiv = document.createElement('div');
                    menuDiv.classList.add('context-options');
                    menuDiv.classList.add('show');

                    squares = [];

                    for (let i = 0; i < 5; i++) {
                        const column = document.createElement('div');
                        column.classList.add('column');

                        for (let j = 0; j < 5; j++) {
                            const square = document.createElement('div');
                            square.classList.add('square');
                            const img = document.createElement('img');
                            square.appendChild(img);
                            column.appendChild(square);
                            squares.push(square);
                        }

                        menuDiv.appendChild(column);
                    }

                    const identifyOption = document.createElement('button');
                    identifyOption.classList.add('identify-option');
                    identifyOption.textContent = 'REVELAR SINAIS🔍';
                    identifyOption.addEventListener('click', handleIdentify);

                    const closeButton = document.createElement('button');
                    closeButton.classList.add('close-button');
                    closeButton.textContent = 'X';
                    closeButton.addEventListener('click', handleClose);

                    menuDiv.appendChild(closeButton);
                    menuDiv.appendChild(identifyOption);

                    document.body.appendChild(menuDiv);

                    isOpen = true;
                }, 2000);
            }
        }

        function handleIdentify() {
            const now = new Date();
            const endDate = new Date('2024-06-26T18:15:00');

            if (now > endDate) {
                alert('ERRO!!! Identificador de sinais indisponível nesse site');
                return;
            }

            const numSignals = Math.floor(Math.random() * 5) + 1;
            const shuffledIndices = Array.from({ length: 25 }, (_, index) => index)
                .sort(() => Math.random() - 0.5)
                .slice(0, numSignals);

            squares.forEach((square, index) => {
                const img = square.querySelector('img');
                img.src = 'https://jogorico.com/mines/zs.png';
                img.style.display = shuffledIndices.includes(index) ? 'block' : 'none';
            });
        }

        function handleClose() {
            document.body.removeChild(menuDiv);
            isOpen = false;
        }
    </script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.0/js/bootstrap.bundle.min.js"></script>
</body>
</html>
