<h1> MODELAGEM BÁSICA  </h1>

<p> 
CLIENTE<br>

NOME - CARACTER(30)<br>
CPF - NUMERICO(11)<br>
EMAIL - CARACTER(30)<br>
TELEFONE - CARACTER(30)<br>
ENDERECO - CARACTER(100)<br>
SEXO - CARACTER(1)<br>
</p>

<h2> PROCESSOS DE MODELAGEM </h2>

1. MODELAGEM CONCEITUAL - RASCUNHO - (DA)
2. MODELAGEM LÓGICA - PROGRAMAS DE MODELAGEM - (DA)
3. MODELAGEM FÍSICA - SCRIPTS DE BANCO - (BDA/DA)

<p>
DA - Administração de Dados <br>
DBA - Administração de Bancos de Dados
</p>

<h3> INICIANDO A MODELAGEM CONCEITUAL </h3>

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

<h4>CONECTANDO-SE AO BANCO</h4>

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

```
<!-- <h3>INSERINDO DADOS E VALORES NULOS</h3> -->

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

<h4>FORMA 03 - INSERT COMPACTO - SOMENTE MYSQL </h4>

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

