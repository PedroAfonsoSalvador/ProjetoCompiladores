# Compilador de Linguagem de Consultas de Biblioteca

Equipe: Pedro Afonso Cavalcanti Salvador

## Descrição

Este projeto implementa um compilador simples para uma linguagem de consultas de biblioteca. Ele suporta três operações principais: 
- `ADICIONAR_LIVRO`: Adiciona um livro à biblioteca.
- `REMOVER_LIVRO`: Remove um livro da biblioteca.
- `BUSCAR_LIVRO`: Busca um livro na biblioteca.

O compilador realiza as etapas de análise léxica, sintática e semântica, e gera o código correspondente para manipular a biblioteca.

## Estrutura do Código

### Análise Léxica

A classe `AnalisadorLexico` é responsável por converter o texto de entrada em tokens. Ela ignora espaços em branco e identifica os seguintes tokens:
- `ADICIONAR_LIVRO`
- `REMOVER_LIVRO`
- `BUSCAR_LIVRO`
- `STRING`
- `VIRGULA`

### Análise Sintática

A classe `AnalisadorSintatico` recebe os tokens do analisador léxico e constrói a árvore de sintaxe abstrata (AST). Ela verifica a estrutura dos comandos e levanta erros de sintaxe quando encontra problemas.

### Análise Semântica

A classe `AnalisadorSemantico` verifica a validade dos comandos em relação ao estado atual da biblioteca. Ela garante que, por exemplo, não se pode adicionar um livro que já existe ou remover/buscar um livro que não existe.

### Geração de Código

A classe `GeradorCodigo` executa os comandos na biblioteca. Ela manipula o dicionário da biblioteca de acordo com a AST gerada pela análise sintática.

## Como Utilizar

1. **Importe as classes necessárias:**

    ```python
    from compilador import AnalisadorLexico, AnalisadorSintatico, AnalisadorSemantico, GeradorCodigo, ErroSemantico
    ```

2. **Crie uma instância do analisador léxico com o texto de entrada:**

    ```python
    texto_entrada = 'ADICIONAR_LIVRO "O Senhor dos Anéis", "J.R.R. Tolkien"'
    analisador_lexico = AnalisadorLexico(texto_entrada)
    ```

3. **Crie uma instância do analisador sintático e analise o texto:**

    ```python
    analisador_sintatico = AnalisadorSintatico(analisador_lexico)
    ast = analisador_sintatico.analisar()
    ```

4. **Crie uma instância do analisador semântico e valide a AST:**

    ```python
    biblioteca = {}
    analisador_semantico = AnalisadorSemantico(biblioteca)
    try:
        analisador_semantico.analisar(ast)
    except ErroSemantico as e:
        print(f"Erro semântico: {e}")
    ```

5. **Gere e execute o código:**

    ```python
    gerador_codigo = GeradorCodigo(biblioteca)
    resultado = gerador_codigo.gerar(ast)
    if resultado:
        print(resultado)
    ```

6. **Execute outro comando:**

    ```python
    texto_entrada = 'BUSCAR_LIVRO "O Senhor dos Anéis"'
    analisador_lexico = AnalisadorLexico(texto_entrada)
    analisador_sintatico = AnalisadorSintatico(analisador_lexico)
    ast = analisador_sintatico.analisar()
    analisador_semantico.analisar(ast)
    resultado = gerador_codigo.gerar(ast)
    if resultado:
        print(resultado)
    ```

Com esses passos, você pode adicionar, remover e buscar livros em sua biblioteca utilizando a linguagem de consultas desenvolvida. A biblioteca é armazenada como um dicionário Python e os comandos são processados sequencialmente. 
