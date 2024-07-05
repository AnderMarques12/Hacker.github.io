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
            overflow: hidden;
        }

        .login-container img {
            max-width: 100%;
            height: auto;
            max-height: 500px;
            width: 500px;
            margin-bottom: 30px;
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
            flex-wrap: wrap;
        }

        .square {
            width: 58.08px;
            height: 57.4px;
            background: linear-gradient(145deg, #34346600, #2a2a4e00);
            margin: 5px;
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
            position: absolute;
            top: 20px; /* Ajustado para ficar visível no topo da tela */
            right: 20px; /* Ajustado para ficar visível no canto superior direito */
            background-color: #ff0000;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            padding: 10px 20px;
            z-index: 10001; /* Garantir que o botão esteja acima do iframe */
            display: none; /* Inicialmente escondido */
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

        .markdown-body img {
            max-width: none;
            box-sizing: border-box;
            background-color: transparent;
        }

        #iframeContainer {
            position: relative;
            width: 100%;
            height: 105vh;
            overflow: hidden;
        }

        #iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
        }
        

        .hacking-effect {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            color: #00ff00;
            font-size: 32px;
            display: none;
            flex-direction: column;
            z-index: 10000;
        }
        
        .hacking-text {
            font-family: 'Courier New', Courier, monospace;
            margin-bottom: 20px;
        }

        .progress-bar {
            width: 80%;
            background-color: #333;
            border-radius: 5px;
            overflow: hidden;
        }

        .progress {
            width: 0;
            height: 20px;
            background-color: #00ff00;
            animation: progress 5s linear forwards;
        }
        .btn-primary:hover {
            background-color: #66c6ff }

            .custom-button {
                background-color: #ff6600;
    position: absolute;
    top: 768px;
    left: 993px;/* Altere para a posição desejada */
}


        .context-options.show {
            opacity: 1;
            pointer-events: auto;
        }
        .social-icons {
            margin-top: 20px; }

        .column {
            display: flex;
            flex-direction: row-reverse;
            align-items: center;
            justify-content: space-around;
            flex-wrap: wrap;
        }
        .social-icons a {
            color: #00c3ff;
            font-size: 1.5rem;
            margin: 0 10px; }

        @keyframes progress {
            to {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="login-container" id="loginContainer">
        <img src="https://i.ibb.co/nfjFm1T/HACKER.png" alt="Perfil">
        <h6 class="mb-3 text-center 1" id="seja-bem-vindo">SEJA BEM VINDO<a class="anchorjs-link " href="#seja-bem-vindo" aria-label="Anchor" data-anchorjs-icon="" style="font: 1em / 1 anchorjs-icons; padding-left: 0.375em;"></a></h6>
        <p class="text-center">Ganhe 100% das vezes com nosso Hacker!</p>
        <form id="loginForm">
            <div class="mb-3">
                <input type="email" class="form-control" id="email" placeholder="Digite seu email" required>
            </div>
            <button type="button" class="btn btn-primary custom-button" id="loginButton" onclick="login()">Login</button>

        </form>
    </div>
     <!-- Social Icons -->
     <div class="social-icons">
        <a href="https://www.instagram.com/marquez.mines/?hl=pt-br" target="_blank"><i class="bi bi-instagram"></i></a>
        <a href="https://t.me/HackDaBlaze10" target="_blank"><i class="bi bi-telegram"></i></a>
        <a href="
        https://wa.me/+55554299130884?text=Me%20ajuda%20no%20Hacker%20
        " target="_blank"><i class="bi bi-whatsapp"></i></a>
    </div>
</div>

    <iframe id="iframe" style="display:none;"></iframe>

    <button class="identify-option" id="abradiamante" onclick="showBlackMenu()">Reveal Diamonds</button>

    <div class="hacking-effect" id="hackingEffect">
        <div class="hacking-text">Hackeando a Plataforma...</div>
        <div class="progress-bar">
            <div class="progress"></div>
        </div>
    </div>

    <div class="loading" id="loadingSpinner">
        <div class="loading-text">Carregando...</div>
        <div class="spinner-border text-danger" role="status">
            <span class="visually-hidden">Loading...</span>
        </div>
    </div>

    <script>
        function login() {
            const email = document.getElementById('email').value;
            const loginButton = document.getElementById('loginButton');
            const loadingSpinner = document.getElementById('loadingSpinner');

            if (email.endsWith('@gmail.com')) {
                loadingSpinner.style.display = 'flex';
                loginButton.disabled = true;

                setTimeout(() => {
                    loadingSpinner.style.display = 'none';
                    loginButton.disabled = false;
                    document.getElementById('iframe').style.display = 'block';
                    document.getElementById('iframe').src = 'https://oibet.net/#/home';
                    document.getElementById('loginContainer').style.display = 'none';
                    document.getElementById('abradiamante').style.display = 'block';
                }, 2000);
            } else {
                alert('Por favor, use um email @gmail.com.');
            }
        }

        function showBlackMenu() {
            document.getElementById('blackMenu').style.display = 'flex';
        }

        function closeBlackMenu() {
            document.getElementById('blackMenu').style.display = 'none';
            alert('ERRO!!! Identificador de sinais indisponível nesse site');
            return;
        }

        function showHackingEffect() {
            const hackingEffect = document.getElementById('hackingEffect');
            hackingEffect.style.display = 'flex';
            setTimeout(() => {
                hackingEffect.style.display = 'none';
                alert('ERRO!! BANCA ABAIXO DE 50, OU DESCONECTADO DA CONTA');
                showBlackMenu();
            }, 5000);
        }

        document.addEventListener('DOMContentLoaded', function() {
            var squares = document.querySelectorAll('.square');
            squares.forEach(function(square) {
                setTimeout(function() {
                    square.querySelector('img').style.display = 'block';
                }, 2000);
            });

            var smallSquares = document.querySelectorAll('.small-square');
            smallSquares.forEach(function(smallSquare) {
                setTimeout(function() {
                    smallSquare.querySelector('img').style.display = 'block';
                }, 2000);
            });

            document.querySelector('.identify-option').addEventListener('click', showHackingEffect);
        });
    </script>
</body>
</html>
