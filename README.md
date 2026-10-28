# microgpt com Nomes Brasileiros

Projeto simples feito como aluno, inspirado no **microgpt** do Andrej Karpathy.

O objetivo é entender, da forma mais mínima possível, como funciona um GPT:
- dataset de texto
- tokenizer
- rede neural (transformer bem pequeno)
- cálculo de gradientes (autograd)
- otimizador
- treinamento
- geração de texto novo

Tudo em **um único arquivo Python**, sem nenhuma biblioteca externa (só a biblioteca padrão).

## O que o programa faz?

1. Carrega uma lista de nomes brasileiros (arquivo `nomes_br.txt`).
2. Treina um modelo minúsculo de linguagem para aprender a "escrever" nomes parecidos.
3. No final, gera nomes novos (alguns reais, alguns inventados, mas com cara de nome brasileiro).

## Como rodar

```bash
python microgpt.py
```

O script vai:
- Baixar a lista de nomes (se ainda não existir)
- Treinar por cerca de 800 passos (leva alguns minutos)
- Mostrar a loss diminuindo
- Gerar 20 nomes no final

## Estrutura do código (bem resumida)

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

## Por que é interessante?

Você vê **todo o algoritmo** de um GPT em ~250 linhas:
- Sem PyTorch
- Sem CUDA
- Sem truques

É a versão "essência" do que modelos grandes fazem, só que minúscula e legível.

## Observações

- O modelo é propositalmente pequeno (`n_embd=16`, 1 camada) para treinar rápido no CPU.
- Nomes com acento foram filtrados para manter o vocabulário simples (só a-z).
- A qualidade dos nomes gerados não é perfeita (é um modelo bem pequeno), mas já dá para ver o padrão sendo aprendido.

## Créditos

- Ideia e arquitetura original: [Andrej Karpathy - microgpt](https://karpathy.github.io/2026/02/12/microgpt/)
- Lista de nomes: baseada em dados públicos brasileiros

Feito de forma simples, só para estudar e brincar. 🇧🇷
