# Compilador de Pseudocódigo

<p> Projeto desenvolvido durante o curso conceitual de compiladores pela <b>Faculdade Impacta</b> na graduação em Engenharia da Computação.</p>

Durante o curso foram apresentados os conceitos por trás dos compiladores, tais como:

●Níveis de linguagens de programação;
● Especificação de linguagens de programação;
● Tipos de processadores de linguagens;
● Técnicas de bootstrapping;
● Fases e passos de compilação;
● Análise léxica;
●Parsing;
● Árvores de sintaxe abstrata;
● Análise de contexto (identificação e verificação de tipos);
● Organização de tempo de execução:
● Representação de dados;
● Avaliação de expressões;
● Alocação de memória;
● Subprogramas;
● Geração de código:
● Constantes e variáveis;
● Subprogramas; 

Devido a limitação de tempo da disciplina, o projeto da mesma se limitou ao desenvolvimento do <b>analidor Léxico e sintático</b>. Futuramento posso dar continuidade ao desenvolvimento com o analisador semantico e geração de codigo assembly para um microprocessaor como o ATmega320P (Arduino).


# Documentação

# Index

 1. Analisador Léxico Definições
	 1.1 Exemplo de utilização
	 1.2 Definição dos Átomos que são Palavras Reservadas
	 1.3 Definição dos átomos sem atributos
	 1.4 Definição do átomo OP_LOGICO
	 1.5 Definição do átomo IDENTIFICADOR
	 1.6 Definição do átomo NUMERO_INTEIRO e NUMERO_REAL
	 1.7 Definição do átomo FRASE
	 1.8 Definição do átomo COMENTÁRIO
	 
 2. Funcionamento
	 2.1 Pseudocodigo de teste.
	 2.2 Retorno do Bash ao TESTE.PTL

				 


	



# 1 - Analisador Lexíco Definições


## 1.1 - Exemplo de utilização:

Exemplo: Se o programa a ser analisado possuir o nome TESTE.PTL, e o programa fonte sendo lexico.py, a execução deve ser:
```bash
$ python lexico.py TESTE.PTL
```
A rotina **proximo_atomo()** deve fazer um controle das linhas do programa fonte e também fazer a eliminação dos delimitadores (espaços em branco, tabulação, nova linha e retorno de carro). Para cada átomo reconhecido devem ser mostrados os seguintes valores:

## 1.2 Definição dos Átomos que são Palavras Reservadas

As palavras chaves da linguagem são consideradas palavras reservadas, ou seja, não podem ser utilizadas como identificadores. Para simplificar a rotina de análise léxica, o reconhecimento de palavras chaves será feito com base na definição regular de identificadores, sendo que a determinação do átomo associado à palavra chave é feita por uma busca em uma tabela de palavras reservadas. A busca na tabela de palavras reservadas deve ser implementada utilizando um dicionário para tabela de palavras reservadas.

Átomos Retornados | Descrição
-- | -------
ALGORITMO | Inicio do algoritmo
ATE | Inicializa a variável de controle do PARA
CADEIA | Tipo de dado para sequência de caracteres
CARACTER | Tipo de dado para definir um caracter
ENQUANTO | Determina um laço com condição no início
ENTAO | usado no bloco de estrutura de seleção
FACA | usado no bloco de estrutura de repetição
FIM | Fim de um bloco ou do programa
FUNCAO | Determina uma função no algoritmo
INICIO | Início do algoritmo
INTEIRO | Tipo de dado para números inteiros
PARA | Determina um laço com variável de controle
PASSO | Incremento da variável de controle na repetição
PROCEDIMENTO | Determina um procedimento no algoritmo
REAL | Tipo de Dado para números reais ( ponto flutuante )
REF | Operador para de referência para variáveis
RETORNE | Retorna de uma função
SE | Determina uma estrutura de seleção
SENAO | Caso contrário da instrução de seleção
VARIAVEIS | Início do bloco de declaração de variáveis

**Obs: As palavras Reservadas podem ser informadas com caracteres maiúsculos ou minúsculos, ou seja, aLgoriTmo o átomo retornado deve ser ALGORITMO**

## 1.3 - Definição dos átomos sem atributos

Átomo | Lexema
-----|---------
ATRIBUICAO |<-
PONTO | .
ABRE_PAR | (
FECHA_PAR | )
PONTO_VIRGULA | ;
VIRGULA | ,
SUBTRACAO | -
ADICAO | +
MULTIPLICACAO | *
DIVISAO | /
RESTO | %
## 1.4 - Definição do átomo OP_LOGICO

OP_LOGICO → & | $ | !

**Onde o atributo associado ao átomo OP_LOGICO deverá ser as constantes simbólicas:**

Átomo | Lexema
-----|-----
E | &
OU | $
NEG | !
## 1.5 - Definição do átomo IDENTIFICADOR

LETRA → [_A-Za-z]

DIGITO → [0-9]

IDENTIFICADOR → LETRA(LETRA|DIGITO)*

Quando um IDENTIFICADOR é reconhecido, deve-se fazer uma busca na tabela de palavras reservados; se for encontrado, deve-se retornar o átomo associado com a palavra chave; caso contrário, o átomo IDENTIFICADOR deve ser retornado
## 1.6 -  Definição do átomo NUMERO_INTEIRO e NUMERO_REAL

