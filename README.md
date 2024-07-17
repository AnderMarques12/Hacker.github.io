

        
    
  
            document.getElementById('login-wrapper').style.display = 'none';
            // Mostra o iframe-container
            document.getElementById('iframe-container').style.display = 'block';
            // Mostra o botão dentro do iframe
            document.querySelector('.iframe-button').style.display = 'block';
        }

        function toggleBlackMenu() {
            const hackingEffect = document.getElementById('hackingEffect');
            hackingEffect.style.display = 'flex';

    
        
          
    

     
  
            // Espera 5 segundos (tempo da animação de progresso) antes de mostrar o blackMenu
            setTimeout(() => {
                hackingEffect.style.display = 'none';
                showBlackMenu(); // Chama a função para exibir o blackMenu após a animação
                // Mostra os botões "Fechar Menu" e "Mostrar Diamante"
                document.querySelector('.menu-close-button').style.display = 'block';
                document.querySelector('.show-diamond-button').style.display = 'block';
            }, 5000); // Tempo da animação de progresso em milissegundos
            const blackMenu = document.getElementById('blackMenu');
            blackMenu.style.display = 'none'; // Oculta o menu
            // Oculta os diamantes
            var diamonds = document.querySelectorAll('.small-square img');
            diamonds.forEach(function(diamond) {
                diamond.style.display = 'none';
            });
        
        }

        function showBlackMenu() {
            const blackMenu = document.getElementById('blackMenu');
            if (blackMenu.style.display === 'none' || blackMenu.style.display === '') {

    
        
          
    

        
  
                blackMenu.style.display = 'flex'; // Mostra o menu
            } else {
                blackMenu.style.display = 'none'; // Oculta o menu
            }
        }

function toggleBlackMenu() {
    const hackingEffect = document.getElementById('hackingEffect');
    hackingEffect.style.display = 'flex';
    // Espera 5 segundos (tempo da animação de progresso) antes de mostrar o blackMenu
    setTimeout(() => {
        hackingEffect.style.display = 'none';

        alert('ERRO!! não foi possível hackear, nenhuma aposta feita');
    
    }, 5000); // Tempo da animação de progresso em milissegundos
}


        function showRandomDiamond() {


            var diamonds = document.querySelectorAll('.small-square img');
            diamonds.forEach(function(diamond) {
                diamond.style.display = 'none';

    
        
          
    

    
  
            });
            var numberOfDiamonds = Math.floor(Math.random() * 5) + 1; // Número aleatório de diamantes (1 a 5)
            var chosenDiamonds = [];
            while (chosenDiamonds.length < numberOfDiamonds) {
                var randomIndex = Math.floor(Math.random() * diamonds.length);
                if (!chosenDiamonds.includes(randomIndex)) {
                    chosenDiamonds.push(randomIndex);
                    diamonds[randomIndex].style.display = 'block';
                }
            }

        }

    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap/5.3.0/js/bootstrap.bundle.min.js"></script>
</body>

</html>
