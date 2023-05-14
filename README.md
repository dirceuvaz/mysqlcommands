Como fazer backup de uma base de dados mysql via linha de comando
Acessar servidor via SSH
No Windows eu recomendo o uso de algum bash ao invés do CMD, qualquer um que "emule um linux" vai ter o comando SSH, por exemplo o Git Bash que vem junto com o Git.

Caso ainda prefira o Putty, sem problemas.

Você pode baixar o Putty aqui: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html

Para usar siga este passo a passo: https://www.secnet.com.br/blog/como-acessar-um-servidor-via-ssh-com-o-putty

Acessando o Mysql
No terminal do servidor você ai rodar o comando mysql -u [usuario] -p e vai teclar enter, a senha será solicitada, a partir deste momento você pode usar qualquer comando MySql para navegar pelos bancos.

SHOW DATABASES; - Mostra todos os bancos
USE alunos_do_erik - Acessa o banco de dados
SHOW TABLES; - Mostra as tabelas no banco atual
DESCRIBE TABLE [NOME DA TABELA]; - Descreve uma tabela
Você também pode usar os famos SELECT, INSERT, UPDATE e DELETE, assim como qualquer outro comando SQL.

Fazendo o backup
No terminal do servidor você vai rodar um comando parecido com o mysql, ele se chama mysqldump, para fazer o backup de um banco de dados listando a saída na tela, mas tome isso apenas como referência por enquanto, não rode o comando ainda.

mysqldump -u [usuario] -p [nome do banco]
Isso ai vai imprimir no terminal o SQL todo, pode demorar e se for muito grande o banco, até travar, a melhor saída é armazenar tudo em um arquivo, para isso usamos um recurso no próprio linux:

mysqldump -u [usuario] -p [nome do banco] > [nome do arquivo]
O backup é até mais rápido assim.

Um exemplo com o banco alunos_do_erik, o usuário é alunos e a senha 123:

mysqldump -u alunos -p alunos_do_erik > alunos_do_erik.sql
A senha será solicitada e o arquivo alunos_do_erik.sql será criado no diretório que você estiver atualmente, eu recomando que você faça isso em um local que o ftp possa acessar, por exemplo a raiz do ftp do spp, para acessar este diretório rode o seguinte comando:

cd /home/super
Espero que isso ajude.
