
# MongoDB introdução

### 1.Abra o MongoDB Compass e crie novo database
Clique no botão **"New Connection"** para se conectar ao servidor MongoDB local (geralmente, você pode usar a configuração padrão: host localhost e porta 27017).
Após se conectar, clique em **"Create Database"** e crie um novo banco de dados chamado **"EtecLab"**.

### 2.Criar 2 collections:  aluno (nome, rm, curso) e professor (nome, cpf, datanasc) .

### 3. Criar servidor node express para acesso ao MongoDB

criação de um servidor para fornecer os dados do MongoDB e configurar a API local. 
Para isso, vou usar Node.js e Express.js como exemplo.

** Configuração do Servidor Node.js com Express.js**

1. Certifique-se de que você tem o Node.js instalado em seu sistema. Você pode verificar a instalação digitando o seguinte comando no terminal:

   ```bash
   node -v
   ```

   Se não estiver instalado, você pode baixá-lo e instalá-lo no site oficial do Node.js: https://nodejs.org/

2. Crie uma pasta para o seu projeto e navegue até ela no terminal:

   ```bash
   mkdir exercicio-mongodb
   cd exercicio-mongodb
   ```

3. Inicialize um projeto Node.js executando o seguinte comando:

   ```bash
   npm init -y
   ```

   Isso criará um arquivo `package.json` que conterá as informações do seu projeto.

4. Instale as dependências necessárias, incluindo o Express.js e o driver MongoDB para Node.js:

   ```bash
   npm install express mongodb
   ```

   instale a biblioteca `cors` necessária para app web acessar o server node.js :

  ```bash
  npm install cors
  ```
   

5. Crie um arquivo JavaScript chamado `server.js` na sua pasta do projeto e adicione o seguinte código:

   ```bash
      const express = require('express');
      const app = express();
      const { MongoClient } = require('mongodb');
      const cors = require('cors'); // Importe o módulo cors
      const port = process.env.PORT || 3000;
      
      // Use o middleware cors para permitir solicitações de qualquer origem
      app.use(cors());

      // Middleware para lidar com JSON
      app.use(express.json());

      // Rota para buscar dados do MongoDB
      app.get('/api/data', async (req, res) => {
          try {
              // Conectar ao banco de dados MongoDB
              const client = new MongoClient('mongodb://localhost:27017');
              await client.connect();
              const db = client.db('Eteclab'); // Alterado para "Eteclab"
      
              // Buscar dados das coleções (aluno e professor) - nomes das coleções alterados
              const alunos = await db.collection('aluno').find().toArray(); // Alterado para "aluno"
              const professores = await db.collection('professor').find().toArray(); // Alterado para "professor"
      
              // Encerrar a conexão com o MongoDB
              client.close();
      
              // Enviar os dados como resposta
              res.json({ alunos, professores });
          } catch (error) {
              console.error('Erro ao buscar dados do MongoDB:', error);
              res.status(500).json({ error: 'Erro ao buscar dados do MongoDB' });
          }
      });
      
      // Iniciar o servidor
      app.listen(port, () => {
          console.log(`Servidor rodando na porta ${port}`);
      });
   ```

**Nota importante**: Certifique-se de que o MongoDB está em execução no mesmo host e porta que você especificou na conexão (`'mongodb://localhost:27017'` neste exemplo).

### 4 Iniciar o Servidor**

Para iniciar o servidor, vá para o diretório do projeto no terminal e execute o seguinte comando:

```bash
node server.js
```
Isso iniciará o servidor na porta especificada (3000, neste exemplo).

### 5. Criar app web  HTML para listar as coleções "aluno" e "professor" 

```html
<!DOCTYPE html>
<html>
<head>
    <title>Exemplo MongoDB</title>
</head>
<body>
    <h1>Lista de Alunos</h1>
    <ul id="aluno-list"></ul>

    <h1>Lista de Professores</h1>
    <ul id="professor-list"></ul>

    <script>
        // Função para buscar dados do MongoDB e exibi-los na página
        async function fetchData() {
            try {
                const response = await fetch("http://localhost:3000/api/data");
                const data = await response.json();

                // Exibindo alunos
                const alunoList = document.getElementById("aluno-list");
                data.alunos.forEach(aluno => {
                    const listItem = document.createElement("li");
                    listItem.textContent = aluno.nome;
                    alunoList.appendChild(listItem);
                });

                // Exibindo professores
                const professorList = document.getElementById("professor-list");
                data.professores.forEach(professor => {
                    const listItem = document.createElement("li");
                    listItem.textContent = professor.nome;
                    professorList.appendChild(listItem);
                });
            } catch (error) {
                console.error("Erro ao buscar dados:", error);
            }
        }

        fetchData();
    </script>
</body>
</html>
```

### 6. Execute o arquivo Web 

De preferência use vscode para editar esse arquivo, pode fazer melhorias, como separar o javascript.

Execute com GoLive ou semelhante para ver o resultado.
Deve mostrar o conteúdo das collections professor e aluno do MongoDB.


