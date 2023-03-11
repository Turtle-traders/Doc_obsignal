### Documentação da API de WebSocket - OBSIGNAL
Este é um guia para utilização da API de WebSocket da plataforma OBSIGNAL.

#### Conexão
Para se conectar à API, utilize a URL abaixo:

`wss://obsignal.agbot.com.br/client`
A autenticação deve ser realizada mediante token de autentificação no formato abaixo:

`**********`
É importante salientar que todas as requisições devem ser enviadas em formato JSON.

Cadastro de recebimento de mensagem
Para receber mensagens da API, você deve realizar um cadastro indicando o seu nome através de uma mensagem JSON.

Exemplo:

`{'name': 'munna'}`
Os dados de mensagens recebidas estarão em formato JSON.

Troca de Timeframe
Caso deseje alterar o timeframe atual, é possível enviar um JSON com os seguintes dados:

`{'name': 'timeframe', 'data': 'M5'}`
O valor da chave 'data' pode ser M1 ou M5.

#### Mensagens Recebidas
Ao se inscrever para receber mensagens, algumas informações importantes serão enviadas pelo WebSocket. Essas informações são estruturadas
de acordo com dados chamados de "instance", que podem ajudá-lo identificar a origem dos sinais. Os dois tipos de instâncias são "cache_signal" e "signal".

##### Cache_signal
Este tipo de comando apresenta os sinais em cache da API.
Esta notificação compartilha todos os sinais armazenados, com exceção dos sinais concluídos. Ele tem geralmente este formato:

Exemplo:

```
{
  "instance": "cache_signal",
  'ok': 'true',
  'message': {
    "1": {
        "strategie": "AG-MVP", 
        "active": "EUR/USD", 
        "hour":"05:00", 
        'direction': "CALL", 
        "timeframe": "M5", 
        "result": "waiting",
        "martigale": 'G0', 
        'date':"2023-02-24 18:59",
        'status': {'color': 'green', 
                'bars': '////', 
                'porcent': 87.27}
    },
    "2": {
        "strategie": "AG-MVP", 
        "active": "AUD/USD", 
        "hour":"06:00", 
        'direction': "CALL", 
        "timeframe": "M5", 
        "result": "waiting",
        "martigale": 'G0', 
        'date':"2023-02-24 18:59",
        'status': {'color': 'green', 
                'bars': '////', 
                'porcent': 87.27}
    }
}

```

Onde "1" e "2" representam o card_id, a chave e dentro dessa chave haverão dados para renderizar o seu site.

##### Signal
Este tipo de comando indica que houve modificações nos sinais, incluindo novos sinais, bem como sinais antigos modificados (que estão em situação de martingale). É importante salientar que as informações sobre "martingale" e "resultado" podem mudar ao longo do tempo.

Exemplo:

```
{
  "instance": "signal",
  
  "card_id": 1,
  "card": {
    "strategie": "AG-MVP", 
    "active": "EUR/USD", 
    "hour":"05:00",
    'direction': "CALL", 
    "timeframe": "M5", 
    "result": "waiting",
    "martigale": 'G0',
    'date':"2023-02-24 18:59",
    'status': {'color': 'green', 
               'bars': '////', 
               'porcent': 87.27}
  }
}

```

