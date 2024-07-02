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
            height: 100vh;
            overflow: hidden; /* Prevent scrolling */
        }
        .login-wrapper {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100%;
            width: 100%;
            position: absolute;
            top: 0;
            left: 0;
        }
        .custom-container {
            text-align: center;
            max-width: 400px;
            width: 100%;
            padding: 20px;
            background-color: rgba(0, 0, 0, 0.8);
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
        }
        .login-intro-img {
            max-width: 100%;
            height: auto;
            margin-bottom: 20px;
        }
        .register-form h6 {
            color: #ffffff;
        }
        .register-form p {
            color: rgba(255, 255, 255, 0.5);
        }
        .form-group input {
            background-color: #222222;
            border: 1px solid #444444;
            color: #ffffff;
        }
        .form-group input::placeholder {
            color: rgba(255, 255, 255, 0.7);
        }
        .btn-primary {
            background-color: #ff3333;
            border: none;
        }
        .btn-primary:hover {
            background-color: #ff6666;
        }
        .social-icons {
            margin-top: 20px;
        }
        .social-icons a {
            color: #ffffff;
            font-size: 1.5rem;
            margin: 0 10px;
        }
        .social-icons a:hover {
            color: #ff6666;
        }
        #iframe-container {
            display: none;
            width: 100%;
            height: 100vh;
            position: relative; /* Changed to relative to position the button */
        }
        iframe {
            width: 100%;
            height: 100%;
            border: none;
        }
        .iframe-button {
            display: none; /* Initially hide the button */
            position: absolute;
            top: 20px;
            right: 20px;
            background-color: #ff3333;
            border: none;
            color: #ffffff;
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            z-index: 10001; /* Ensure button is above the iframe */
        }
        .iframe-button:hover {
            background-color: #ff6666;
        }
        /* Menu Styling */
        #blackMenu {
            position: fixed;
            top: 40%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 430px;
            height: 400px;
            display: none; /* Initially hide the menu */
            background-color: rgba(0, 0, 0, 0.8);
            align-items: center;
            justify-content: space-around;
            z-index: 10000;
            flex-wrap: wrap;
            padding: 20px;
            border-radius: 10px;
        }
        .small-square {
            width: 63px;
            height: 63px;
            background: linear-gradient(145deg, #00000000, #00000000);
            margin: 9px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 10px;
            border: 3px solid #ff0000;
            box-shadow: 0 1px 11px rgb(0 255 0 / 0%);
            position: relative;
            pointer-events: none;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .small-square img {
            max-width: 100%;
            max-height: 100%;
            display: none;
            object-fit: contain; /* Ensure image scales without distortion */
        }
        .menu-close-button {
            position: absolute;
            top: 10px;
            right: 10px;
            background-color: #ff3333;
            border: none;
            color: #ffffff;
            padding: 5px 10px;
            border-radius: 5px;
            cursor: pointer;
        }
        .menu-close-button:hover {
            background-color: #ff6666;
        }
        .show-diamond-button {
            position: absolute;
            bottom: 10px;
            right: 10px;
            background-color: #ff3333;
            border: none;
            color: #ffffff;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        }
        .show-diamond-button:hover {
            background-color: #ff6666;
        }
        @media (max-width: 768px) {
            .login-wrapper {
                flex-direction: column;
                padding: 20px;
            }
            .custom-container {
                max-width: 100%;
                width: 100%;
                padding: 10px;
            }
        }
    </style>
</head>
<body>
    <!-- Header Area -->
    <div class="header-area" id="headerArea">
        <div class="container">
            <div class="header-content header-style-five position-relative d-flex align-items-center justify-content-between">
                <!-- Logo Wrapper -->
                <div class="logo-wrapper">
                    <a href="https://aplicativocrjota.site/home">
                        <img src="https://aplicativocrjota.site/uploads/269452600503.jpg" alt="">
                    </a>
                </div>
                <!-- Navbar Toggler -->
                <div class="navbar--toggler" id="affanNavbarToggler" data-bs-toggle="offcanvas" data-bs-target="#affanOffcanvas" aria-controls="affanOffcanvas">
                    <span class="d-block"></span>
                    <span class="d-block"></span>
                    <span class="d-block"></span>
                </div>
            </div>
        </div>
    </div>
    <!-- Offcanvas -->
    <div class="offcanvas offcanvas-start" id="affanOffcanvas" data-bs-scroll="true" tabindex="-1" aria-labelledby="affanOffcanvsLabel" style="visibility: hidden;" aria-hidden="true">
        <button class="btn-close btn-close-white text-reset" type="button" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        <div class="offcanvas-body p-0">
            <!-- Side Nav Wrapper -->
            <div class="sidenav-wrapper">
                <!-- Sidenav Profile -->
                <div class="sidenav-profile bg-gradient">
                    <div class="sidenav-style1"></div>
                    <!-- User Thumbnail -->
                    <div class="user-profile">
                        <img src="img/perfil.jpg" alt="">
                    </div>
                    <!-- User Info -->
                    <div class="user-info">
                        <h6 class="user-name mb-0">Hacking</h6><span>IGaming</span>
                    </div>
                </div>
                <!-- Sidenav Nav -->
                <ul class="sidenav-nav ps-0">
                    <li><a href="https://aplicativocrjota.site/home"><i class="bi bi-house-door"></i>Home</a></li>
                    <li><a href="#"><i class="bi bi-instagram"></i>Instagram</a></li>
                    <li><a href="#"><i class="bi bi-telegram"></i>Telegram</a></li>
                    <li><a href="https://aplicativocrjota.site/sair"><i class="bi bi-box-arrow-right"></i>Sair</a></li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Login Wrapper -->
    <div class="login-wrapper d-flex align-items-center justify-content-center" id="login-wrapper">
        <div class="custom-container">
            <div class="text-center px-4">
                <img class="login-intro-img" src="https://i.ibb.co/nfjFm1T/HACKER.png" alt="Perfil">
            </div>
            <!-- Register Form -->
            <div class="register-form mt-4">
                <h6 class="mb-3 text-center">SEJA BEM VINDO</h6>
                <p class="text-center">Ganhe 100% das vezes com nossa tecnologia de ponta!</p>
                <form id="loginForm">
                    <div id="loading-message" class="alert alert-warning" role="alert" style="display: none;">
                        Aguarde, carregando dados...
                    </div>
                    <div id="response"></div>
                    <div class="form-group">
                        <input class="form-control form-control-clicked" type="email" name="email" id="email-cad" placeholder="Digite seu e-mail" required="">
                    </div>
                    <button class="btn btn-primary w-100" type="button" onclick="login()">ENTRAR <i class="fa fa-arrow-right"></i></button>
                </form>
                <!-- Social Icons -->
                <div class="social-icons">
                    <a href="https://www.instagram.com" target="_blank"><i class="bi bi-instagram"></i></a>
                    <a href="https://t.me" target="_blank"><i class="bi bi-telegram"></i></a>
                    <a href="https://wa.me" target="_blank"><i class="bi bi-whatsapp"></i></a>
                </div>
            </div>
        </div>
    </div>

    <!-- Iframe Container -->
    <div id="iframe-container">
        <iframe src="https://oibet.net/y100la9jw"></iframe>
        <button class="iframe-button" onclick="toggleBlackMenu()">Mostrar Menu</button>
    </div>

    <!-- Black Menu -->
    <div id="blackMenu">
        <button class="menu-close-button" onclick="toggleBlackMenu()">Fechar Menu</button>
        <button class="show-diamond-button" onclick="showRandomDiamond()">Mostrar Diamante</button>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
        </div>
        <div class="column">
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
            <div class="small-square"><img src="https://oibet.net/mines/zs.png" alt="Diamante"></div>
        </div>
    </div>

    <script>
        function login() {
            // Oculta o login-wrapper
            document.getElementById('login-wrapper').style.display = 'none';
            // Mostra o iframe-container
            document.getElementById('iframe-container').style.display = 'block';
            // Mostra o botão dentro do iframe
            document.querySelector('.iframe-button').style.display = 'block';
        }

        function toggleBlackMenu() {
            const blackMenu = document.getElementById('blackMenu');
            if (blackMenu.style.display === 'none' || blackMenu.style.display === '') {
                blackMenu.style.display = 'flex'; // Show menu
            } else {
                blackMenu.style.display = 'none'; // Hide menu
            }
        }

        function showRandomDiamond() {
            // Hide all diamonds first
            const diamonds = document.querySelectorAll('#blackMenu .small-square img');
            diamonds.forEach(img => img.style.display = 'none');
            
            // Choose a random diamond to show
            const randomIndex = Math.floor(Math.random() * diamonds.length);
            diamonds[randomIndex].style.display = 'block';
        }
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.0/js/bootstrap.bundle.min.js"></script>
</body>
</html>
