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

        #iframeContainer {
            display: none; /* Inicialmente oculto */
            margin-top: 20px;
            width: 100%;
        }

        @media (max-width: 600px) {
            .identify-option,
            .close-button {
                font-size: 14px;
                padding: 8px 16px;
            }
        }
    </style>
</head>
<body>
    <div class="login-container" id="loginContainer">
        <img src="https://i.ibb.co/nfjFm1T/HACKER.png" alt="Perfil">
        <h2>Aplicativo do Marques</h2>
        <form id="loginForm" onsubmit="return login()">
            <label for="email"><b>Email</b></label>
            <input type="email" placeholder="Digite seu email" name="email" required>
            <button type="submit">Login</button>
            <div id="loading" class="loading">
                <div class="spinner-border" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
                <p class="loading-text">Carregando...</p>
            </div>
        </form>
    </div>

    <div id="iframeContainer">
        <iframe id="mainContent" src="https://oibet.net/#/home" width="100%" height="600" frameborder="0"></iframe>
    </div>

    <script>
        function login() {
            var email = document.getElementsByName('email')[0].value;
            var loading = document.getElementById('loading');
            var loginForm = document.getElementById('loginForm');
            var iframeContainer = document.getElementById('iframeContainer');

            if (email.endsWith('@gmail.com')) {
                loginForm.style.display = 'none'; // Oculta o formulário de login
                loading.style.display = 'flex'; // Mostra o loading

                setTimeout(function() {
                    loading.style.display = 'none'; // Esconde o loading após 3 segundos (simulação)
                    iframeContainer.style.display = 'block'; // Mostra o container do iframe
                }, 3000); // Simula um tempo de carga de 3 segundos

                return false; // Evita o envio do formulário
            } else {
                alert('Por favor, utilize um email que termine com @gmail.com.');
                return false; // Evita o envio do formulário
            }
        }
    </script>
</body>
</html>
