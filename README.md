# Classificação de Imagens com CNN — CIFAR-10

Projeto end-to-end de visão computacional no Databricks: CNN (2 blocos
conv+pooling+dropout) treinada no CIFAR-10 (60.000 imagens 32x32, 10 categorias),
carregado diretamente de `keras.datasets.cifar10` — o notebook é auto-contido e
replicável (o dataset descarrega-se automaticamente com as divisões oficiais).

## Resultados

- **Acurácia no teste: 77.75%** (métrica de sucesso: >= 70% — CUMPRIDA)
- Modelo: 2 blocos convolucionais (32 e 64 filtros), dropout 0.25/0.5, Dense 256,
  Adam, categorical crossentropy — 1.116.970 parâmetros
- Treino base: 20 épocas | P7 (efeito de 40 épocas): GANHO MARGINAL — o custo de treinar mais não compensa e o overfitting instala-se
- Melhor classe: automóvel
  | Pior: gato
- Confusão dominante: gato -> cão (301 confusões nos dois sentidos, P2)
- Veículos 85,9% vs animais 72,3% (P3); a categoria com mais falsos positivos:
  cão (389 FP; P6)

## Ficheiros

- `historico_treino_40_epocas.csv` — curva de aprendizagem completa (treino e
  validação, época a época)
- `acuracia_por_classe.csv` — acurácia por categoria no teste
- `matriz_confusao.csv` — matriz de confusão 10x10
- `previsoes_teste.csv` — as 10.000 previsões, auditáveis imagem a imagem
- `distribuicao_classes.csv` — equilíbrio das classes (5.000/1.000 por categoria)

## Metodologia (resumo)

Divisão treino/teste oficial desde o início (sem leakage), normalização [0,1],
one-hot encoding, validação de 10% do treino, 7 perguntas de negócio respondidas
com dados (P1-P7). Métrica de sucesso definida antes do treino. Seeds fixas.

## Estrutura do repositório

- `CNN-CIFAR-10` — o notebook completo (formato fonte Databricks: Introdução, STEPs 0-9, perguntas de negócio P1-P7 e Conclusão)
- `dataset/` — o dataset CIFAR-10 completo em 5 ficheiros `.npy` (ver `dataset/README.md`)
- `resultados/` — tabelas de resultados em CSV (histórico de treino, acurácia por classe, matriz de confusão, previsões auditáveis, distribuição)
- `images/` — grelha visual 10x10 e curvas de aprendizagem (PNG)
- `requirements.txt` — dependências para execução fora do Databricks

## Dataset

O CIFAR-10 está **incluído** na pasta `dataset/` (60.000 imagens 32x32x3, uint8, em `.npy`).
O notebook carrega-o automaticamente do Keras (`keras.datasets.cifar10`) — a pasta
`também` permite: (a) uso offline, (b) replicar em Jupyter local sem download,
e (c) anexar como Dataset no Kaggle. Origem: CIFAR-10 (Krizhevsky, 2009),
divisão oficial 50.000/10.000.

## Como replicar

1. Databricks: importar o notebook e Run All (o STEP 0 instala o TensorFlow; ~2 min/época em CPU serverless; ~45 min no total, incluindo a P7 de 40 épocas).
2. Jupyter local: `pip install -r requirements.txt`, correr as células (trocar `%pip`/`%md` pelos equivalentes), com o dataset ao lado em `dataset/` (instruções no `dataset/README.md`).
