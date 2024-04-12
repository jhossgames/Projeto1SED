# Projeto Cruzamento de Carros e Pedestres

## Descrição

Este projeto busca desenvolver um sistema de controle de tráfego eficiente que gerencie o fluxo de pedestres e veículos, minimizando o tempo de espera e evitando congestionamentos no software SUPREMICA, uma ferramenta para modelagem e análise de funções de controle de eventos discretos com base em modelos. Como prioridade fundamental, o sistema foi pensado para garantir a segurança de todos os usuários. 

![Visão Geral](https://raw.githubusercontent.com/jhossgames/Projeto1SED/main/imagens/Captura%20de%20tela%202024-04-12%20003145.png)

## Funcionalidades

- Controle de dois semáforos para carros e dois semáforos para pedestres.
- Sincronismo no sistema entre os semáforos para evitar comportamentos proibidos, como ambos os semáforos ficarem verdes simultaneamente ou um semáforo de carros e um de pedestres ficarem verdes ao mesmo tempo.
- Lógica para permitir que um pedestre possa acionar um botão para fechar o semáforo de carros mais rapidamente, mudando-o de verde para amarelo e prolongando o tempo de fechamento caso já esteja fechado.

## Topologia do Cruzamento

![Topologia do Cruzamento](https://i.imgur.com/49DzwJG.png)

  Para modelagem do sistema, primeiramente foi desenvolvido o diagrama acima, relacionamos os estados de cada semáforo independente com os estados esperados de seus pares, a fim de minimizar erros durante o desenvolvimento. 
  Podemos perceber que nunca dois semáforos estarão permitindo a passagem de fluxo ao mesmo tempo. Assim, temos os seguintes eventos controláveis no sistema:
  - Estágio 1-2: Liberação dos veículos do semáforo 2, Semáforo pedestre 1 liberado;
  - Estágio 2-3: Alerta para os veículos do semáforo 2, preparação para liberação do semáforo 1;
  - Estágio 3-4: Liberação dos veículos do semáforo 1, Semáforo pedestre 2 liberado;
  - Estágio 4-1: Alerta para os veículos do semáforo 2, preparação para liberação do semáforo 1.
    
  Além disso, consideramos que os estágios onde ocorrem o amarelo em algum dos semáforos são estados fundamentais para a segurança dos usuários, portanto, para que não ocorram erros, não sofreram alterações dos eventos não controláveis.   
  Ainda temos eventos não controláveis, como os botões de travessia dos pedestres e o surgimento de veículos de emergência, que podem ser ativados nos seguites estágios:
  - Botão S1:
    - Estágio 4: Botão_S1 aciona a mudança de estágio 4-1;
    - Estágio 2: Botão_S1 aciona a manutenção do estágio 2.
  - Botão S2:
    - Estágio 2: Botão_S2 aciona a mudança de estágio 2-3;
    - Estágio 4: Botão_S2 aciona a manutenção do estágio 4.
  - Emergência no semáforo 1:
    - Estágio 2: Emergência_S1 aciona a mudança de estágio 2-3;
    - Estágio 4: Emergência_S1 aciona a manutenção do estágio 4.
  - Emergência no semáforo 2:
    - Estágio 4: Emergência_S2 aciona a mudança de estágio 4-1;
    - Estágio 2: Emergência_S2 aciona a manutenção do estágio 2.
      
## Construção dos Autômatos

 Com a topologia e os eventos controláveis ou não definidos podemos utilizar o software SUPREMICA para construção dos autômatos de acordo com o funcionamento estabelecidos. Criado um novo projeto e adicionando os eventos, podemos criar as 4 plantas necessárias. Assim temos: 
 
 Autômato do semáforo 1:
 ![automato S1](https://github.com/jhossgames/Projeto1SED/blob/main/imagens/Automatos1.1.png?raw=true)
 
 Autômato do semáforo de pedestres 1:
 ![automato P1](https://github.com/jhossgames/Projeto1SED/blob/main/imagens/AutomatoP1.png?raw=true)
 
 Autômato do semáforo 2:
  ![automato S2](https://github.com/jhossgames/Projeto1SED/blob/main/imagens/AutomatoS2.png?raw=true)
  
   Autômato do semáforo de pedestres 1:
 ![automato P2](https://github.com/jhossgames/Projeto1SED/blob/main/imagens/AutomatoP2.png?raw=true)


## Supervisor Sintetizado
  Com todos as plantas executadas e com o correto funcionamento, podemos utilizar o software para criar o supervisor de forma automatizada. Assim temos:
  
![Supervisor Sintetizado](https://github.com/jhossgames/Projeto1SED/blob/main/imagens/AutomatoSupervis%C3%B3rio.png?raw=true)

  Podemos utilizar o Software para a simulação do supervisório, constatando-se o correto funcionamento do sistemas de semáforos.
  Para a simulação, basta abrir o arquivo Projeto1_SED_Adson_Francisco.wmod no software SUPREMICA, recomenda-se abrir o arquivo diretamente pelo supremica.jar.
  Para visualizar a simulação do supervisório:

  [![Veja a simulação](https://i.imgur.com/XllV2DE.png)](https://youtu.be/ni8EY2Vam8o)

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE). Consulte o arquivo `LICENSE` para obter detalhes.

## Contribuindo

Contribuições são bem-vindas! Sinta-se á  vontade para abrir uma issue ou enviar um pull request.


## Autores

Este projeto foi desenvolvido por:
Ádson Vital Correia (adson.correia@ee.ufcg.edu.br); 

Francisco Olimpio Ferreira da Silva. (francisco.silva@ee.ufcg.edu.br).
