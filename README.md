# SQL-para-Banco-de-Dados-Postgres
# Esta tabela serve de base de estudos basicos e exemplos de Querys que podem ser utilizadas para filtrar dados nas tabelas#
# Nessa tabela é possivel executar filtros como: AVG, ROUND, valor total de todas a notas, extrair somente um valor etc...#
# primeiro, precisamos instalar o Docker.com, que servirá, Em termos simples: ele permite rodar programas isolados dentro de "caixinhas" chamadas containers, sem precisar instalar tudo diretamente no   #   seu   sistema.
# para se criar um Conteiner, usarei um exemplo que eu mesmo criei, a escolha dos nomes e portas são pessoais.
# no Prompt de comando após instalar o Docker e com ele aberto ( para o Docker rodar as vezes, é necessário desabilitar alguns Firewalls do Windows) 
##   digite: docker run --name dbdan -p 5436:5432 -e POSTGRES_USER=dan -e POSTGRES_PASSWORD=dan1010 -e POSTGRES_DB=dandb -d postgres:17.5.  Lembrando que a porta da direita é onde o  utilizador pode     escolher, a da esquerda é interna do Docker.
# Após, é necessário a intalação do SGBD POstgres/PG admin, para que possamos rodar o banco de dados criado no Docker.
# Após, crie um servidor, inserindo os dados pedidos e a senha criada no Prompt( para essas configurações recomendo buscar no youtube, caso não tenha familiaridade com a ferramenta).
# Após servidor criado, é hora de criar um novo 'SCHEMA', conforme segue abaixo os codigos de inserção de tabela e dados FICTICIOS DA TABELA. 


############################                                                                      OS DADOS SÃO FICTICIOS                                                       #######################




-- Cria o schema no banco de dados
CREATE SCHEMA tab01 AUTHORIZATION dan;


-- Criando a tabela 'estudantes_dan'
CREATE TABLE tab01.estudantes_dan (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(50),
    sobrenome VARCHAR(50),
    nota_exame1 DECIMAL(5, 2),
    nota_exame2 DECIMAL(5, 2),
    tipo_sistema_operacional VARCHAR(20)
);


-- Inserindo 32 registros fictícios na tabela 'estudantes_dan'
INSERT INTO tab01.estudantes_dan (nome, sobrenome, nota_exame1, nota_exame2, tipo_sistema_operacional) VALUES
('Xavier', 'Murphy', 86.0, 89.0, 'Linux'),
('Yara', 'Bailey', 80.5, 81.0, 'Windows'),
('Alice', 'Smith', 80.5, 85.0, 'Windows'),
('Quincy', 'Roberts', 86.5, 90.0, 'Mac'),
('Bob', 'Johnson', 75.0, 88.0, 'Linux'),
('Carol', 'Williams', 90.0, 90.5, 'Mac'),
('Grace', 'Miller', 95.5, 93.0, 'Windows'),
('Nina', 'Carter', 80.5, 81.0, 'Windows'),
('Ursula', 'Kim', 80.0, 82.5, 'Linux'),
('Eve', 'Jones', 90.0, 88.0, 'Mac'),
('Frank', 'Garcia', 79.0, 82.0, 'Linux'),
('Helen', 'Davis', 90.0, 89.5, 'Mac'),
('Grace', 'Rodriguez', 89.0, 88.0, 'Windows'),
('Jack', 'Martinez', 90.0, 80.0, 'Linux'),
('Karen', 'Hernandez', 93.5, 91.0, 'Windows'),
('Leo', 'Lewis', 82.0, 85.5, 'Mac'),
('Mallory', 'Nelson', 91.0, 89.0, 'Linux'),
('Oscar', 'Mitchell', 88.0, 87.5, 'Linux'),
('Paul', 'Perez', 94.0, 92.0, 'Windows'),
('Rita', 'Gomez', 77.0, 80.0, 'Linux'),
('Steve', 'Freeman', 89.5, 88.5, 'Windows'),
('Troy', 'Reed', 90.0, 92.0, 'Mac'),
('Victor', 'Morgan', 90.0, 85.0, 'Windows'),
('Oscar', 'Bell', 85.5, 87.0, 'Mac'),
('Zane', 'Rivera', 89.0, 90.5, 'Mac'),
('Aria', 'Wright', 75.0, 76.5, 'Linux'),
('Bruce', 'Cooper', 90.0, 84.0, 'Windows'),
('Karen', 'Peterson', 90.0, 92.5, 'Mac'),
('Dave', 'Brown', 88.5, 89.0, 'Windows'),
('Carlos', 'Cunha', 87.5, 90.0, 'Linux'),
('Margot', 'Suares', 80.5, 95.0, 'Windows'),
('Derek', 'Wood', 86.0, 87.5, 'Linux');


#################################                                      DAREI ALGUNS EXEMPLOS DE QUERYS DE FILTRAGEM DE TABELA                                       #######################################



===========================================================================PARA CONSULTAR A TABELA E VER TODAS  AS COLUNAS==================================================================================

SELECT *
FROM tab01.estudantes_dan

========================================================================PARA CONSULTAR TABELA E ORDENANDO POR NOME E SOBRE NOME=============================================================================

SELECT  nome, sobrenome, nota_exame1, nota_exame2, tipo_sistema_operacional
FROM tab01.estudantes_dan
ORDER BY nome, sobrenome;

===============================================================================SELECIONANDO O TIPO DE SISTEMA OPERACIONAL===================================================================================

SELECT  nome, sobrenome,  tipo_sistema_operacional
FROM tab01.estudantes_dan
ORDER BY tipo_sistema_operacional;

============================================================================================CLAUSULA WHERE=================================================================================================

# A Clausula WHERE é uma das mais importantes em SQL, ela serve principalmente para filtar linhas e quando queremos expecificar um valor em especifico!!

SELECT  nome,  tipo_sistema_operacional
FROM tab01.estudantes_dan
WHERE tipo_sistema_operacional = 'Linux'
ORDER BY nome;

#nesse caso ela retornará todos os valor que contem 'tipo_sistema_operacional = Linux', ordenando por nome e sobre nome!!!

=====================================================================SOMANDO TODAS AS NOTAS E FAZENDO A MEDIA E ARREDONDANDO PARA 2 CASAS DEPOIS DA VIRGULA==============================================

SELECT  nome, sobrenome, round(avg(nota_exame1 + nota_exame2), 2) as Media_total
FROM tab01.estudantes_dan
group by nome, sobrenome
ORDER BY nome;

# Esses são alguns comandos em SQL para banco de dados, existem muitos outros, inclusive com mais tabelas, onde através dos comandos UNION, LEFT JOIN, RIGHT JOIN, INNER JOIN podemos cruzar informações...
