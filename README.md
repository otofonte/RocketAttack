# Rocket Attack é um jogo de corrida de navinhas !

Ele foi feito para rodar em computadores com windows e usa-se o teclado para direcionar a nave.

O jogo existe desde 2006, apesar de que o projeto ficou parado durante alguns períodos.\
Depois de um certo tempo eu voltava ao desenvolvimento e implementava novidades.

Um dos objetivos desse texto é explicar o código-fonte e explicar decisões tomadas durante o desenvolvimento.

### 1 - arquivo hta
O arquivo principal do jogo é um arquivo **hta**\
Esse tipo de arquivo é ao mesmo tempo texto e executável.\
É uma espécie de html executável !!!

### 2 - imagens dos foguetes
A pasta foguetes contém **36** imagens.\
No jogo a **nave principal** sempre fica no meio da tela.\
A nave rotaciona no sentido horário quando o jogador mantém a seta do teclado pressionada.\
No código-fonte existe uma váriável que armazena o ângulo de inclinação da nave.\
Na tela a nave é redesenhada constantemente no ângulo de inclinação correto.\
0 graus, 10 graus, 20 graus, 30 graus, 40 graus... até 350 graus.

### 3 - imagens da nave adversária
A nave adversária sempre anda em linha reta.\
0 graus ou 90 graus ou 180 graus ou 270 graus\
Por isso só são necessárias quatro imagens.\
No código-fonte existe a variável **anguloadv** que armazena o ângulo de inclinação da nave oponente.

### 4 - imagens do chão da pista
A pasta **/RA** contém as imagens 1.png, 2.png, 3.png e 4.png\
No código-fonte existe um array chamado pista.\
Esse array armazena se cada **ladrilho** deve ser uma seta para cima, ou uma seta para baixo, ou para algum lado, ou deve ser um ladrilho vazio.\
Na função drawStage a pista é desenhada e cada ladrilho é 'assentado' na sua posição correta em uma enorme **table**.

### 5 - função vira() e função para()
Faz sentido que o ângulo da nave seja atualizado quando o jogador pressiona a seta do teclado.\
Mas existe um delay entre o momento que o user pressiona a tecla e o modo repetição.\
Para lidar com isso existem as variáveis **esq** e **dir**. Elas armazenam se as setas estão pressionadas.

### 6 - xiniciais yiniciais xfinais yfinais
O mapa de cada fase é armazenado no array pista.\
A função **init** configura algumas variáveis.\
**posx** armazena a posição da navinha no eixo x\
**posy** armazena a posição da navinha no eixo y\
A função **init** calcula o posicionamento da navinha baseada nas coordenadas **xiniciais** , **yiniciais**

### 7 - tempo
A variável **tempo** é inicializada com zero na função **init**.\
A cada **'frame'** essa variável é incrementada.

### 8 - função init
A função init é executada a cada reinício do jogo.

### 9 - função gameLoop
A função gameLoop é executada a cada **'frame'**.\
No início dessa função as variáveis **lx** e **ly** armazenam as coordenadas do **'ladrilho'** em que a nave oponente está.\
As variáveis **advx** e **advy** armazenam a posição da nave oponente.\
A variável **pista\[fase]\[lx]\[ly]** armazena se o ladrilho aponta para cima ou para baixo ou para esquerda ou para direita. Isso determina o **anguloadv**.\
anguloadv é o ângulo da nave oponente.\
A nave oponente é renderizada no ângulo correto e na posição atualizada.\
As variáveis xfinais e yfinais armazenam a coordenada do fim da pista. Se a nave oponente chegou ao fim, uma mensagem é exibida e o jogo é reiniciado.\
As variáveis **esq** e **dir** armazenam **true** se as setas do teclado estiverem pressionadas.\
O ângulo da nave principal é recalculado.\
A nave é renderizada no angulo correto.\
O cálculo para verificar se a nave colide com a nave oponente é mais simples do que parece.\
Agora as variáveis **lx** e **ly** armazenam as coordenadas do ladrilho em que a **nave** está.\
Se a nave está corretamente **'sobre algum ladrilho'** da pista, então a posição da nave é recalculada.\
Caso contrário o jogo é reiniciado.\
As variáveis **xfinais** e **yfinais** armazenam a coordenada do fim da pista. Se a **nave** chegou ao fim, uma mensagem de vitória é exibida e a próxima fase é iniciada.\
A variável **tempo** é **incrementada** ao **mesmo tempo** em que a função gameLoop é reinvocada.\
Um cálculo determina o tempo de delay até que o próximo frame seja exibido.

### 10 - fatorx fatory
Esse trecho talvez seja o mais complicado de entender.\
A cada **frame** a posição da nave é recalculada.\
Para recalcular, os arrays **fatorx** e **fatory** são importantes.\
O fatorx armazena a distância no eixo x.\
O fatory armazena a distância no eixo y.\
São 36 valores em cada um desses arrays.\
Um valor para cada ângulo.\
Por exemplo: se o ângulo for 4, **fatorx\[4]** é 5 e **fatory\[4]** é -4\
Isso significa que a nave deve se mover 5px no eixo x e -4px no eixo y.

### 11 - setTimeout
A função **setTimeout** determina uma ação após um período de tempo.\
A última linha da função **gameLoop** chama novamente a função gameLoop.\
Após um delay calculado.
