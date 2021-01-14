# Ooze Attack Level Editor **v0.2.0**

Este repositório é um local para subir os arquivos de level do jogo Ooze Attack para poder testá-los e editá-los. Fique atento as versões da documentação.

- \* : significa que foi modificado recentemente, uma novidade.
- \# : significa que foi modificado a um certo tempo e daqui a pouco não será mais uma "novidade".

# Novidades

- Documentação *

- Novo link para download da build standalone do Level editor v0.2.0 *:  [link](https://drive.google.com/file/d/1G6SZW0OnUloq_UUohtc1KiY4fBHZ_-5T/view?usp=sharing)

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

* **Level Info**
 <br/>
 Classe principal que tem as informações necessárias para um Level do Ooze Attack
    * buffsAvailable[] (Lista de buffs disponíveis)
    <br/>
    Esses serão os buffs disponíveis dentro do Level
        * Apolo Light
        * Areas Rage
        * Atenas Wisdom
        * Artemis Dexterity
    * **[SpawnData]** spawnData (Dados de Spawn)
     <br/>
     Classe que contém as informações de spawn

 <br/>     

* **Spawn Data**
 <br/>
    Classe contém todas as informações para realizar todos os spawns do Level, tendo spawns sequenciados e spawns paralelos associados.
    * spawnDataName (Nome dos dados de spawn)
     <br/>
     essa varíavel corresponde ao nome do arquivo (spawnData), pode não ser tão relevante, serve mais para organização.
    * timeToStartFirstSpawn (Tempo para começar o primeiro Spawn)
     <br/>
     tempo em segundos para especificar quanto tempo o primeiro spawn acontecerá, ou seja, quando o spawn de fato começará a entrar em ação.
    * timeBetweenSequencedSpawns (Tempo entre spawns sequenciais)
    <br/>
    tempo em segundos para especifificar o tempo entre spawns sequenciais, ou seja, o tempo para começar o próximo spawn depois que um spawn foi terminado.
    * **[SpawnGroup]** sequencedSpawns[] (Lista de Spawns Sequenciais)
    <br/>
    variável correspondente a uma lista de **SpawnGroups**, que serão seguidos sequencialmente. Ou seja, o spawn seguirá uma ordem crescente, sempre esperando um terminar, para começar o próximo.
    * **[SpawnGroup]** parallelSpawns[] (Lista de Spawns Paralelos)
    <br/>
    variável correspondente a uma lista de **SpawnGroups**, que serão seguidos paralelamente. Ou seja, o spawn não respeitará ordem e todos spawns aqui, estarão rodando em paralelo, inclusive, paralelos entre si.

<br/>

* **Spawn Group**
<br/>
    * spawnGroupName (Nome do Grupo de Spawn)
    <br/>
     essa varíavel corresponde ao nome do arquivo, pode não ser tão relevante, serve mais para organização.
    * enemySpawnGroup[] (Lista Grupo de Spawn de Inimigos)
    <br/>
    Lista de objetos spawnáveis que serão spawnados pelo Spawner em si, a palavra inimigo aqui foi utilizada pelo contexto de spawners, pois eles normalmente spawnam inimigos, mas não é necessário ser um inimigo. Uma moeda por exemplo, também é um spawnável.
    * inOrderEnemy (Inimigo em Ordem)
    <br/>
    Ao colocar essa variável como true, ou marcada na checkbox, significa que os objetos spawnaveis (enemSpawnGroup) serão selecionados em ordem. ATENÇÃO: se marcar essa opção, não marque a opção randomEnemy, ou randomWeightedEnemy, elas são excludentes.
    * randomEnemy (Inimigo aleatório)
    <br/>
    Ao colocar essa variável como true, ou marcada na checkbox, significa que os objetos spawnaveis (enemSpawnGroup) serão selecionados em aleatoriamente de forma equiprovável. ATENÇÃO: se marcar essa opção, não marque a opção inOrderEnemy, ou randomWeightedEnemy, elas são excludentes.
    * randomWeightedEnemy (Inimigo aleatório com pesos)
    <br/>
    Ao colocar essa variável como true, ou marcada na checkbox, significa que os objetos spawnaveis (enemSpawnGroup) serão selecionados em aleatoriamente utilizando os pesos associados a variável weightsEnemy. ATENÇÃO-1: a lista de pesos dos inimigos deve ter o mesmo tamanho que a quantidade de objetos spawnáveis. ATENÇÃO-2: se marcar essa opção, não marque a opção randomEnemy, ou inOrderEnemy, elas são excludentes. 
    * weightsEnemy[] (Lista de Pesos dos inimigos)
    <br/>
    Ao colocar a variável randomWeightedEnemy como true, os valores dessa lista serão considerados, caso contrário, será ignorado. Essa lista se refere ao peso que o objeto terá na hora de sortear aleatoriamente um objeto spawnável. Ou seja, você pode colocar algo, para ter mais chances que outras e vice-versa.
    * **[SpawnArea]** spawnPositions[] (Lista Posições de Spawn)
    <br/>
    Lista de spawn areas em que os spawnáveis podem ser spawnados, ou seja, local em que eles podem ser spawnados.
    Cada spawn area é delimitado previamente pelo GDD.
        * Coin Area
        * Top
        * TopMiddle
        * Middle 1
        * Middle 2
        * BottomMiddle
        * Bottom
    * inOrderSpawn (Spawn Area em Ordem)
    <br/>
    Funciona analogamente a variável inOrderEnemy, porém, se refere a lista de spawn area e de como será selecionada.
    * randomSpawnArea (Spawn Area aleatoriamente)
    <br/>
    Funciona analogamente a variável randomEnemy, porém, se refere a lista de spawn area e de como será selecionada.
    * randomWeightedSpawnArea (Spawn Area aleatoriamente com pesos)
    <br/>
    Funciona analogamente a variável randomWeightedSpawnArea, porém, se refere a lista de spawn area e de como será selecionada.
    * weightsSpawnArea[] (Lista de Pesos das Spawn Areas)
    Funciona analogamente a variável weightsEnemy[], porém, se refere a lista de spawn area e de como será selecionada.
    * **[Spawner]** spawner (Tipo de Spawner)
    <br/>
    escolher qual é o tipo de **Spawner** que será utilizado, ou seja, escolher como cada spawn será spawnado, literalmente, "como". Por exemplo, os spawnaveis serão spawnados por waves, ou então serão spawnados por waves com tempo...

<br/>

* **Spawner**
<br/>
Esta classe define como os objetos spawnáveis serão spawnados, como por exemplo, será em forma de waves, waves com tempo, ou então vai spawnar com refil, toda vez que um objeto for eliminado, ele será reposto até certo tempo... Vários tipos, e os disponíveis estarão detalhados mais abaixo. Porém, há algumas variáveis que são comuns entre eles.
    * spawnerName (Nome do Spawner)
    <br/>
     essa varíavel corresponde ao nome do arquivo, pode não ser tão relevante, serve mais para organização.
    * delayBetweenSpawns (Tempo entre spawns)
    <br/>
    tempo entre um spawn e o próximo spawn, ou seja, depois de terminar um spawn, haverá um tempo em segundos de espera para o próximo.
    <br/>
    * spawnerType (tipo de spawner)
        * Wave Spawner (Spawner de Onda)
        <br/>
        Spawner clássico para jogos, em que haverá uma quantidade de inimigos por onda e também pode haver mais de uma onda, que acontece ao acabar a onda anterior, que acaba quando os inimigos morrem.
            * numberOfWaves (Número de ondas)
            <br/>
            número de waves que o spawner terá por
            * totalEnemiesPerWave (Número de inimigos por onda)
            <br/>
            número de objetos spawnaveis que o spawner terá por onda
        * Timed Wave Spawner (Spawner de Onda com tempo)
        <br/>
        Funciona muito parecido com Wave Spawner, porém a diferença é que independente de se a wave atual foi terminada ou não (ou seja, se os inimigos morreram ou não), se der o tempo para próxima wave, a próxima wave será spawnada e acumulará com a atual.
            * waveTimer (Contagem regressiva da Onda)
            <br/>
            tempo para a próxima wave ser spawnada, independente da wave atual, ter sido terminada ou não.
        * Once Spawner (Spawner "Único", ou, uma vez)
        <br/>
        Esse spawner ele funciona da seguinte forma: Um objeto será spawnado uma única vez, o objeto e só. Ele pode acabar quando matar todos inimigos, ou no momento tiver terminado de spawnar os inimgos, basta escolher.
            * totalEnemies (Total de Inimigos)
            <br/>
            quantidade total de inimigos que serão spawnados
            * howToComplete (Como completar)
            <br/>
            como completar o spawner em si, quando finalizar? 
                * AfterAllSpawned (Depois de todos terem sido spawnados)
                * AfterKillingAllEnemies (Depois de matar todos inimigos)
        * Order Time Spawner (Spawner em Ordem com tempo)
        <br/>
        Esse spawner funciona como uma wave única, na qual você pode manualmente dizer qual é o tempo entre cada inimigo de ser spawnado, ou seja, é uma wave única um pouco mais customizável. Atenção é importante colocar a quantidade de elementos dentro do enemyDelay, com o mesmo número de inimigos totais;
            * totalEnemies (Total de inimigos)
            <br/>
            Quantidade de inimigos que serão spawnados
            * enemyDelay[] (Lista Tempo dos Inimigos)
            <br/>
            É uma lista dos tempos em segundos em que cada inimigo será spawnado. PORÉM TEM UMA OBSERVAÇÃO IMPORTANTE: a lista deve ter o mesmo tamanho que a quantidade de inimigos. ou seja, é como se para cada inimigo você tivesse que manualmente escolher um tempo.
        * Probabilistic Spawner (Spawner com probabilidade)
        <br/>
        Esse spawner funciona com uma probabilidade de spawn. Ou seja, ele pode acabar não spawnando nada, mas a cada Tick, ou cada intervalo, ele tentará spawnar, sorteará se irá spawnar. O tempo do intervalo, customizável pela variável timeBetweenSpawns, e a chance de sucesso, customizável pela variável chanceToSpawn.
            * chanceToSpawn (Chance para Spawnar)
            <br/>
            Chance de sucesso para spawnar um objeto a cada sorteio que acontecerá ao fim de cada intervalo. Chance de 0% a 100%.
            * timeToStopSpawner (tempo para parar o spawner)
            <br/>
            Tempo em segundos para parar o spawner, ou seja, depois que passar o tempo, o spawner dará como concluído, tendo spawnado ou não, ou seja, tendo "ganhado" ou não o sorteio, ele dará como concluído, quando o tempo acabar.
        * Refill Spawner (Spawner com reposição)
        <br/>
        Esse spawner funciona fazendo reposições dos inimgos que foram mortos, ele sempre tenta manter uma certa quantidade de inimigos dentro do jogo por um determinado tempo, e assim, conclui.
            * totalEnemies (Total de Inimigos)
            <br/>
            Quantidade de inimigos para spawnar e quantidade associada a quantos inimigos devem "permanecer" dentro do jogo, pois caso contrário, haverá reposição após timeBetweenSpawns ter passado.
            * maxRefilTime (Tempo máximo de reposição)
            <br/>
            máximo de tempo em segundos em que poderá haver reposição
            * howToCompleteSpawn (Como completar o spawn)
            <br/>
            como o spawner irá dar como concluído?
                * KillingAllEnemies (Matando todos inimigos)
                <br/>
                ou seja, depois que matar todos os inimigos, depois que o maxRefilTime acabar, o spawner dará como concluído.
                * TimeOut (Tempo Esgotado)
                <br/>
                Se o tempo de MaxRefilTime acabou, o spawner, instantaneamente se dá como concluído.

<br/>

