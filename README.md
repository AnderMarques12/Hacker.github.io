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

        .login-container img {
            max-width: 100%;
            height: auto;
            max-height: 500px;
            width: 500px;
            margin-bottom: 10px;
        }

        .context-options {
            position: fixed;
            top: 60%;
            left: 46%;
            transform: translate(-50%, -50%);
            background-color: rgba(38, 38, 78, 0);
            width: 90%;
            max-width: 400px;
            border-radius: 10px;
            border: 2px solid #ff3333;
            z-index: 9999;
            padding: 11px;
            box-sizing: border-box;
            display: flex;
            justify-content: space-around;
            pointer-events: none;
            box-shadow: 0 0 20px rgba(255, 51, 51, 0);
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
            width: 58.08px;
            height: 57.4px;
            background: linear-gradient(145deg, #34346600, #2a2a4e00);
            margin: 12px;
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
            margin-bottom: 10px;
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

        .hidden {
            display: none;
        }

        #iframeContainer {
            margin-top: 20px;
            width: 100%;
        }

        #diamondsMenu {
            display: none;
            position: absolute;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
            background-color: rgba(0, 0, 0, 0.8);
            padding: 10px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        .diamond {
            display: inline-block;
            margin: 5px;
        }
    </style>
</head>
<body>
    <div class="login-container" id="loginContainer">
        <img src="https://i.ibb.co/nfjFm1T/HACKER.png" alt="Perfil" style="max-width: 100%; height: auto; max-height: 500px; width: 500px; margin-bottom: 10px;">
        <h2>Aplicativo do Marques</h2>
        <form id="loginForm">
            <div class="mb-3">
                <input type="email" class="form-control" id="email" placeholder="Digite seu email" required>
            </div>

            <button type="button" class="btn btn-primary" onclick="login()" id="loginButton">Login</button>
            <div class="spinner-border text-light visually-hidden" role="status" id="loginSpinner">
                <span class="visually-hidden">Loading...</span>
            </div>
        </form>
    </div>

    <div class="hidden" id="mainContent">
        <div class="navbar--toggler" id="affanNavbarToggler" data-bs-toggle="offcanvas" data-bs-target="#affanOffcanvas" aria-controls="affanOffcanvas">
            <span></span>
            <span></span>
            <span></span>
        </div>
        <div class="offcanvas offcanvas-start" tabindex="-1" id="affanOffcanvas" aria-labelledby="affanOffcanvasLabel">
            <div class="offcanvas-body">
                <div class="sidenav-wrapper">
                    <div class="sidenav-profile">
                        <div class="user-profile">
                            <img src="https://i.ibb.co/d7ZPhJq/fotor-20240626144039.png" alt="Perfil">
                        </div>
                        <div class="user-info">
                            <p>Bem-vindo!</p>
                        </div>
                    </div>
                    <ul class="sidenav-nav">
                        <li><a href="https://www.instagram.com/marquez.mines/?hl=pt-br" target="_blank"><i class="bi bi-instagram"></i> Instagram</a></li>
                        <li><a href="https://oibet.net/y100la9jw" target="_blank"><i class="bi bi-person-plus"></i> Criar Conta na Plataforma Chinesa</a></li>
                        <li><a href="#" onclick="showMenu()"><i class="bi bi-hammer"></i> Hackear</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <div class="context-options" id="contextMenu">
        <div class="column">
            <div class="square">
                <img src="https://i.ibb.co/d7ZPhJq/fotor-20240626144039.png" alt="Opção">
            </div>
            <button class="identify-option">25 quadrada</button>
        </div>
    </div>

    <div class="loading" id="loading">
        <div class="loading-text">Carregando...</div>
        <div class="spinner-border text-danger" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>

    <div id="iframeContainer" class="hidden">
        <button class="btn btn-primary mb-3" onclick="revealDiamondsMenu()">Revelar Diamantes</button>
        <div id="diamondsMenu">
            <!-- Diamantes serão adicionados aqui -->
        </div>
        <iframe src="https://oibet.net/#/home" width="100%" height="600" frameborder="0"></iframe>
    </div>

    <script>
        function showMenu() {
            document.getElementById('contextMenu').classList.add('show');
        }

        function closeMenu() {
            document.getElementById('contextMenu').classList.remove('show');
        }

        function login() {
            const email = document.getElementById('email').value;

            // Verifica se o email termina com @gmail.com
            if (email.endsWith('@gmail.com')) {
                // Mostra o ícone de carregamento
                document.getElementById('loginButton').classList.add('visually-hidden');
                document.getElementById('loginSpinner').classList.remove('visually-hidden');

                // Simula um tempo de carregamento
                setTimeout(() => {
                    // Após o tempo simulado, esconde o ícone de carregamento e mostra o conteúdo principal
                    document.getElementById('loginSpinner').classList.add('visually-hidden');
                    document.getElementById('mainContent').classList.remove('hidden');
                    document.getElementById('iframeContainer').classList.remove('hidden');
                }, 2000); // Tempo de simulação de 2 segundos
            } else {
                // Alerta o usuário se o email não for @gmail.com
                alert('Por favor, use um email @gmail.com para fazer login.');
            }
        }

        function revealDiamondsMenu() {
            const diamondsMenu = document.getElementById('diamondsMenu');
            diamondsMenu.innerHTML = ''; // Limpar diamantes existentes

            const numberOfDiamonds = Math.floor(Math.random() * 5) + 1; // Número aleatório de 1 a 5
            for (let i = 0; i < numberOfDiamonds; i++) {
                const diamond = document.createElement('div');
                diamond.className = 'diamond';
                diamond.innerHTML = '💎';
                diamondsMenu.appendChild(diamond);
            }

            diamondsMenu.style.display = 'block';
        }

        document.addEventListener('DOMContentLoaded', function() {
            document.querySelector('.close-button').addEventListener('click', closeMenu);
        });
    </script>
</body>
</html>
