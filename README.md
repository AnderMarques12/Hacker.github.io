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
            margin-bottom: 30px; /* Increased margin for more space */
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

        #blackMenu {
            position: fixed;
            top: 40%;
            left: 50%;
            padding: 11px;
            transform: translate(-50%, -50%);
            width: 409px;
            height: 386px;
            display: none;
            align-items: center;
            justify-content: space-around;
            z-index: 10000;
            flex-wrap: wrap;
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
            top: 370px;
            right: 110px;
            background-color: #ff0000;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            padding: 5px 20px;
        }

        .abradiamante {
            position: absolute;
            top: 60px;
            right: 100px;
            background-color: #ff0000;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            padding: 10px 20px;
            z-index: 9999;
            display: none;
        }

        .small-square {
            width: 63px;
            height: 60px;
            background: linear-gradient(145deg, #00000000, #00000000);
            margin: 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 10px;
            border: 3px solid #00ff0d;
            box-shadow: 0 1px 11px rgb(0 255 0 / 0%);
            position: relative;
            pointer-events: none;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .small-square img {
            max-width: 100%;
            max-height: 100%;
            display: none;
            object-fit: contain;
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
        <button class="abradiamante" id="abradiamante" onclick="showBlackMenu()">Hackear Plataforma</button>
        <iframe id="iframe" src="" style="display:none;"></iframe>
    </div>

    <div id="blackMenu">
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png"></div>
        </div>
        <button class="menu-close" onclick="closeBlackMenu()">Fechar</button>
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
        });
    </script>
</body>
</html>
