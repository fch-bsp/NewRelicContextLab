# New Relic Laboratório Log In Context
Resources for FoodMe Lab with log in context

Para acessar o ambiente do EC2, procurar pelo seu nome e copiar o endereço de acesso para a instancia.

[Lista de Acesso para o ambiente EC2](https://docs.google.com/spreadsheets/d/1cfW43Swlm5nCJ3z2q_fuYlbbsd8eGuRWW5MRIK78gxs/edit#gid=1975914412)

Copiar o arquivo *foodme-br.pem* para sua maquina local.



Feedback
Sua opnião importa!

(https://bit.ly/Feedback_NewRelic)

=============================================

1. Instalar Biblioteca Winston
npm init -y

npm i winston
2. Criar o arquivo logger.js no diretório:
/opt/NewRelic-basics-lab-material/FoodMe

logger.js

const winston = require('winston');

const userlogger = winston.createLogger({
    format: winston.format.combine(
        winston.format.errors({ stack: true }),
        winston.format.json()
    ),
    transports: [
            new winston.transports.Console(),
            new winston.transports.File({ filename: 'applog.log' }),
    ],
});
module.exports = userlogger;
3. Importar a biblioteca winston
No arquivo server/index.js inserir no TOPO do arquivo.

const userLogger = require('../logger.js');
4. Criar mensagem de Logs
No arquivo server/index.js configurar algumas mensagens de log, para que apareçam na plataforma

dir: /opt/NewRelic-basics-lab-material/FoodMe

 42.   // API
 43.  app.get(API_URL, function(req, res, next){
 44.    //Loggin NR
 45.    userLogger.info('pagina Home selecionada');
 46.    res.status(200).send(storage.getAll().map(removeMenuItems))
 47.  });
Como ativar ou desativar Log in Context
No arquivo newrelic.js ativar o Log in Context no agente

dir: /opt/NewRelic-basics-lab-material/FoodMe

application_logging: {
     forwarding: {
     enabled: true
    }
