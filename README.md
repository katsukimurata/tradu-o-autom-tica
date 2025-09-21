## Pergunta 1: Impacto de Diferentes Valores de num_examples no Tamanho do Vocabulário
Resultados observados:

```
num_examples | Tamanho do vocabulário (origem) | Tamanho do vocabulário (destino)
    100      |              40                 |              40
    300      |              102                |              107
    600      |              184                |              201
    1000     |              266                |              321
    2000     |              454                |              585
```
Interpretação:

1. **Aumento do vocabulário**:
À medida que o valor de num_examples aumenta, tanto o vocabulário do idioma de origem quanto o do destino crescem significativamente. Por exemplo, com 100 exemplos, o vocabulário possui aproximadamente 40 tokens; com 2000 exemplos, os vocabulários atingem 454 tokens (origem) e 585 tokens (destino).

2. **Diversidade de palavras**:
Isso ocorre porque um número maior de exemplos expõe o modelo a uma variedade maior de palavras e expressões. Palavras menos frequentes que não apareceriam em um conjunto pequeno podem passar o critério de frequência mínima (por exemplo, min_freq=2) e, assim, serem incluídas no vocabulário.

3. **Trade-off**:
Embora vocabulários maiores possam capturar mais nuances da linguagem, eles também podem aumentar a complexidade do modelo e o custo computacional. Por isso, é importante equilibrar a quantidade de dados e o tamanho do vocabulário conforme a aplicação.


## Pergunta 2: Tokenização em Idiomas sem Delimitadores Explícitos (Chinês e Japonês)

Observação Experimental (Exemplo com "teste katsuki"):

Tokenização simples:
Utilizando o método split(' '), o texto "测试胜希" é interpretado como um único token, pois não há espaços para indicar separações:

```python
tokens_simples = chinese_text.split(' ')
# Resultado: ['测试胜希']
```
Tokenização com ferramenta especializada (jieba):
Ao aplicar o jieba, o mesmo texto é segmentado em tokens mais significativos:

```python
tokens_jieba = tokenize_chinese(chinese_text)
# Resultado: ['测试', '胜希']
```
Análise:

Problema da tokenização simples:
Em idiomas como chinês e japonês, onde não há espaços explícitos entre as palavras, o método de divisão simples falha em separar os componentes linguísticos corretamente, resultando em um único token para toda a sequência.

Solução com tokenizadores especializados:
Utilizar ferramentas como o jieba (para chinês) ou Mecab (para japonês) permite identificar as fronteiras naturais das palavras ou subunidades, proporcionando uma segmentação que faz sentido para o idioma.

