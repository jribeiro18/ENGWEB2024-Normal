Análise do conjunto de dados

Ao analisar o conjunto de dados, notei que este estava num formato diferente do JSON (CSV) e que o campo "idcontrato" deveria ser renomeado para "_id" para evitar conflitos com o MongoDB.

Também observei que existiam campos com valores numéricos que estavam a ser interpretados como strings, o que poderia causar problemas mais tarde. Consequentemente, converti os campos "precoContratual" para float e "prazoExecucao" e "_id" para inteiros. 

Estes passos foram todos realizados através do ficheiro "script.py"

Configuração do MongoDB:

Para começar, criei o container "mongoEWTeste" com o comando:
sudo docker run -d -p 27017:27017 --name mongoEWTeste mongo

Para configurar o MongoDB, utilizei o Docker, copiando o conjunto de dados para o container com o comando:
docker cp contratos2024.json mongoEWTeste:/tmp

Em seguida, carreguei o conjunto de dados para o MongoDB com o comando:
docker exec mongoEWTeste mongoimport -d contratos -c contratos /tmp/contratos2024.json --jsonArray

Testes no MongoDB:

Para verificar se os dados foram carregados corretamente, executei as consultas conforme descrito no ficheiro "queries.txt", localizado na pasta "ex1".

API de dados:

Para criar a estrutura inicial da API, utilizei o Express com o seguinte comando:
npx express-generator --no-view ex1

Posteriormente, criei modelos e controladores para interagir com o MongoDB e rotas em "routes/contratos.js". Configurei o Mongoose em "app.js" e instalei as dependências necessárias com os comandos:
npm install
npm install mongoose

Para iniciar, executa-se o comando:
npm start

Para criar a estrutura inicial da interface com pug utilizei o comando:
npx express-generator --view=pug ex2

Após criar os ficheiros necessários dentro da pasta view, e executar os comandos npm feitos em cima, é possível inicializar a interface.

Acedi à interface no navegador, verificando se os dados eram carregados corretamente.
