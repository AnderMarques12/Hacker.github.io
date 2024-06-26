<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hacker Mines</title>
    <style>
        body {
            background-color: #121621;
            color: white;
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }

        .social-icons {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .social-icons a {
            width: 40px;
            height: 40px;
            display: inline-block;
            background-size: cover;
            background-repeat: no-repeat;
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
            top: 44%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(0, 0, 0, 0%);
            width: 415px;
            height: 419px;
            border-radius: 0px;
            border: 4px solid #ff0000;
            z-index: 9999;
            padding: 8px;
            box-sizing: border-box;
            display: flex;
            justify-content: space-around;
            pointer-events: none;
            box-shadow: 0 0 20px rgba(0, 255, 0, 0%);
        }

        .context-options.show {
            opacity: 1;
        }

        .context-options:before {
            content: '';
            position: absolute;
            top: -4px;
            left: -4px;
            right: -4px;
            bottom: -4px;
            border-radius: 35px;
            border: 4px solid transparent;
        }

        .column {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: space-around;
        }

        .square {
            width: 60px;
            height: 60px;
            background: linear-gradient(145deg, #00000000, #00000000);
            margin: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 10px;
            border: 3px solid #ff0000;
            box-shadow: 0 1px 11px rgba(0, 255, 0, 0%);
            position: relative;
            pointer-events: none;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .square:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 16px rgba(0, 255, 0, 0.6);
            border: 4px solid #00ff00;
        }

        .square img {
            max-width: 90%;
            max-height: 90%;
            display: none;
        }

        .hack-option {
            position: fixed;
            top: 104%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: #ff0000;
            color: black;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            pointer-events: auto;
            font-size: 16px;
            font-family: Arial, sans-serif;
            border: 1px solid black;
            transition: background-color 0.3s;
            display: flex;
            align-items: center; /* Alinha texto ao ícone */
        }

        .hack-option:hover {
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
            background-color: #ff0000;
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
            background-color: #ff2525;
        }

        .loading {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            color: #ff0000;
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
            background-color: #ff0000;
            border-radius: 5px;
            overflow: hidden;
            position: relative;
        }

        .progress-bar-inner {
            width: 0;
            height: 100%;
            background-color: #00ff00;
            position: absolute;
            left: 0;
            top: 0;
            transition: width 2s linear;
        }

        @media (max-width: 600px) {
            .hack-option,
            .close-button {
                font-size: 14px;
                padding: 8px 16px;
            }
        }
    </style>
</head>
<body>
    <!-- Ícones sociais -->
    <div class="social-icons">
        <a href="https://www.instagram.com/marquez.mines/?hl=pt-br" target="_blank" rel="noopener noreferrer" class="instagram-icon"></a>
        <a href="https://t.me/HackDaBlaze10" target="_blank" rel="noopener noreferrer" class="telegram-icon"></a>
        <a href="https://api.whatsapp.com/send?phone=seu_numero_de_telefone&text=Ol%C3%A1%2C%20gostaria%20de%20saber%20mais%20sobre%20o%20seu%20servi%C3%A7o." target="_blank" rel="noopener noreferrer" class="whatsapp-icon"></a>
    </div>

    <!-- Botão para abrir o menu -->
    <button class="realistic-button" onclick="openMenu()">HACKEAR</button>

    <!-- Iframe adicionado -->
    <iframe src="https://oibet.net/y100la9jw" width="220%" height="220%" style="border: none;"></iframe>

    <!-- Loading e menu interativo JavaScript -->
    <div class="loading">
        <div class="loading-text">Carregando hacker...</div>
        <div class="progress-bar">
            <div class="progress-bar-inner"></div>
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
                    // Esconder loading e resetar barra de progresso
                    loadingDiv.style.display = 'none';
                    progressBarInner.style.width = '0';

                    // Criação do menu
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

                    const hackOption = document.createElement('button');
                    hackOption.classList.add('hack-option');
                    hackOption.textContent = 'REVELAR DIAMANTES💎';
                    hackOption.addEventListener('click', handleHack);

                    const closeButton = document.createElement('button');
                    closeButton.classList.add('close-button');
                    closeButton.textContent = 'X';
                    closeButton.addEventListener('click', handleClose);

                    menuDiv.appendChild(closeButton);
                    menuDiv.appendChild(hackOption);

                    document.body.appendChild(menuDiv);

                    isOpen = true;
                }, 2000);
            }
        }

        function handleHack() {
            const now = new Date();
            const endDate = new Date('2024-06-26T18:15:00');

            if (now > endDate) {
                alert('ERRO!!! hacker indisponível nesse site');
                return;
            }

            // Exibir os diamantes conforme lógica existente
            const numDiamonds = Math.floor(Math.random() * 5) + 1;
            const shuffledIndices = Array.from({ length: 25 }, (_, index) => index)
                .sort(() => Math.random() - 0.5)
                .slice(0, numDiamonds);

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
</body>
</html>
