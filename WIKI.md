# Uno Distribuído

## Visão Geral

Uno Distribuído é um protótipo de jogo de Uno que explora uma arquitetura peer-to-peer com controle de estado por contrato em uma aplicação desktop moderna. O objetivo é permitir que vários jogadores participem de uma partida distribuída usando Electron, React e TypeScript, com troca de mensagens em tempo real via WebSocket.

## Objetivo do Projeto

- Construir um sistema de Uno em que cada jogador mantenha uma cópia local do estado do jogo.
- Implementar validação de ações por consenso entre os pares antes de aplicar qualquer mudança de estado.
- Estudar e aplicar um modelo de comunicação distribuída baseado em contrato.
- Garantir que a execução seja feita em duas ou mais máquinas para testar comportamento real de rede.

## Limitações Conhecidas

- Potencialmente, cada jogador pode ver a mão de outro jogador e o baralho.
- Isso indica que o protótipo ainda não resolve totalmente problemas de privacidade e confidencialidade de estado.
- O foco atual é validar a arquitetura de mensagens e o consenso, não em criptografia de dados ou ocultação de informações.

## Modelo Estudado e Escolhido

- Modelo estudado: Peer to Peer.
- Modelo adotado: Peer to Peer com um papel de controle centralizado dentro da sala.
- O sistema funciona com cada participante sendo um nó ativo que replica e concorda com o estado do jogo.

## Arquitetura de Software Interna

- Plataforma: Electron.
- Interface: React com TypeScript.
- Comunicação: WebSockets persistentes.
- Arquitetura de mensageira por contrato:
  - Cada ação de jogo é enviada como mensagem para todos os pares.
  - A ação só é aplicada localmente após receber a confirmação de todos os jogadores.
  - Existe um middleware que valida contratos de mensagem antes de modificar o estado final.

## Papéis e Funções

- Um jogador assume a `Role` de controlador da sala.
- Esse controlador é responsável por gerenciar a lista de IPs dos jogadores conectados.
- Ele também pode ser usado para coordenar a criação de salas e a descoberta inicial de pares.
- Mesmo com um controlador, o fluxo de decisão depende do consenso de todos os jogadores.

## Comunicação

### Tipo de comunicação

- Comunicação síncrona.
- Conexões duradouras usando WebSocket.
- O sistema mantém canais abertos enquanto a partida está em execução.

### Protocolo

- Transporte: WebSocket.
- Conexões: duradouras, com heartbeat/keepAlive para garantir disponibilidade.
- O protocolo é leve, orientado a eventos e em formato JSON.

## Formato de Mensagens

Todas as mensagens seguem o padrão JSON:

```json
{
  "type": "string",
  "seq": 1,
  "data": {}
}
```

### Tipos de mensagem

- `action`: solicita uma ação de jogo (comprar carta, descartar, etc.).
- `agree`: confirma que a ação é válida e aceita pelo nó receptor.
- `disagree`: indica que a ação foi rejeitada por algum motivo.
- `keepAlive`: mantém a conexão ativa e verifica se o par ainda está online.
- `ACK`: confirma o recebimento de uma mensagem.
- `ERR`: informa um erro no processamento da mensagem.

## Validação e Middleware

- Antes de qualquer modificação de estado final, o middleware executa validação de contrato.
- As mensagens são verificadas quanto a formato, sequência e correção lógica.
- Se o contrato falhar, a mensagem é rejeitada e um `ERR` é devolvido.
- Somente após validação e aceitação coletiva o estado do jogo é atualizado.

## Testes

- Os testes serão manuais, focados em pontos específicos da aplicação.
- A validação inclui verificar o estado da aplicação e a corretude das mensagens trocadas.
- Os testes exigem pelo menos 2 máquinas diferentes para simular uma rede real e conexões distribuídas.

### Cenários de teste

- Conexão de dois ou mais jogadores.
- Envio de uma ação e recepção de `agree` / `disagree` de todos os pares.
- Identificação e tratamento de pares desconectados.
- Checagem de `keepAlive` e revalidação de estado após reconexão.

## Diagrama de Sequência (Definição)

A seguir está a definição lógica do fluxo de mensagens entre os componentes principais:

1. `Jogador A` envia `action` para todos os pares.
2. Cada par recebe a mensagem e executa a validação local via middleware.
3. Cada par responde com `agree` ou `disagree`.
4. `Jogador A` coleta todas as respostas.
5. Se todas as respostas forem `agree`, o estado do jogo é atualizado localmente e uma confirmação final pode ser difundida.
6. Se houver ao menos um `disagree`, a ação é abortada e o motivo é propagado.
7. Enquanto isso, mensagens `keepAlive` podem ser trocadas para manter as conexões vivas.

## Caminho Futuro e Melhorias

- Implementar proteção adicional para mãos e baralho, reduzindo exposição de informações.
- Evoluir para um consenso mais robusto, talvez com tolerância a falhas parciais.
- Adicionar testes automatizados de integração para o protocolo de mensagens.
- Incluir lógica de descoberta de jogadores sem depender exclusivamente de IPs estáticos.

## Conclusão

Este projeto é um estudo técnico sobre como construir um jogo distribuído de Uno usando Electron + React + TypeScript e uma arquitetura peer-to-peer baseada em contratos. Ele foca em garantir que cada ação seja validada coletivamente antes de alterar o estado do jogo, com conexões duradouras por WebSocket e um jogador controlador para coordenar os pares.
