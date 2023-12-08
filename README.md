## Comandos para manipular o banco de dados - Mysql

### Acessando o Mysql com permissões de root

Com acesso ssh do seu servidor do mysql, digite o seguinte comando ```mysql -u [usuario] -p``` e tecle enter, a senha será solicitada, a partir deste momento você pode usar qualquer comando MySql para navegar pelos bancos.

 - ```SHOW DATABASES;``` // Mostra todos os bancos
 - ```USE alunos_do_erik``` // Acessa o banco de dados
 - ```SHOW TABLES;``` // Mostra as tabelas no banco atual
 - ```DESCRIBE TABLE [NOME DA TABELA];``` // Descreve uma tabela

Você também pode usar os famosos comamandos SELECT, INSERT, UPDATE e DELETE, assim como qualquer outro comando SQL.

### Fazendo o backup

No terminal rode um comando parecido com o ```mysql```, chamado ```mysqldump```, para fazer o backup de um banco de dados listando a saída na tela, mas use isso apenas como referência por enquanto.

 - ```mysqldump -u [usuario] -p [nome do banco]```

Executado o comanado no terminal irá parecer diversas informações, pode demorar e se for muito grande o banco, até travar, a melhor saída é armazenar tudo em um arquivo, para isso usamos um recurso no próprio linux:

 - ```mysqldump -u [usuario] -p [nome do banco] > [nome do arquivo].sql```
 - ```mysqldump -uroot -p [nome do banco] > [nome do arquivo].sql```

O backup é até mais rápido assim.

Um exemplo com o banco alunos, o usuário é alunos e a senha 123:

 - ```mysqldump -u alunos -p alunos_do_erik > alunos_db_bkp.sql```

A senha do banco será solicitada e o arquivo alunos_db_bkp.sql será criado no diretório que você estiver atualmente, eu recomando que você faça isso em um local que o ftp possa acessar, por exemplo a raiz do ftp do spp, para acessar este diretório rode o seguinte comando:

 - ```cd /home/super```

### Restaurando Backup 

O processo é semelhante ao comando usado para fazer backup, mas existe um detalhe que faz a total difirença e que as pessoas costuma esquecer, retire o comando mysqldump e deixa assim:

 - ```mysql -u alunos -p alunos < alunos_db_bkp.sql```

Agora aguarde o backup ser restaurado e depois ao terminar o restore, verifique nas tabelas do backup restaurado se os dados estão recuperados.


## Comandos básicos SQL para banco de dados MYSQL

create database - // cria o banco.

use <nome-do-banco> - // usado para selecionar o banco que vc vai manipular.

####  CREATE TABLE
create table - // usado para criar uma tabela.


    create table vendas (
    id_venda INT,
    Curso VARCHAR(45),
    Valor DECIMAL(10,2)
    Estado VARCHAR(2)
    );

#### INSERT INTO
insert into - // usado para inserir dados.

    inser into vendas (id_venda, Curso, Nome, Valor, Estado) value (1, 'ADS', 999, 'CE');

#### SELECT

select * from - //usado para exibir as colunas da tabela.

    select * from vendas;

#### UPDATE
    UPDATE vendas SET Valor = 1500 where = 'SP' ; - usado para atualizar algum dado das colunas da tabela.

#### DELETE
DELETE FROM vendas where id_venda = 10; - Usado para deletar algum registro da tabela.

### Funções
order by - Função usada para ordenar os dados.
ASC - Função combinada com order by, os dados de uma coluna em ordem crescente. 
DESC - Função combinada com order by, os dados de uma coluna em ordem decrescente.
where - Função para filtar dados de uma coluna.

Exemplo:

    select * from Vendas WHERE Estado = 'CE' ;

 - TRUNCATE TABLE - // nome da tabela - Usado para zerar a tabela 
 - DROP   TABLE nome da tabela - // deletar a tabela toda 
 - DROP DATABASE nome do  banco - // Deletar o banco de dados todo 
 - SHOW DATABASES - // Mostra os bancos
 - SHOW TABLES; - // Mostra as tabela de um banco de dados  selecionado 
 - INNER JOIN - // Usado para fazer um consulta de duas tabelas ou mais.

### Usando INNER JOIN
    SELECT * FROM tbl_Livro
    INNER JOIN tbl_autores
    ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor; 

// Relacionamento entre as tabelas - Chave estrangeira

### Outra maneira de função INNER JOIN

    SELECT tbl_Livro.Nome_Livro, tbl_Livro.ISBN, tbl_autores.Nome_Autor
    FROM tbl_Livro
    INNER JOIN tbl_autores
    ON tbl_Livro.ID_Autor = tbl_autores.ID_Autor;

    SELECT L.Nome_Livro AS Livros, E.Nome_editora AS Editoras
    FROM tbl_Livro AS L
    INNER JOIN tbl_editoras AS E
    ON L.ID_editora = E.ID_editora
    WHERE E.Nome_Editora LIKE 'M%';

    SELECT L.Nome_Livro AS Livro,
    A.Nome_autor AS Autor,
    E.Nome_Editora AS Editora,
    L.Preco_Livro AS 'Preço do Livro'
    FROM tbl_Livro AS L
    INNER JOIN tbl_autores AS A
    ON L.ID_autor = A.ID_autor
    INNER JOIN tbl_editoras AS E
    ON L.ID_editora = E.ID_editora
    WHERE E.Nome_Editora LIKE 'O%'
    ORDER BY L.Preco_Livro DESC;


### Exportando ou Backup do bando de dados

> Usando o comando msqldump 
para extrair dados com as tabelas, o banco todos.

    mysqldump -h HOST -u User -p PASSWORD nome-do-banco > nome-do-arquivo-sql-gerado.sql

### Importando o banco

> Usando o comando msql sem o dump
para importar dados com as tabelas, o banco todos.

    mysql -h HOST -u USER -p PASSWORD --default_character_set utf8 nome-do-banco <nome-do-arquivo-sql-gerado.sql>