NUMERO_INTEIRO → DIGITOS+

OP_FRACAO → .DIGITOS*

OP_EXP → ( (E|e) ( +| – | λ) DIGITO+)

NUMERO_REAL → NUMERO_INTEIRO OP_FRACAO (OP_EXP | λ)

O atributo para  **NUMERO_INTEIRO**  ou  **NUMERO_REAL**  é o valor da constante numérica que gerou o átomo.
## 1.7 - Definição do átomo FRASE

CHAR1 → {qualquer caractere ASCII menos os caracteres de retorno de carro e avanço de linha }

FRASE → “ CHAR1* ”

Quando a frase tiver “ (aspas) esta deve ser precedida pelo caracter ‘\’. O atributo para  **FRASE**  é um apontador para a cadeia de caracteres.
## 1.8 - Definição do átomo COMENTÁRIO

CHAR2 → {qualquer caractere ASCII }

COMENTARIO → /* CHAR2 */

Para COMENTARIO deve ser retornado átomo correspondente, e o controle de linhas deve ser mantido dentro do comentário. COMENTARIO não possui atributo.

## 2 - Funcionamento
## 2.1 - Pseudocodigo de teste.
```bash
/*teste*/
AlGoRiTmO programa_teste
VARIAVEIS 
       INTEIRO  X 
INICIO
   IMPRIMA("TESTE\n")
   x <- 0;
   ENQUANTO (X <= 10) ENTAO
      SE (x % 2 = 0) ENTAO
          IMPRIMA(x)
      FIM
      X <- x + 1
   FIM 
FIM
```
## 2.2 - Retorno do Bash ao TESTE.PTL
```bash
┌💁  leandro @ 💻  NAVE in 📁  Compilador on 🌿  main •2 ⌀9 ✗
└❯ python lexico2.py teste.ptl 
Linha: 1 - atomo: ALGORITMO 	lexema: ALGORITMO	valor: 0	operador: --
Linha: 1 - atomo: IDENTIF 	lexema: Exemplo01	valor: 0	operador: --
Linha: 2 - atomo: VARIAVEIS 	lexema: VARIAVEIS	valor: 0	operador: --
Linha: 2 - atomo: INTEIRO 	lexema: INTEIRO	valor: 0	operador: --
Linha: 2 - atomo: IDENTIF 	lexema: x	valor: 0	operador: --
Linha: 2 - atomo: VIRGULA 	lexema: ,	valor: 0	operador: --
Linha: 2 - atomo: IDENTIF 	lexema: y	valor: 0	operador: --
Linha: 2 - atomo: VIRGULA 	lexema: ,	valor: 0	operador: --
Linha: 2 - atomo: IDENTIF 	lexema: z	valor: 0	operador: --
Linha: 3 - atomo: INICIO 	lexema: INICIO	valor: 0	operador: --
Linha: 4 - atomo: IDENTIF 	lexema: x	valor: 0	operador: --
Linha: 4 - atomo: ATRIBUIÇÃO 	lexema: <-	valor: 0	operador: --
Linha: 4 - atomo: NUM_INT 	lexema: 10	valor: 10	operador: --
Linha: 4 - atomo: PONTO_VIRGULA 	lexema: ;	valor: 0	operador: --
Linha: 5 - atomo: IDENTIF 	lexema: y	valor: 0	operador: --
Linha: 5 - atomo: ATRIBUIÇÃO 	lexema: <-	valor: 0	operador: --
Linha: 5 - atomo: IDENTIF 	lexema: x	valor: 0	operador: --
Linha: 5 - atomo: MULOP 	lexema: /	valor: 0	operador: DIVISAO
Linha: 5 - atomo: NUM_INT 	lexema: 100	valor: 100	operador: --
Linha: 5 - atomo: PONTO_VIRGULA 	lexema: ;	valor: 0	operador: --
Linha: 6 - atomo: IDENTIF 	lexema: z	valor: 0	operador: --
Linha: 6 - atomo: ATRIBUIÇÃO 	lexema: <-	valor: 0	operador: --
Linha: 6 - atomo: ABRE_PAR 	lexema: (	valor: 0	operador: --
Linha: 6 - atomo: IDENTIF 	lexema: x	valor: 0	operador: --
Linha: 6 - atomo: ADDOP 	lexema: +	valor: 0	operador: ADICAO
Linha: 6 - atomo: IDENTIF 	lexema: y	valor: 0	operador: --
Linha: 6 - atomo: FECHA_PAR 	lexema: )	valor: 0	operador: --
Linha: 6 - atomo: MULOP 	lexema: /	valor: 0	operador: DIVISAO
Linha: 6 - atomo: ABRE_PAR 	lexema: (	valor: 0	operador: --
Linha: 6 - atomo: IDENTIF 	lexema: x	valor: 0	operador: --
Linha: 6 - atomo: MULOP 	lexema: *	valor: 0	operador: MULTIPLICACAO
Linha: 6 - atomo: NUM_INT 	lexema: 2	valor: 2	operador: --
Linha: 6 - atomo: FECHA_PAR 	lexema: )	valor: 0	operador: --
Linha: 7 - atomo: FIM 	lexema: FIM	valor: 0	operador: --
Linha: 7 - atomo: PONTO 	lexema: .	valor: 0	operador: --
Linha: 7 - atomo: EOS 	lexema: 	valor: 0	operador: --
```
