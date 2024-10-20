# O que será abordado nesse Projeto
- Acesso ao banco de dados MySQL, usando JDBC
- O que é JDBC
- Álgebra Relacional
- O Uso de Libraries

# Acesso ao banco de dados JDBC

- **JDBC(Java Database Connectivity)**: é a API padrão do Java para acesso a dados, atraves do **JDBC Driver Manager**, que pega o código desenvolvido e o converter de acordo com banco de dados escolhido.
- Toda interface no **JDBC** ganha sua implementação atraves do **JDBC Driver Manager**

- **Álgebra relacional**: é um formalismo que define operações dentro do modelo relacional, as operações básicas são,
 `restricão`, `projeção`, `produto cartesiano`, `junção(produto cartesiano + restrição de chaves correspondentes)`
 
# Todos os códigos aqui partiram do jdbc1, mas ganharam incrementos correspondentes a cada exemplo
-  Nessa parte do projeto é criada a classe `DBException`, para criar uma exceção personalizada, e a classe `DB` que ajuda a simplificar o uso da `Connection`.
- A classe `DB` gerencia a conexão com o banco de dados. Ela fornece métodos estáticos para abrir e fechar conexões, além de carregar as propriedades do banco de dados a partir de um arquivo externo. O método `getConnection`  verifica se já existe uma conexão ativa e, se não, carrega as propriedades necessárias e estabelece a conexão. O método `closeConnection` fecha a conexão aberta, se existir. O método `loadProperties` carrega as configurações do banco a partir de um arquivo de propriedades, garantindo que os parâmetros de conexão estejam devidamente configurados.
-  A interface `Connection` é fundamental no gerenciamento de conexões com o banco de dados. Nesse cenário, a classe `DB` serve como uma camada de conveniência que encapsula a lógica de criação e gerenciamento de uma instância de `Connection`. Quando se chama `DB.getConnection()`, ocorre a utilização da lógica da `DB` para obter uma instância da `Connection`, que então será utilizada para enviar consultas SQL, atualizar dados, etc. 
  A `Connection` em si é responsável por:
  Abrir e Manter a Conexão: Estabelece e mantém a comunicação ativa com o banco de dados.
  Criar Statements: Permite criar declarações SQL (`Statement`, `PreparedStatement` e `CallableStatement`).
  Gerenciar Transações: Comandos como `commit` e `rollback` para transações.
  Fechar Conexão: Fecha a conexão quando não é mais necessária.

**jdbc2**: Nessa parte do projeto é mostrado como se fazer consultas SQL com Java, utilizando as interfaces `Statement` que permite a criação de comandos `SQL`, e a  `ResultSet` que traz os dados em forma de tabelas. A classe `DB` possui dois novos métodos para evitar vazamento de memória: `closeStatement`, que fecha um `Statement` passado como parâmetro, e `closeResultSet`, que fecha um `ResultSet` passado como parâmetro. Ambos métodos verificam se os objetos não são nulos antes de tentar fechá-los e lidam com possíveis exceções lançando `DbException`.

**jdbc3**: Nessa parte do projeto é mostrado como se faz para inserir dados no banco de dados

**jdbc4**: Nessa parte do projeto é mostrado como faz para atualizar dados

**jdbc5**: Nessa parte do projeto é mostrado como faz para deletar dados, não houve incremento na classe `DB`, houve a criação da classe `DbIntegrityException` para mostrar problemas na integridade referencial do banco de dados

**jdbc6**: Nessa parte do projeto é mostrado como fazer transações, é usado funções como `setAutoCommit`, `commit` e `rollback` da interface `Connection` para garantir a integridade das transações. Usando métodos como `setAutoCommit(false)` para desativar o commit automático, permitindo que múltiplas operações sejam agrupadas em uma única transação. Isso nos dá controle sobre quando realizar o `commit` ou o `rollback`, garantindo que as operações sejam concluídas com sucesso antes de confirmar a transação, ou revertendo todas as operações caso ocorra algum problema.

# Como usar: 
  - Clone o repositório
  - Usando o MySQL Workbench, crie uma base de dados chamada "coursejdbc"
  - Baixar o MySQL Java Connector
  - Caso ainda não exista, criar uma User Library contendo o arquivo .jar do driver do MySQL
    - Window -> Preferences -> Java -> Build path -> User Libraries
    - Dê o nome da User Library de MySQLConnector
    - Add external JARs -> (localize o arquivo jar)
  - Certifique-se que o arquivo `db.properties` contém as informações corretas da sua conexão com o MySQL
    - user=developer
    - password='suasenhaaqui'
    - dburl=jdbc:mysql://localhost:3306/coursejdbc
    - useSSL=false