# Testes

## Estratégia de testes

- Os testes serão manuais, com foco em pontos específicos da aplicação.
- A validação deve verificar o estado da aplicação e a corretude das mensagens trocadas.
- O ambiente mínimo recomendado é de pelo menos 2 máquinas diferentes.

## Cenários de teste

- Conexão de dois ou mais jogadores em uma sala.
- Envio de uma mensagem `action` e coleta de respostas `agree` / `disagree`.
- Verificação de rejeição quando um nó responde com `disagree`.
- Monitoramento de `keepAlive` e detecção de pares desconectados.
- Conferência da atualização de estado local apenas após consenso completo.

## Pontos específicos a verificar

- Se a mensagem segue o formato JSON esperado.
- Se as mensagens `ACK` são recebidas corretamente.
- Se o middleware rejeita mensagens inválidas.
- Se estados divergentes são tratados adequadamente.

## Observação

- Como o projeto é distribuído, testes em apenas uma máquina não são suficientes.
- É importante replicar a execução em múltiplos dispositivos para avaliar latência, perda de conexão e consistência.
