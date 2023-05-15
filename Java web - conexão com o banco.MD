
## Roteiro da Aula
### CONECTANDO UMA APLICAÇÃO JAVA A UM BANCO DE DADOS DO JEITO CERTO

#### Objetivo geral

 - Conhecer os principais recursos para acesso a um bancos de dados (teoria e prática); 
 - Elaborar a estrutura básica de um projeto;
 - Implementar o padrão Repository com Java

#### Visão geral

A conexão com bancos de dados é uma etapa essencial para muitos projetos de desenvolvimento de software, seja para armazenar informações do usuário, gerenciar estoques de produtos ou fornecer dados para análises de negócios. Nesse contexto, compreender como conectar uma aplicação a um bancos de dados é fundamental.. Neste texto, discutiremos os principais conceitos e técnicas envolvidos na conexão de uma aplicação Java com bancos de dados, abordando desde as bibliotecas Java mais utilizadas até as melhores práticas de segurança e performance.

#### Java Database Connectivity - JDBC

Uma das principais ferramentas utilizadas para conectar o Java a bancos de dados é o JDBC (Java Database Connectivity). O JDBC é uma API do Java que oferece um conjunto de classes e métodos para conectar e interagir com bancos de dados relacionais. Ele fornece uma maneira padronizada de se comunicar com diferentes bancos de dados, independentemente do sistema operacional ou do tipo de banco de dados utilizado.

A utilização do JDBC é essencial para os programadores Java que precisam trabalhar com bancos de dados relacionais (e alguns não relacionais). Espera-se que com uma compreensão sólida desse fundamento, os desenvolvedores possam criar aplicações eficientes e escaláveis, com um mínimo de segurança.

Na prática, o **JDBC funciona como uma ponte**, ou seja, é **uma camada intermediária entre a aplicação e o banco de dados**. Ele realiza a interpretação e a conversão dos comandos necessários para a manipulação do banco de dados, de acordo com as características de cada um. Isso porque, apesar de todos os bancos de dados relacionais utilizarem a linguagem SQL — Structured Query Language —, existem diferenças entre as diversas bases existentes no mercado. Portanto, o JDBC é uma ferramenta responsável por realizar essa comunicação, conforme o banco acessado pela aplicação.

É importante destacar que é preciso utilizar o driver JDBC de acordo com a base de dados utilizada, ou seja, se formos utilizar um banco MySQL, devemos usar o JDBC apropriado para ele. Por isso, cada empresa desenvolvedora de banco de dados disponibiliza o seu próprio driver para ser utilizado no Java.

#### Recursos necessários:

 - Instalar o MySQL Server Instalar MySQL Workbench (ou outro gestor
 - visual de banco de dados de seu domínio)

#### Preparação do primeiro Projeto

##### Checklist:

 - Usando o MySQL Workbench, crie uma base de dados chamada "ifpr_store";
 - Popule seu banco de dados usando este script;
 - Certifique-se que seu banco de dados funciona realizando consultas e inserções; 
 - Criar um novo Projeto Java; 
 - Inclua a biblioteca  MySQL Connector ao projeto (arquivo jar ou incluindo a dependência no POM.xml);
 - Crie um pacote chamado connection;
 -- No pacote "connection", crie uma classe ConnectionFactory;
 - Crie um pacote chamado exceptions; 
 -- No pacote "exceptions", criar uma exceção personalizada DatabaseException 
 - Crie um pacote chamado repository; 
 -- Neste pacote crie uma classe chamada SellerRepository;
 -- Crie uma outra classe chamada DepartmentRepository;
 - Obtenha e fechar uma conexão com o banco de dados

##### Opcional:
- Na pasta raiz do projeto, criar um arquivo "db.properties" contendo os dados de conexão:
-- user=root  password=bancodedados
-- dburl=jdbc:mysql://localhost:3306/ifpr_store;useSSL=false

### Operação 1: Fábrica de Conexões
---
Material de apoio: Código Java

Ao utilizar o JDBC, devemos passar os dados necessários para fazer a conexão com o banco, tais como usuário, senha e nome do banco e as instruções SQL para realizar as operações na base, entre elas, inclusão, alteração, pesquisa ou exclusão de registros. Uma das formas de se fazer uma conexão é criar um método para retornar o resultado dessa operação. A vantagem de criar um método para fazer a conexão é que poderemos reutilizá-lo outras vezes na aplicação. Assim, atendemos aos princípios da programação orientada a objeto de reaproveitamento de código. Confira o método, a seguir:



No exemplo acima, o método getConnection realiza a conexão com o banco de dados e retorna um objeto do tipo Connection, que representa e contém os dados dessa conexão. O método getConnection  deverá ser utilizado sempre que uma conexão com o banco de dados for necessária.

### Operação 2: recuperar dados
---
