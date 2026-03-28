# Arquitetura do Uno Distribuído

## Visão geral da arquitetura

A arquitetura do Uno Distribuído é centrada em uma aplicação desktop construída com Electron, React e TypeScript. O sistema usa WebSockets persistentes para comunicação entre nós em uma rede peer-to-peer.

## Componentes principais

- Electron: ambiente desktop que abriga a aplicação.
- React com TypeScript: interface de usuário e lógica de componentes.
- WebSocket: canal de comunicação contínuo entre jogadores.
- Middleware de validação: responsável por garantir que as mensagens respeitem o contrato antes de alterar o estado.

## Modelo de execução

- Cada jogador é um nó ativo que mantém seu próprio estado local do jogo.
- Para executar uma ação, o jogador envia uma mensagem de `action` para todos os pares.
- A ação só é aplicada após os outros jogadores confirmarem a validade com mensagens `agree`.
- Se um ou mais jogadores enviarem `disagree`, a ação é rejeitada.

## Role de controlador de sala

- Existe um jogador com a `Role` de controlador da sala.
- Esse controlador gerencia a lista de IPs dos participantes.
- Ele facilita a descoberta inicial dos pares e a organização da sala.
- No entanto, a decisão final ainda depende do consenso de todos os jogadores.

## Limitações do modelo

- Potencialmente, cada jogador pode ver a mão de outro jogador e o baralho.
- O projeto ainda não implementa mecanismos completos de privacidade de estado.
- O foco atual é validar a troca de mensagens e o processo de consenso.
