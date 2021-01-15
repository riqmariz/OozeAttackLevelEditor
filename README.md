# Ooze Attack Level Editor **v0.2.1**

Este repositório é um local para subir os arquivos de level do jogo Ooze Attack para poder testá-los e editá-los. Fique atento as versões da documentação.

- \* : significa que foi modificado recentemente, uma novidade.
- \# : significa que foi modificado a um certo tempo e daqui a pouco não será mais uma "novidade".

# Novidades

- Documentação *

- Novo link para download da build standalone do Level editor v0.2.1 *:  [link](https://drive.google.com/file/d/1zduFgl3LvdxikaGDjrQjcik7hCgZ6nMV/view?usp=sharing)

# Dicas

Nothing to see here, yet.

# Documentação *

É importante mencionar que essa documentação é só uma forma de tentar manter as regras/funcionalidades por escrito dos elementos específicos do jogo Ooze Attack, que virá a modificar ao longo do processo de evolução então é de bastante importância, sempre verificar a TAG da documentação para checar o versionamento de tal.

## Geração de Level

Ao clicar em geração de Level, você se deparará com um "formulário", ou falando mais tecnicamente, você irá popular uma classe chamada **LevelInfo** (esse formulário/classe será detalhado mais abaixo) que precisará preencher para no final, clicar no botão de gerar arquivo e suas configurações serão salvas em um arquivo .json na pasta escolhida. É importante mencionar que o Level Editor não tem capacidade ainda de perceber erros e cabe ao usuário preencher corretamente.

Ao gerar o arquivo, é imprescendível nomear o arquivo corretamente. Os nomes do arquivo serão associados com os levels do game. Você deve nomear os leveis com o seguinte padrão:
<br/>
 - Level_01.json
 - Level_02.json
 - Level_03.json
 - …
 - Level_XY.json

Caso contrário, é possível que o jogo não carregue corretamente os arquivos.
<br/>

## Classes

O propósito dessa seção é tentar dissecar as classes e explicar o que cada variável dela significa dentro do jogo.

Algumas infos não cabem serem explicadas aqui, pois estão detalhadas no Game Design Document (GDD)

<ul>
<li> <strong>Level Info</strong> </li>
 Classe principal que tem as informações necessárias para um Level do Ooze Attack
    <ul> 
    <li>buffsAvailable[] (Lista de buffs disponíveis)</li>
    Esses serão os buffs disponíveis dentro do Level
    <ul>
        <li>Apolo Light</li>
        <li>Areas Rage</li>
        <li>Atenas Wisdom</li>
        <li>Artemis Dexterity</li>
    </ul>
    <li><strong>[SpawnData]</strong> spawnData (Dados de Spawn)</li>
     Classe que contém as informações de spawn
     </ul>

 <br/>     

<li> <strong>Spawn Data</strong> </li>
    Classe contém todas as informações para realizar todos os spawns do Level, tendo spawns sequenciados e spawns paralelos associados.
    <ul>
    <li>spawnDataName (Nome dos dados de spawn)</li>
     essa varíavel corresponde ao nome do arquivo (spawnData), pode não ser tão relevante, serve mais para organização.
    <li>timeToStartFirstSpawn (Tempo para começar o primeiro Spawn)</li>
     tempo em segundos para especificar quanto tempo o primeiro spawn acontecerá, ou seja, quando o spawn de fato começará a entrar em ação.
    <li>timeBetweenSequencedSpawns (Tempo entre spawns sequenciais)</li>
    tempo em segundos para especifificar o tempo entre spawns sequenciais, ou seja, o tempo para começar o próximo spawn depois que um spawn foi terminado.
    <li><strong>[SpawnGroup]</strong>sequencedSpawns[] (Lista de Spawns Sequenciais)</li>
    variável correspondente a uma lista de <strong>SpawnGroups</strong>, que serão seguidos sequencialmente. Ou seja, o spawn seguirá uma ordem crescente, sempre esperando um terminar, para começar o próximo.
    <li><strong>[SpawnGroup]</strong> parallelSpawns[] (Lista de Spawns Paralelos)</li>
    variável correspondente a uma lista de <strong>SpawnGroups</strong>, que serão seguidos paralelamente. Ou seja, o spawn não respeitará ordem e todos spawns aqui, estarão rodando em paralelo, inclusive, paralelos entre si.
    </ul>

<br/>

<li> <strong>Spawn Group</strong> </li>
    <ul>
    <li> spawnGroupName (Nome do Grupo de Spawn)</li>
     essa varíavel corresponde ao nome do arquivo, pode não ser tão relevante, serve mais para organização.
    <li>enemySpawnGroup[] (Lista Grupo de Spawn de Inimigos)</li>
    Lista de objetos spawnáveis que serão spawnados pelo Spawner em si, a palavra inimigo aqui foi utilizada pelo contexto de spawners, pois eles normalmente spawnam inimigos, mas não é necessário ser um inimigo. Uma moeda por exemplo, também é um spawnável.
    <li>inOrderEnemy (Inimigo em Ordem)</li>
    Ao colocar essa variável como true, ou marcada na checkbox, significa que os objetos spawnaveis (enemSpawnGroup) serão selecionados em ordem. <strong>ATENÇÃO</strong>: se marcar essa opção, não marque a opção randomEnemy, ou randomWeightedEnemy, elas são excludentes.
    <li>randomEnemy (Inimigo aleatório)</li>
    Ao colocar essa variável como true, ou marcada na checkbox, significa que os objetos spawnaveis (enemSpawnGroup) serão selecionados em aleatoriamente de forma equiprovável. <strong>ATENÇÃO</strong>: se marcar essa opção, não marque a opção inOrderEnemy, ou randomWeightedEnemy, elas são excludentes.
    <li>randomWeightedEnemy (Inimigo aleatório com pesos)</li>
    Ao colocar essa variável como true, ou marcada na checkbox, significa que os objetos spawnaveis (enemSpawnGroup) serão selecionados em aleatoriamente utilizando os pesos associados a variável weightsEnemy. <strong>ATENÇÃO-1</strong>: a lista de pesos dos inimigos deve ter o mesmo tamanho que a quantidade de objetos spawnáveis. <strong>ATENÇÃO-2</strong>: se marcar essa opção, não marque a opção randomEnemy, ou inOrderEnemy, elas são excludentes. 
    <li>weightsEnemy[] (Lista de Pesos dos inimigos)</li>
    Ao colocar a variável randomWeightedEnemy como true, os valores dessa lista serão considerados, caso contrário, será ignorado. Essa lista se refere ao peso que o objeto terá na hora de sortear aleatoriamente um objeto spawnável. Ou seja, você pode colocar algo, para ter mais chances que outras e vice-versa.
    <li><strong>[SpawnArea]</strong> spawnPositions[] (Lista Posições de Spawn)</li>
    Lista de spawn areas em que os spawnáveis podem ser spawnados, ou seja, local em que eles podem ser spawnados.
    Cada spawn area é delimitado previamente pelo GDD. <img src="Readme Images/spawnAreasPic.PNG" alt="Spawn Areas Representation">
    <ul>
       <li> Coin Area </li>
        <li> Top </li>
       <li> TopMiddle </li>
        <li> Middle</li>
       <li> BottomMiddle </li>
        <li> Bottom </li>
    </ul>
    <li>inOrderSpawn (Spawn Area em Ordem)</li>
    Funciona analogamente a variável inOrderEnemy, porém, se refere a lista de spawn area e de como será selecionada.
    <li>randomSpawnArea (Spawn Area aleatoriamente)</li>
    Funciona analogamente a variável randomEnemy, porém, se refere a lista de spawn area e de como será selecionada.
    <li>randomWeightedSpawnArea (Spawn Area aleatoriamente com pesos)</li>
    Funciona analogamente a variável randomWeightedSpawnArea, porém, se refere a lista de spawn area e de como será selecionada.
    <li>weightsSpawnArea[] (Lista de Pesos das Spawn Areas)</li>
    Funciona analogamente a variável weightsEnemy[], porém, se refere a lista de spawn area e de como será selecionada.
    <li><strong>[Spawner]</strong> spawner (Tipo de Spawner)</li>
    escolher qual é o tipo de <strong>Spawner</strong> que será utilizado, ou seja, escolher como cada spawn será spawnado, literalmente, "como". Por exemplo, os spawnaveis serão spawnados por waves, ou então serão spawnados por waves com tempo...
    </ul>
<br/>

<li> <strong>Spawner</strong> </li>
Esta classe define como os objetos spawnáveis serão spawnados, como por exemplo, será em forma de waves, waves com tempo, ou então vai spawnar com refil, toda vez que um objeto for eliminado, ele será reposto até certo tempo... Vários tipos, e os disponíveis estarão detalhados mais abaixo. Porém, há algumas variáveis que são comuns entre eles.
    <ul>
    <li>spawnerName (Nome do Spawner)</li>
    <br/>
     essa varíavel corresponde ao nome do arquivo, pode não ser tão relevante, serve mais para organização.
    <li>delayBetweenSpawns (Tempo entre spawns) </li>
    <br/>
    tempo entre um spawn e o próximo spawn, ou seja, depois de terminar um spawn, haverá um tempo em segundos de espera para o próximo.
    <br/>
    <li>spawnerType (tipo de spawner) </li>
        <ul>
        <li>Wave Spawner (Spawner de Onda)</li>
        Spawner clássico para jogos, em que haverá uma quantidade de inimigos por onda e também pode haver mais de uma onda, que acontece ao acabar a onda anterior, que acaba quando os inimigos morrem.
            <ul>
            <li>numberOfWaves (Número de ondas)</li>
            número de waves que o spawner terá por
            <li>totalEnemiesPerWave (Número de inimigos por onda)</li>
            número de objetos spawnaveis que o spawner terá por onda
            </ul>
        <li>Timed Wave Spawner (Spawner de Onda com tempo)</li>
        Funciona muito parecido com Wave Spawner, porém a diferença é que independente de se a wave atual foi terminada ou não (ou seja, se os inimigos morreram ou não), se der o tempo para próxima wave, a próxima wave será spawnada e acumulará com a atual.
            <ul>
            <li>waveTimer (Contagem regressiva da Onda)</li>
            tempo para a próxima wave ser spawnada, independente da wave atual, ter sido terminada ou não.
            </ul>
        <li>Once Spawner (Spawner "Único", ou, uma vez)</li>
        Esse spawner ele funciona da seguinte forma: Um objeto será spawnado uma única vez, o objeto e só. Ele pode acabar quando matar todos inimigos, ou no momento tiver terminado de spawnar os inimgos, basta escolher.
            <ul>
            <li>totalEnemies (Total de Inimigos)</li>
            quantidade total de inimigos que serão spawnados
            <li>howToComplete (Como completar)</li>
            como completar o spawner em si, quando finalizar? 
                <ul>
                <li>AfterAllSpawned (Depois de todos terem sido spawnados)</li>
                <li>AfterKillingAllEnemies (Depois de matar todos inimigos)</li>
                </ul>
            </ul>
        <li>Order Time Spawner (Spawner em Ordem com tempo)</li>
        Esse spawner funciona como uma wave única, na qual você pode manualmente dizer qual é o tempo entre cada inimigo de ser spawnado, ou seja, é uma wave única um pouco mais customizável. Atenção é importante colocar a quantidade de elementos dentro do enemyDelay, com o mesmo número de inimigos totais;
            <ul>
            <li>totalEnemies (Total de inimigos)</li>
            Quantidade de inimigos que serão spawnados
            <li>enemyDelay[] (Lista Tempo dos Inimigos)</li>
            É uma lista dos tempos em segundos em que cada inimigo será spawnado. <strong>PORÉM TEM UMA OBSERVAÇÃO IMPORTANTE</strong>: a lista deve ter o mesmo tamanho que a quantidade de inimigos. ou seja, é como se para cada inimigo você tivesse que manualmente escolher um tempo.
            </ul>
        <li>Probabilistic Spawner (Spawner com probabilidade)</li>
        Esse spawner funciona com uma probabilidade de spawn. Ou seja, ele pode acabar não spawnando nada, mas a cada Tick, ou cada intervalo, ele tentará spawnar, sorteará se irá spawnar. O tempo do intervalo, customizável pela variável timeBetweenSpawns, e a chance de sucesso, customizável pela variável chanceToSpawn.
            <ul>
            <li>chanceToSpawn (Chance para Spawnar)</li>
            Chance de sucesso para spawnar um objeto a cada sorteio que acontecerá ao fim de cada intervalo. Chance de 0% a 100%.
            <li>timeToStopSpawner (tempo para parar o spawner)</li>
            Tempo em segundos para parar o spawner, ou seja, depois que passar o tempo, o spawner dará como concluído, tendo spawnado ou não, ou seja, tendo "ganhado" ou não o sorteio, ele dará como concluído, quando o tempo acabar.
            </ul>
        <li>Refill Spawner (Spawner com reposição)</li>
        Esse spawner funciona fazendo reposições dos inimgos que foram mortos, ele sempre tenta manter uma certa quantidade de inimigos dentro do jogo por um determinado tempo, e assim, conclui.
            <ul>
            <li>totalEnemies (Total de Inimigos)</li>
            Quantidade de inimigos para spawnar e quantidade associada a quantos inimigos devem "permanecer" dentro do jogo, pois caso contrário, haverá reposição após timeBetweenSpawns ter passado.
            <li>maxRefilTime (Tempo máximo de reposição)</li>
            máximo de tempo em segundos em que poderá haver reposição
            <li>howToCompleteSpawn (Como completar o spawn)</li>
            como o spawner irá dar como concluído?
                <ul>
                <li>KillingAllEnemies (Matando todos inimigos)</li>
                ou seja, depois que matar todos os inimigos, depois que o maxRefilTime acabar, o spawner dará como concluído.
                <li>TimeOut (Tempo Esgotado)</li>
                Se o tempo de MaxRefilTime acabou, o spawner, instantaneamente se dá como concluído.
                </ul>
            </ul>
        </ul>
    </ul>

