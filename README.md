<h1 style="text-align:center"> MODELAGEM BÁSICA </h1>

<h2> PROCESSOS DE MODELAGEM </h2>

1. MODELAGEM CONCEITUAL - RASCUNHO - (<font color="#7c22d6"><b>DA</b></font>)
2. MODELAGEM LÓGICA - PROGRAMAS DE MODELAGEM - (<font color="#7c22d6"><b>DA</b></font>)
3. MODELAGEM FÍSICA - SCRIPTS DE BANCO - (<font color="#7c22d6"><b>DBA/DA</b></font>)

<p>
<font color="#7c22d6"><b>DA</b></font> - Administração de Dados <br>
<font color="#7c22d6"><b>BDA</b></font> - Administração de Bancos de Dados
</p>

<h3> INICIANDO A MODELAGEM CONCEITUAL </h3>

<p> 
CLIENTE<br>

NOME - CARACTER(30)<br>
CPF - NUMERICO(11)<br>
EMAIL - CARACTER(30)<br>
TELEFONE - CARACTER(30)<br>
ENDERECO - CARACTER(100)<br>
SEXO - CARACTER(1)<br>
</p>

<h3> INICIANDO A MODELAGEM LÓGICA </h3>

<a href="https://imgur.com/fJeTHUe"><img src="https://i.imgur.com/fJeTHUe.png" title="source: imgur.com" /></a>

<h3> INICIANDO A MODELAGEM FÍSICA </h3>


<h4> CRIANDO O BANCO DE DADOS </h4>

```SQL

CREATE DATABASE PROJETO;

```

<h4>  CONECTANDO-SE AO BANCO </h4>

```SQL

USE PROJETO;

```

<h4> CRIANDO A TABLA DO CLIENTES </h4>

```SQL

CREATE TABLE CLIENTE (
	NOME VARCHAR(30),
	SEXO CHAR(1),
	EMAIL VARCHAR(30),
	CPF INT(11),
	TELEFONE VARCHAR(30),
	ENDERECO VARCHAR(100)
);

```
<h4> VERIFICANDO AS TABELAS DO BANCO DE DADOS </h4>

```SQL

SHOW TABLES;

```

<h4> DESCOBRINDO COMO É A ESTRUTURA DE UMA TABELA </h4>

```SQL

DESC CLIENTE;

```

<h2>TIPOS DE DADOS</h2>
<p>
Todos os banos de dados possuem tipos que devem ser atribuidos aos dados de uma tabela.
Para caracteres literais, temos <font color="#f70000"><b>char</b></font> e <font color="#f70000"><b>varchar</b></font>, para números temos <font color="#f70000"><b>int</b></font> e <font color="#f70000"><b>float</b></font>, para
objetos como fotos e documentos, temos o <font color="#f70000"><b>blob</b></font>, para textos extensos, temos o <font color="#f70000"><b>text</b></font>. 
</p>
<p>
Cada caracter no banco de dados, vale <font color="#0bb1c4">1</font> byte. Sendo assim, se eu entro com o dado JOÃO,
estou entrando com <font color="#0bb1c4">4</font> bytes no meu banco. E o que isso tem a ver com a tipagem de tabelas?
</p>
<p>
O banco de dados funciona como um download de dados da internet. Se baixamos um arquivo de <font color="#0bb1c4">1</font> giga,
temos um temo maior que o download de <font color="#0bb1c4">50</font> megas, considerando a mesma velocidade de conexão.
</p>
<p>
Ao tiparmos uma tabela de modo errado ou displicente, vamos aumentar a quantidade de dados que 
será baixada do banco de dados, prolongando assim o tempo de resposta.
</p>

<p>
Uma comparacao bem didatica é o tipo <font color="#f70000"><b>char</b></font> e <font color="#f70000"><b>varchar</b></font>
A palavra <font color="#7c22d6"><b>var</b></font>, vem de variant, em ingles, ou seja, que é dinâmica. Logo, vimos que 1 caracter
é igual a <font color="#0bb1c4">1</font> byte. Vejamos então a tipagem
</p>


```SQL

VARCHAR(10)
CHAR(10)

```

<p>
entrando a palavra joao <br>

total de bytes <font color="#f70000"><b>varchar</b></font>(<font color="#0bb1c4">10</font>) = <font color="#0bb1c4">4</font> bytes <br>
toal de bytes <font color="#f70000"><b>char</b></font>(<font color="#0bb1c4">10</font>) = <font color="#0bb1c4">10</font> bytes
</p>

<p>
isso ocorre pois o <font color="#f70000"><b>char</b></font> não varia. Os caracteres restantes serao preenchidos com espaço. 
eles nao ficam vazios. Enquanto que no <font color="#f70000"><b>varchar</b></font>, o tipo varia conforme o dado.
Entao utilizo sempre o <font color="#f70000"><b>varchar</b></font>? Não. O charé ligeiramente mais performatico, por nao
ter que gastar tempo variando de tamanho. Entao a regra é utilizar sempre o <font color="#f70000"><b>char</b></font> quando
sabemos que o numero de caracteres naquela coluna nao vai variar nunca. Por exemplo,
unidade federativa, com dois digitos, sexo com um digito e assim por diante. Vista a diferença
que podemos fazer com uma tipagem correta de tabelas.
</p>

