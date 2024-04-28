# BD III  Bases Tecnológicas

Banco de dados III

**Última revsão: 28/04/2024**

### Bancos de dados não relacionais

**- O termo NoSQL: Ok-2024**
   - Definição: NoSQL é um termo que se refere a um conjunto diversificado de sistemas de gerenciamento de banco de dados (DBMS) que não seguem o modelo tradicional de bancos de dados relacionais. 
   - Origem: O termo "NoSQL" surgiu inicialmente como uma hashtag (#NoSQL) em 2009, durante uma discussão no Twitter sobre sistemas de bancos de dados de código aberto não relacionais. Mais tarde, o termo foi formalizado como "Not Only SQL", indicando que esses sistemas podem oferecer suporte a modelos de dados além do modelo relacional tradicional.
   - Características:
     - Flexibilidade de esquema: Os bancos de dados NoSQL permitem que os desenvolvedores armazenem e manipulem dados sem a necessidade de um esquema rígido.
     - Escalabilidade horizontal: Muitos sistemas NoSQL são projetados para escalar facilmente adicionando mais servidores ao cluster, em vez de aumentar a capacidade de um único servidor.
     - Alta disponibilidade: Muitos sistemas NoSQL são distribuídos e replicam automaticamente os dados para garantir alta disponibilidade e tolerância a falhas.
   - Exemplos iniciais: Alguns dos primeiros sistemas NoSQL incluíam o Apache Cassandra, MongoDB e CouchDB.

**- Motivação: Ok-2024**
   - Exploração de dados não estruturados: Com o crescimento explosivo de dados não estruturados, como texto, imagens e vídeos, os sistemas NoSQL oferecem uma maneira mais flexível de armazenar e consultar esses tipos de dados.
   - Escalabilidade: Com o aumento do volume de dados e o número de usuários, os sistemas tradicionais de bancos de dados relacionais podem ter dificuldades para lidar com a carga. Os sistemas NoSQL foram projetados desde o início para escalabilidade horizontal.
   - Velocidade: Para muitas aplicações, especialmente aquelas que exigem baixa latência e alto throughput, os sistemas NoSQL oferecem desempenho superior em comparação com os bancos de dados relacionais.
   - Modelos de dados variados: Os sistemas NoSQL suportam uma variedade de modelos de dados, incluindo documentos, colunas, chave-valor e grafos, permitindo que os desenvolvedores escolham o modelo mais adequado para suas necessidades.

**- Aplicações: Ok-2024**
   - Redes Sociais: Plataformas de redes sociais como Facebook, Twitter e LinkedIn lidam com grandes volumes de dados gerados por milhões de usuários e interações diárias, tornando os sistemas NoSQL uma escolha natural devido à sua escalabilidade e flexibilidade.
   - Internet das Coisas (IoT): Dispositivos IoT geram enormes quantidades de dados em tempo real, que precisam ser armazenados e processados de maneira eficiente. Bancos de dados NoSQL são frequentemente usados para lidar com esses fluxos de dados em grande escala.
   - Análise de Dados em Tempo Real: Aplicações que exigem análise em tempo real de grandes volumes de dados, como sistemas de recomendação em sites de comércio eletrônico e análise de logs em tempo real, muitas vezes se beneficiam do uso de sistemas NoSQL devido à sua capacidade de lidar com cargas de trabalho intensivas em dados.


### Abordagens e exemplos notáveis de bancos NoSql Ok-2024 conceitual**
**- Documento:** 
Introdução ao modelo de banco de dados de documentos, onde cada registro é um documento JSON ou similar. Exemplos de bancos de dados de documentos incluem MongoDB, CouchDB e RavenDB. Explicar as vantagens deste modelo em termos de flexibilidade e facilidade de escala.

**- Colunar:** 
Apresentação do modelo de banco de dados de colunas, projetado para lidar com grandes volumes de dados e consultas analíticas. Exemplos incluem Cassandra, Bigtable (Google Cloud Bigtable) e DynamoDB (AWS). Destacar a eficiência em leituras de dados em larga escala.

**- Chave-valor:** 
Explicar o modelo de banco de dados chave-valor, onde cada item é armazenado como uma chave única associada a um valor. Exemplos incluem Redis, Amazon DynamoDB (como uma opção chave-valor) e Riak. Destacar a simplicidade e velocidade deste modelo, adequado para armazenamento em cache e sessões de aplicativos.

**- Grafos:** 
Introdução ao modelo de banco de dados de grafos, onde os dados são representados como nós e arestas. Exemplos incluem Neo4j, Amazon Neptune e ArangoDB. Destacar a capacidade deste modelo para representar e consultar relações complexas entre os dados.

### Laboratório de bancos de dados de documentos com MongoDB

**- Criação de bancos de dados e coleções:** Demonstração prática de como criar bancos de dados e coleções no MongoDB.

**- Documentos e campos:** Explicação dos conceitos de documentos e campos no MongoDB, mostrando como inserir e consultar dados.

**- Tipos de dados:** Apresentação dos tipos de dados suportados pelo MongoDB, como string, número, booleano, data, array, entre outros.

**- Modelos de dados Embedded e Normalized:** Comparação entre os modelos de dados embutidos e normalizados no MongoDB, destacando as vantagens e desvantagens de cada abordagem.

**- Operações CRUD (Create, Read, Update, Delete):** Demonstração prática das operações CRUD no MongoDB, incluindo inserção, consulta, atualização e exclusão de documentos.

**- Agregação:** Explicação de como usar a estrutura de agregação do MongoDB para realizar operações de agregação de dados, como agrupamento, filtragem e projeção.


**Ok-2024 => visto e praticado em lab até aqui**



**- Map-Reduce:** Introdução ao conceito de Map-Reduce no MongoDB para processamento paralelo de grandes conjuntos de dados.

**- Transações:** Explicação de como realizar transações no MongoDB para garantir a consistência dos dados em operações que envolvem múltiplos documentos.

**- Índices:** Demonstração de como criar e usar índices no MongoDB para melhorar o desempenho das consultas.

### Tópicos adicionais

**- Conceitos de Big Data:** Introdução aos conceitos fundamentais de Big Data, como volume, velocidade e variedade dos dados, bem como as tecnologias e técnicas para lidar com esses desafios.

**- Conceitos de Ciência de Dados:** 
Exploração dos conceitos básicos de Ciência de Dados, incluindo coleta, limpeza, análise e interpretação de dados para obter insights valiosos e tomar decisões informadas. 
Discussão sobre ferramentas e técnicas comuns, como aprendizado de máquina e visualização de dados.

