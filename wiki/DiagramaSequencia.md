# Diagrama de Sequência

## Definição do fluxo de sequência

A sequência de mensagens descreve o processo de validação e aplicação de uma ação no jogo.

1. `Jogador A` envia mensagem `action` para todos os pares.
2. Cada par recebe a mensagem e executa a validação local via middleware.
3. Cada par retorna `agree` ou `disagree`.
4. `Jogador A` colet a resposta de todos os pares.
5. Se todas as respostas forem `agree`, a ação é aplicada localmente e o estado do jogo é atualizado.
6. Se houver pelo menos um `disagree`, a ação é abortada e o motivo é comunicado.
7. Paralelamente, mensagens `keepAlive` circulam para manter as conexões ativas.

## Objetivo do diagrama

- Mostrar o caminho de uma ação válida até a atualização de estado.
- Registrar o comportamento do protocolo de consenso.
- Evidenciar pontos de falha e rejeição de ações.

## Observações

- O diagrama pressupõe que todos os pares recebem a mesma mensagem de `action`.
- A etapa de validação deve incluir checagem de formato, sequência e regras de jogo.
- O controle final do estado só ocorre após o consenso de todos os jogadores.