<h2>SINTAXE BÁSICA DE INSERÇÃO</h2>

<!-- <h4>CONECTANDO-SE AO BANCO</h4>

```SQL

USE PROJETO;

```

<h4>MOSTRANDO AS TABELAS</h4>

```SQL

SHOW TABLES;

```

<h4>EXIBINDO A ESTRUTURA DE UMA TABELA</h4>

```SQL

DESC CLIENTE;

``` -->

<h3>INSERINDO DADOS E VALORES NULOS</h3>

<h4>FORMA 01 - OMITINDO AS COLUNAS</h4>

```SQL

INSERT INTO CLIENTE VALUES('JOAO','M','JOAO@GMAIL.COM',988638273,'22923110','MAIA LACERDA - ESTACIO - RIO DE JANEIRO - RJ');

INSERT INTO CLIENTE VALUES('CELIA','F','CELIA@GMAIL.COM',541521456,'25078869','RIACHUELO - CENTRO - RIO DE JANEIRO - RJ');

INSERT INTO CLIENTE VALUES('JORGE','M',NULL,885755896,'58748895','OSCAR CURY - BOM RETIRO - PATOS DE MINAS - MG');

INSERT INTO CLIENTE VALUES('JHONATAN', 'M', 'JHONY@GMAIL.COM', 988633441, '16999333990', 'RUA MAIA - RIBEIRAO PRETO - SP');


```

<h4>FORMA 02 - DESCREVENDO AS COLUNAS</h4>

```SQL

INSERT INTO CLIENTE(NOME,SEXO,ENDERECO,TELEFONE,CPF) VALUES('LILIAN','F','SENADOR SOARES - TIJUCA - RIO DE JANEIRO - RJ','947785696',887774856);

INSERT INTO CLIENTE(NOME,SEXO,ENDERECO,TELEFONE,CPF) VALUES('THIAGO', 'M', 'RUA TACO - RIBEIRAO PRETO - SP', '16999333944', 988633455);

```

<h4>FORMA 03 - INSERT COMPACTO - SOMENTE MYSQL</h4>

```SQL

INSERT INTO CLIENTE VALUES('ANA','F','ANA@GLOBO.COM',85548962,'548556985','PRES ANTONIO CARLOS - CENTRO - SAO PAULO - SP'),
                          ('CARLA','F','CARLA@TERATI.COM.BR',7745828,'66587458','SAMUEL SILVA - CENTRO - BELO HORIZONTE - MG'),
			  ('DANIEL','M','DANI@GMAIL.COM',988563441,'16999833990','RUA EUCLIDES - RIBEIRAO PRETO - SP'),
			  ('MANUELA','F','MANU@GMAIL.COM',863344112,'16999339493','RUA JOÃO - RIBEIRAO PRETO - SP'),
			  ('MATHEUS','M','MATHEUS@GMAIL.COM',812344112,'16900339493','RUA ORION - SERTÃOZINHO - SP'),
			  ('LETICIA','F','LETICIA@GMAIL.COM',835344112,'16919330493','RUA JOÃO - RIBEIRAO PRETO - SP'),
		          ('JOSY','F','JOSY@GMAIL.COM',863347212,'16592332493','RUA ITAPIRU - SERTÃOZINHO - SP'),
			  ('EDUARDO','M','MANU@GMAIL.COM',869244112,'11789329493','RUA ITAPIRU - RIO DE JANEIRO - RJ'),
			  ('DANIELA','F','DANIELA@GMAIL.COM',863294112,'11789329493','RUA ITAPIRU - RIO DE JANEIRO - RJ');
						  
INSERT INTO CLIENTE(NOME,SEXO,ENDERECO,TELEFONE,CPF) VALUES('CLARA','F','SENADOR SOARES - TIJUCA - RIO DE JANEIRO - RJ','883665843',99999999999);

INSERT INTO CLIENTE(NOME,SEXO,ENDERECO,TELEFONE,CPF) VALUES('CLARA','F','SENADOR SOARES - TIJUCA - RIO DE JANEIRO - RJ','883665843',22222222222);
			
```

<h4><font color="#f70000"><b>ERROR</b></font> - Out of range value for column 'CPF' at row 1</h4>

```SQL

INSERT INTO CLIENTE VALUES('LARISSA', 'F', 'LARI@GMAIL.COM', 98863344112, '16999339490', 'RUA MAIA - RIBEIRAO PRETO - SP');

```

<h2>O COMANDO SELECT - SELEÇÃO, PROJEÇÃO E JUNÇÃO</h2>

<p>
<font color="#7c22d6"><b>SELEÇÃO</b></font>
- A seleção, como o próprio nome já diz, seleciona linhas, tuplas por meio de uma determinada condição.

