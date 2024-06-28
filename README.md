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
            flex-direction: row-reverse;
            align-items: center;
            justify-content: space-around;
        }

        .square {
            width: 58.08px;
            height: 57.4px;
            background: linear-gradient(145deg, #34346600, #2a2a4e00);
            margin: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 0px;
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

        /* Estilos para o menu preto */
        #blackMenu {
            position: absolute;
            top: 55%;
            left: 49%;
            transform: translate(-50%, -50%);
            background-color: #00000000;
            width: 400px;
            height: 400px;
            display: none; /* Inicialmente escondido */
            border-radius: 5px;
            padding: 10px;
            box-sizing: border-box;
            z-index: 999;
        }

        #blackMenu .close-button {
            background-color: #cc0000;
            top: -10%;
            left: -6%;
            color: white;
            padding: 9px 39px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            border: none;
            transition: background-color 0.3s;
        }

        #blackMenu .close-button:hover {
            background-color: #ff0000;
        }

        /* Estilos para 25 quadrado branco 5 */
        .white-square {
            width: 45px;
            height: 45px;
            background-color: white;
            border: 1px solid black;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
            color: black;
            margin: 5px;
            position: relative;
        }

        .white-square img {
            max-width: 100%;
            max-height: 100%;
            display: none;
        }
    </style>
</head>
<body>
    <div class="login-container" id="loginContainer">
        <img src="https://i.ibb.co/nfjFm1T/HACKER.png" alt="Perfil">
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
        <div class="offcanvas offcanvas-start" tabindex="-1" id="affanOffcanvas" aria-labelledby="offcanvasExampleLabel">
            <div class="offcanvas-header">
                <h3 class="offcanvas-title" id="offcanvasExampleLabel">Minhas Preferências</h3>
                <button type="button" class="btn-close text-reset" data-bs-dismiss="offcanvas" aria-label="Close"></button>
            </div>
            <div class="offcanvas-body">
                <div class="sidenav-wrapper">
                    <div class="sidenav-profile">
                        <div class="user-profile">
                            <img src="https://i.ibb.co/d7ZPhJq/fotor-20240626144039.png" alt="Opção">
                        </div>
                        <div class="user-info">
                            <p>Marques</p>
                            <p>27</p>
                        </div>
                    </div>
                    <ul class="sidenav-nav">
                        <li><a href="#"><i class="bi bi-instagram"></i> Instagram</a></li>
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
        <div id="blackMenu">
            <div class="column"><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div></div>
            <div class="column"><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div></div>
            <div class="column"><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div></div>
            <div class="column"><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div></div>
            <div class="column"><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div><div class="square"><img></div></div>
           
            <!-- Conteúdo do menu preto -->
            <button class="close-button" onclick="closeBlackMenu()">Fechar</button>
            <button class="btn btn-danger mb-3" onclick="shuffleDiamonds()">Shuffle Diamonds</button>
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
                    document.getElementById('loginContainer').classList.add('hidden');
                    document.getElementById('mainContent').classList.remove('hidden');
                    document.getElementById('iframeContainer').classList.remove('hidden');
                }, 2000); // Tempo de simulação de 2 segundos
            } else {
                // Alerta o usuário se o email não for @gmail.com
                alert('Por favor, use um email @gmail.com para fazer login.');
            }
        }

        function revealDiamondsMenu() {
            // Mostra o menu preto
            document.getElementById('blackMenu').style.display = 'block';
            generateDiamonds();
        }

        function closeBlackMenu() {
            // Fecha o menu preto
            document.getElementById('blackMenu').style.display = 'none';
        }

        function generateDiamonds() {
            const diamondContainer = document.querySelector('.diamond-container');
            diamondContainer.innerHTML = '';

            const numDiamonds = Math.floor(Math.random() * 5) + 1; // Gera de 1 a 5 diamantes

            for (let i = 0; i < numDiamonds; i++) {
                const diamond = document.createElement('div');
                diamond.classList.add('diamond');
                diamond.textContent = '💎';
                diamondContainer.appendChild(diamond);
            }

            // Adiciona 25 quadrado branco 5 em cada coluna
            const whiteSquares = document.querySelectorAll('.white-square');
            const shuffledWhiteSquares = Array.from(whiteSquares).sort(() => Math.random() - 0.5);

            for (let i = 0; i < numDiamonds && i < shuffledWhiteSquares.length; i++) {
                const whiteSquare = shuffledWhiteSquares[i];
                const diamond = document.createElement('div');
                diamond.classList.add('diamond');
                diamond.textContent = '💎';
                whiteSquare.appendChild(diamond);
            }
        }

        function shuffleDiamonds() {
            const diamondContainer = document.querySelector('.diamond-container');
            const diamonds = Array.from(diamondContainer.querySelectorAll('.diamond'));

            // Embaralha a ordem dos diamantes
            diamonds.sort(() => Math.random() - 0.5);

            // Reinsere os diamantes na ordem embaralhada
            diamondContainer.innerHTML = '';
            diamonds.forEach(diamond => diamondContainer.appendChild(diamond));
        }

        document.addEventListener('DOMContentLoaded', function() {
            document.querySelector('.close-button').addEventListener('click', closeMenu);
        });
    </script>
</body>
</html>
