# Wiki do Uno Distribuído

Bem-vindo à wiki do projeto Uno Distribuído. Esta documentação está organizada em páginas separadas para facilitar a leitura e a manutenção.

## Páginas disponíveis

- [Arquitetura](Arquitetura.md)
- [Comunicação](Comunicacao.md)
- [Testes](Testes.md)
- [Diagrama de Sequência](DiagramaSequencia.md)

## Sobre o projeto

Uno Distribuído é um protótipo de jogo de Uno que explora uma arquitetura peer-to-peer com validação de estado por contrato. O projeto utiliza Electron, React e TypeScript, e mantém conexões duradouras via WebSocket para sincronização entre jogadores.

## Objetivos principais

- Permitir que vários jogadores participem de uma partida distribuída.
- Validar ações em consenso antes de modificar o estado do jogo.
- Estudar a aplicação de modelos de comunicação distribuída em uma aplicação desktop.
- Testar o sistema utilizando pelo menos duas máquinas diferentes para simular rede real.
