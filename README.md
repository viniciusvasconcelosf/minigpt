# minigpt gerador de nomes brasileiros por inferencia

O objetivo é entender, da forma mais mínima possível, como funciona o treinamento de um LLM:
- dataset de texto
- tokenizer
- rede neural (transformer bem pequeno)
- cálculo de gradientes (autograd)
- otimizador
- treinamento
- geração de texto novo

Tudo em **um único arquivo Python**, sem nenhuma biblioteca externa.

## O que o programa faz?

1. carrega uma lista de nomes brasileiros (arquivo `nomes_br.txt`).
2. treina um modelo minúsculo de linguagem para aprender a "escrever" nomes parecidos.
3. no final, gera nomes novos (alguns reais, alguns inventados, seguindo o padrão de nomes brasileiros).

## como rodar

```bash
python minigpt.py
```

O script vai:
- baixar a lista de nomes (se ainda não existir)
- treinar em alguns passos (configuravel no arquivo)
- calcular o loss durante o loop de treinamento
- gerar 20 nomes de exemplo

## Estrutura do código resumida

| Parte              | O que faz                                      |
|--------------------|------------------------------------------------|
| Dataset            | Lista de nomes brasileiros                     |
| Tokenizer          | Cada letra vira um número                      |
| Classe `Value`     | Autograd (calcula os gradientes sozinho)       |
| Parâmetros         | Os "números" que a rede aprende                |
| Função `gpt`       | A arquitetura (attention + MLP)                |
| Adam               | Otimizador que atualiza os parâmetros          |
| Loop de treino     | Passa nomes, calcula loss, atualiza pesos      |
| Inferência         | Gera nomes novos letra por letra               |


você vê **todo o algoritmo** de uma LLM em ~220 linhas:
- sem PyTorch
- sem CUDA
- sem truques

versão "essência" do que modelos grandes fazem, só que minúscula e legível.

## Observações

- o modelo é propositalmente pequeno para treinar rápido no CPU.
- a qualidade dos nomes gerados não é perfeita (é um modelo bem pequeno), mas já dá para ver o padrão sendo aprendido.
- lista de nomes: baseada em dados públicos brasileiros
