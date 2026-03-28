# Comunicação

## Tipo de comunicação

- Comunicação síncrona.
- Conexões duradouras usando WebSocket.
- O sistema mantém canais abertos enquanto a partida está ativa.

## Protocolo

- Transporte: WebSocket.
- Conexões duradouras entre todos os jogadores.
- Uso de `keepAlive` para verificar se os pares continuam conectados.

## Formato de mensagem

Todas as mensagens seguem o padrão JSON:

```json
{
  "type": "string",
  "seq": 1,
  "data": {}
}
```

### Tipos de mensagem

- `action`: solicita uma ação de jogo (comprar carta, descartar, pular vez, etc.).
- `agree`: confirma que a ação é válida para o nó receptor.
- `disagree`: indica que a ação foi rejeitada.
- `keepAlive`: mantém a conexão ativa e verifica disponibilidade.
- `ACK`: confirma o recebimento de uma mensagem.
- `ERR`: informa um erro no processamento.

## Mensageria por contrato

- Cada mensagem é validada por um middleware antes de qualquer modificação de estado.
- O contrato verifica formato, sequência (`seq`) e consistência lógica.
- Se o contrato falhar, o nó responde com `ERR`.
- Apenas mensagens validadas coletivamente são aplicadas ao estado final.