Ex: nome=“Daniel”(cliente)

A seleção pode ser entendida como uma operação que filtra as linhas de uma relação(tabela), e é uma operação unária, pois opera sobre um único conjunto de dados.
</p>

<p>
<font color="#7c22d6"><b>PROJEÇÃO</b></font>
- A projeção é utilizada quando existe a necessidade de pegar somente colunas de interesse em uma relação, e não trabalhar com todas as colunas dessa relação.

Ex: nome(cliente)

Pode ser entendida como uma operação que filtra as colunas de uma tabela. Por operar sobre apenas um conjunto de entrada é classificada como uma operação unária.
</p>

<p>
<font color="#7c22d6"><b>JUNÇÃO</b></font>
- Logo após a realização de um produto cartesiano em uma relação, geralmente existe a necessidade de se fazer uma seleção na qual os campos que estão em A e também estão em B sejam iguais, porque o produto cartesiano traz tuplas que não são de interesse. A junção é a operação que simplifica tudo isso. Ela realiza um produto cartesiano, depois uma seleção das tuplas de interesse e por fim uma projeção, para remoção de colunas duplicadas.

Ex: (cliente) ⋈ (veiculo)

A tabela resultante de uma junção tem todas as colunas da primeira tabela e todas da segunda tabela.

</p>

<h3>SELECT</h3>

```SQL

SELECT NOW();

SELECT NOW() AS DATA_HORA;

SELECT NOW() AS DATA_HORA, 'JHONATAN' AS ALUNO;

SELECT 'JHONATAN';

SELECT 'BANCO DE DADOS';

```

<h3>ALIAS DE COLUNAS</h3>

```SQL

SELECT NOME AS CLIENTE, SEXO, EMAIL FROM CLIENTE;

SELECT NOME, SEXO, EMAIL FROM CLIENTE;

SELECT NOME, SEXO, EMAIL, ENDERECO FROM CLIENTE;

SELECT EMAIL, SEXO, ENDERECO, NOME FROM CLIENTE;

SELECT EMAIL, SEXO, ENDERECO, NOME, NOW() AS DATA_HORA FROM CLIENTE;

```

<h3>APENAS PARA FINS ACADEMICOS</h3>

```SQL

SELECT * FROM CLIENTE;

```

<h3>FILTRANDO DADOS COM WHERE E LIKE</h3>

```SQL

SELECT NOME, TELEFONE FROM CLIENTE;

```

<h3>FILTRANDO</h3>

```SQL

SELECT NOME, SEXO
FROM CLIENTE
WHERE SEXO = 'M';

SELECT NOME, ENDERECO
FROM CLIENTE
WHERE SEXO = 'F';

SELECT NOME, SEXO
FROM CLIENTE
WHERE ENDERECO = 'SP';

```

<p>
<font color="#7c22d6"><b>EMPTY SET</b></font> - CONJUNTO VAZIO
<br>
<font color="#0bb1c4"><b>ENDERECO</b></font>  não é igual a <font color="#0bb1c4"><b>SP</b></font> , para dados de aproximação utilizar o <font color="#f70000"><b>LIKE</b></font> 
</p>

<h3>UTILIZANDO O LIKE</h3>

```SQL

SELECT NOME, SEXO 
FROM CLIENTE
WHERE ENDERECO LIKE 'SP';

SELECT NOME, SEXO 
FROM CLIENTE
WHERE ENDERECO LIKE 'RJ';

```

<h3>CARACTER CORINGA % -> QUALQUER COISA</h3>

```SQL

SELECT NOME, SEXO
FROM CLIENTE
WHERE ENDERECO LIKE '%SP';

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE ENDERECO LIKE '%SP';

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE ENDERECO LIKE 'RUA MAIA%';

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE ENDERECO LIKE '%RIBEIRAO PRETO%';

```
<h3>EXERCICICO</h3>

[Resolvendo o exercício](./exerciocios/exercicio-01.sql)

<h2>OPERADORES LÓGICOS</h2>

<p>
<font color="#7c22d6"><b>OR</b></font> -> PARA QUE A SAIDA DA QUERY SEJA VERDADEIRA, BASTA QUE APENAS UMA CONDICAO SEJA VERDADEIRA.
<br>
<font color="#7c22d6"><b>AND</b></font> -> PARA QUE A SAIDA SEJA VERDADEIRA TODAS AS CONDICOES PRECISAM SER VERDADEIRAS.
</p>

<h3>OR - OU</h3>

<!-- ```SQL

SHOW DATABASES;

USE PROJETO;

SELECT * FROM CLIENTE;

``` -->

```SQL

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE SEXO = 'M' OR ENDERECO LIKE '%RJ';

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE SEXO = 'F' OR ENDERECO LIKE '%MG';

```

<h3>AND - E</h3>

```SQL

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE SEXO = 'M' AND ENDERECO LIKE '%RJ';

SELECT NOME, SEXO, ENDERECO
FROM CLIENTE
WHERE SEXO = 'F' AND ENDERECO LIKE '%MG';

```