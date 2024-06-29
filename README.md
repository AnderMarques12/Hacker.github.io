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
            margin: 44;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            overflow: hidden; /* Prevent scrolling */
        }

        .login-container img {
            max-width: 100%;
            height: auto;
            max-height: 500px;
            width: 500px;
            margin-bottom: 100px;
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

        #iframeContainer {
            position: relative;
            width: 100%;
            height: 100vh; /* Full viewport height */
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

        #blackMenu {
            position: fixed;
            top: 36%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 409px;
            height: 400px;
            background-color: #00000088;
            border: 0px solid #fff;
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            flex-wrap: wrap;
            overflow: auto; /* Allow scrolling if needed */
        }

        .menu-close {
            position: absolute;
            top: -20px;
            right: 10px;
            background-color: #ff0000;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            padding: 5px 20px;
        }

        .showDiamondButton {
            position: absolute;
            top: 390px;
            right: 15px;
            background-color: #ff0000;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            padding: 5px 20px;
        }

        .abradiamante {
            position: absolute;
            top: 20px;
            right: 20px;
            background-color: #ff0000;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            padding: 10px 20px;
            z-index: 9999;
        }

        .small-square {
            width: 50px;
            height: 50px;
            border: 1px solid #000;
            box-sizing: border-box;
            position: relative;
            margin: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .small-square img {
            max-width: 100%;
            max-height: 100%;
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
        </form>
    </div>

    <div id="iframeContainer">
        <button class="abradiamante" id="abradiamante" onclick="showBlackMenu()">Abrir Diamante</button>
        <iframe id="iframe" src="" style="display:none;"></iframe>
    </div>

    <div id="blackMenu">
        <button class="menu-close" onclick="closeBlackMenu()">X</button>
        <button id="showDiamondButton">Mostrar Diamante</button>
        <div class="column">
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
        </div>
        <div class="column">
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
        </div>
        <div class="column">
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
        </div>
        <div class="column">
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
        </div>
        <div class="column">
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
            <div class="small-square"><img></div>
        </div>
    </div>

    <div class="loading" id="loading">
        <div class="loading-text">Carregando...</div>
        <div class="spinner-border" role="status"></div>
    </div>

    <script>
        function login() {
            var email = document.getElementById('email').value;
            var loading = document.getElementById('loading');
            var loginButton = document.getElementById('loginButton');

            if (email.endsWith('@gmail.com')) {
                loading.style.display = 'flex';
                loginButton.disabled = true;

                setTimeout(function() {
                    document.getElementById('loginContainer').style.display = 'none';
                    document.getElementById('iframe').src = "https://oibet.net/#/home";
                    document.getElementById('iframe').style.display = 'block';
                    document.getElementById('abradiamante').style.display = 'block';
                    loading.style.display = 'none';
                    loginButton.disabled = false;
                }, 2000);
            } else {
                alert('Por favor, insira um email válido do Gmail.');
            }
        }

        function showBlackMenu() {
            var blackMenu = document.getElementById('blackMenu');
            blackMenu.style.display = 'flex';
        }

        function closeBlackMenu() {
            var blackMenu = document.getElementById('blackMenu');
            blackMenu.style.display = 'none';
        }

        document.getElementById('showDiamondButton').addEventListener('click', function() {
            // Remove any existing images from all small squares
            const allSquares = document.querySelectorAll('.small-square');
            allSquares.forEach(square => {
                const existingImage = square.querySelector('img');
                if (existingImage) {
                    square.removeChild(existingImage);
                }
            });

            // Randomly select a small square to show the image
            const squares = Array.from(document.querySelectorAll('.small-square'));
            const randomSquare = squares[Math.floor(Math.random() * squares.length)];

            // Create and add the image to the selected square
            const img = document.createElement('img');
            img.src = 'https://oibet.net/mines/zs.png';
            img.alt = 'Diamante';
            randomSquare.appendChild(img);
        });
    </script>
</body>
</html>
