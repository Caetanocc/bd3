## Exemplo de APIs para interagir com MongoBD

Vamos retomar o projeto de exemplo da Introdução ao MongoDB.
Editar o arquivo **server.js** para incluir novas APIs
### 1. API para obter json da collection aluno 

Edite arquivo **server.js** após o bloco **api/data/** incluir o código:

```bash
app.get('/api/alunos', async (req, res) => {
    try {
        // Conectar ao banco de dados MongoDB
        const client = new MongoClient('mongodb://127.0.0.1:27017' );

        await client.connect();
        const db = client.db('Eteclab'); // conectar a base  "Eteclab"

        // Buscar dados das coleções (aluno e professor) - nomes das coleções alterados
        const alunos = await db.collection('aluno').find().toArray(); // obter conteúdo completo da collection "aluno"

        // Encerrar a conexão com o MongoDB
        client.close();

        // Enviar os dados como resposta
        res.json({ alunos });
    } catch (error) {
        console.error('Erro ao buscar dados do MongoDB:', error);
        res.status(500).json({ error: 'Erro ao buscar dados do MongoDB' });
    }
});
```

### 2. API para Postar novo ALUNO na collection aluno 

No arquivo **server.js** após o bloco **api/alunos/** incluir o código:

```bash
// Função para conectar ao MongoDB
async function connectDB() {
    const client = new MongoClient('mongodb://127.0.0.1:27017');
    await client.connect();
    const db = client.db('Eteclab');
    return { client, db };
}

// Rota para criar um novo aluno
app.post('/api/alunos', async (req, res) => {
    try {
        const { nome, ra, curso } = req.body;
        const { db, client } = await connectDB();
        const result = await db.collection('aluno').insertOne({ nome, ra, curso });
        client.close();
        res.json({ message: 'Aluno criado com sucesso', _id: result.insertedId });
    } catch (error) {
        console.error('Erro ao criar aluno:', error);
        res.status(500).json({ error: 'Erro ao criar aluno' });
    }
});

```

### 3. API para DELETAR um aluno

No arquivo **server.js** após o bloco **api/aluno/** incluir o código:

```bash
// Rota para excluir um aluno existente
app.delete('/api/alunos/:id', async (req, res) => {
    try {
        const { id } = req.params;
        const { db, client } = await connectDB();
        const result = await db.collection('aluno').deleteOne({ _id: new ObjectId(id) });
        client.close();
        if (result.deletedCount === 0) {
            res.status(404).json({ message: 'Aluno não encontrado' });
        } else {
            res.json({ message: 'Aluno excluído com sucesso' });
        }
    } catch (error) {
        console.error('Erro ao excluir aluno:', error);
        res.status(500).json({ error: 'Erro ao excluir aluno' });
    }
});

```

### 4. Vamos criar um html para testar as APIs MongoBB

Crie um novo arquivo **cad.html** usando por exemplo esse código

```bash

<!DOCTYPE html>
<html>
<head>
    <title>Exemplo MongoDB</title>
</head>
<body>
    <h1>Lista de Alunos</h1>
    <ul id="aluno-list"></ul>

    <h2>Adicionar Novo Aluno</h2>
    <form id="add-aluno-form">
        <input type="text" id="nome" placeholder="Nome">
        <input type="text" id="ra" placeholder="RA">
        <input type="text" id="curso" placeholder="Curso">
        <button type="submit">Adicionar</button>
    </form>

    <script>
        // Função para buscar dados do MongoDB e exibi-los na página

        async function fetchData() {
            try {
                const response = await fetch("http://127.0.0.1:3000/api/alunos");
                const data = await response.json();
                const alunoList = document.getElementById("aluno-list");
                alunoList.innerHTML = ''; // Limpar lista antes de preenchê-la

                data.alunos.forEach(aluno => {
                    const listItem = document.createElement("li");
                    listItem.textContent = `${aluno.nome} - Idade: ${aluno.ra}, Curso: ${aluno.curso}`;

                    const deleteButton = document.createElement("button");
                    deleteButton.textContent = "Excluir";
                    deleteButton.addEventListener("click", () => deleteAluno(aluno._id));

                    listItem.appendChild(deleteButton);
                    alunoList.appendChild(listItem);
                });
            } catch (error) {
                console.error("Erro ao buscar dados:", error);
            }
        }


        // Função para adicionar um novo aluno
        async function addAluno(event) {
            event.preventDefault();
            const nome = document.getElementById("nome").value;
            const idade = document.getElementById("ra").value;
            const curso = document.getElementById("curso").value;

            try {
                await fetch("http://localhost:3000/api/alunos", {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({ nome, idade, curso }),
                });

                // Limpar campos do formulário
                document.getElementById("nome").value = "";
                document.getElementById("ra").value = "";
                document.getElementById("curso").value = "";

                // Recarregar a lista após a adição
                fetchData();
            } catch (error) {
                console.error("Erro ao adicionar aluno:", error);
            }
        }

        // Função para excluir um aluno
        async function deleteAluno(id) {
            try {
                await fetch(`http://localhost:3000/api/alunos/${id}`, {
                    method: "DELETE",
                });

                // Recarregar a lista após a exclusão
                fetchData();
            } catch (error) {
                console.error("Erro ao excluir aluno:", error);
            }
        }

        // Chamar a função fetchData para carregar os dados iniciais
        fetchData();

        // Adicionar um ouvinte de evento para o formulário de adição de aluno
        document.getElementById("add-aluno-form").addEventListener("submit", addAluno);
    </script>
</body>
</html>


```

### 5. Fazer testes com cad.html para validar o acesso aos dados e incluir e excluir alunos.

### 6. Melhorar o código, separar a parte javascript em arquivos.











