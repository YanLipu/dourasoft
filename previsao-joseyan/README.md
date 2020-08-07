# Aplicação de Previsão do Tempo

Desenvolvi essa aplicação usando o framework Quasar. O primeiro passo foi criar uma interface onde as informações de 
previsão do tempo iam ser mostradas. Em seguida precisei aprender como lidar com API's e como tratar os dados recebidos;
A API utilizada foi da OpenWeather(https://openweathermap.org/forecast5). A API retorna as informações de previsão do tempo
divididas de 3 em 3 horas, ou seja, retorna um array de tamanho 40. Então separei o array em 5, para mostrar a previsão do dia 
atual e dos proximos 4 dias.

## Instale as dependencias
```
npm install -g @quasar/cli
```

### Iniciar a aplicação em modo dev
```
quasar dev
```

## Caso não inicie automaticamente
 
 ``http://localhost:8080/#``
 
## Coloquei a aplicação no Netlify

``https://wizardly-colden-d3aa2f.netlify.app/#/``
