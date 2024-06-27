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
            background-color: #000000;
            color: #ffffff;
            font-family: Arial, sans-serif;
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .context-options {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(38, 38, 78, 0.9);
            width: 90%;
            max-width: 400px;
            border-radius: 10px;
            border: 2px solid #ff3333;
            z-index: 9999;
            padding: 16px;
            box-sizing: border-box;
            display: flex;
            justify-content: space-around;
            pointer-events: none;
            box-shadow: 0 0 20px rgba(255, 51, 51, 0.8);
            opacity: 0;
            transition: opacity 0.5s ease;
        }

        .context-options.show {
            opacity: 1;
            pointer-events: auto;
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
            background: linear-gradient(145deg, #343466, #2a2a4e);
            margin: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 5px;
            border: 2px solid #ff3333;
            box-shadow: 0 1px 5px rgba(255, 51, 51, 0.4);
            position: relative;
            pointer-events: none;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .square:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 16px rgba(255, 51, 51, 0.6);
            border: 2px solid #00cc66;
        }

        .square img {
            max-width: 90%;
            max-height: 90%;
            display: none;
        }

        .identify-option {
            background-color: #ff3333;
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
            background-color: #ff6666;
        }

        .close-button {
            position: absolute;
            top: -9%;
            right: -4%;
            background-color: #cc0000;
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
            background-color: #ff0000;
        }

        .loading {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            color: #ff3333;
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .loading-text {
            margin-bottom: 20px;
        }

        .spinner-border {
            width: 3rem;
            height: 3rem;
            border-width: 0.3rem;
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
            background-color: rgb(0, 0, 0); /* Alteração para fundo vermelho */
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
            background: linear-gradient(145deg, #000000,#2a3f4e); /* Ajuste do gradiente de fundo */
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

        .user-info p {
            margin-top: 0;
            margin-bottom: 1rem;
            color: white; /* Adicionando a cor branca */
        }

        .sidenav-nav {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .sidenav-nav li {
            border-bottom: 1px solid #3a3a3a;
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
            background-color: #343466;
        }

        .sidenav-nav i {
            margin-right: 10px;
            font-size: 20px;
        }

        .navbar--toggler {
            position: fixed;
            top: 10px;
            left: 10px;
            background-color: #000000;
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
        <span></span>
        <span></span>
        <span></span>
    </div>
    <div class="offcanvas offcanvas-start" id="affanOffcanvas" data-bs-scroll="true" tabindex="-1" aria-labelledby="affanOffcanvsLabel">
        <div class="offcanvas-body">
            <div class="sidenav-wrapper">
                <div class="sidenav-profile">
                    <div class="user-profile">
                        <img src="https://i.ibb.co/d7ZPhJq/fotor-20240626144039.png" alt="Perfil">
                    </div>
                    <div class="user-info">
                        <h6 class="user-name mb-1"></h6>
                        <p style="color: white;">Hacker Marques</p>
                    </div>
                </div>
                <ul class="sidenav-nav ps-0">
                    <li><a href="https://www.instagram.com/marquez.mines/?hl=pt-br" target="_blank"><i class="bi bi-instagram"></i>Instagram</a></li>
                    <li><a href="https://t.me/arnaldolac" target="_blank"><i class="bi bi-telegram"></i>Telegram</a></li>
                    <li><a href="https://wa.me/message/HIQKKQYH65N4P1" target="_blank"><i class="bi bi-whatsapp"></i>WhatsApp</a></li>
                </ul>
            </div>
        </div>
    </div>
    <div id="botao" class="identify-option" onclick="startLoading()">REVELAR SINAIS🔍</div>
    <div id="contextMenu" class="context-options">
        <div class="column">
            <div class="square" onclick="openLink('https://t.me/arnaldolac')"><img src="img/icone1.png"></div>
            <div class="square" onclick="openLink('https://wa.me/message/HIQKKQYH65N4P1')"><img src="img/icone2.png"></div>
        </div>
        <button class="close-button" onclick="toggleContextMenu()">X</button>
    </div>
    <div class="loading" id="loadingIndicator">
        <div class="loading-text">Carregando...</div>
        <div class="spinner-border text-danger" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>
    <iframe src="https://oibet.net/#/home" width="100%" height="600" frameborder="0"></iframe>
    <script>
        function toggleContextMenu() {
            const contextMenu = document.getElementById('contextMenu');
            contextMenu.classList.toggle('show');
        }

        function openLink(url) {
            window.open(url, '_blank');
        }

        function startLoading() {
            const loadingIndicator = document.getElementById('loadingIndicator');
            loadingIndicator.style.display = 'flex';
            setTimeout(() => {
                loadingIndicator.style.display = 'none';
                toggleContextMenu();
            }, 2000);
        }
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.0/js/bootstrap.bundle.min.js"></script>
</body>
</html>
