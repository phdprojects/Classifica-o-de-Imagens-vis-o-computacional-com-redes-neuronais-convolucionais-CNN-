# Dataset — CIFAR-10 (60.000 imagens 32x32x3, uint8)

Origem: CIFAR-10 (Alex Krizhevsky, 2009; via `keras.datasets.cifar10`),
divisão oficial 50.000 treino / 10.000 teste, 10 categorias equilibradas
(5.000 treino / 1.000 teste por categoria).

## Ficheiros (limite de 100 MB/ficheiro do GitHub: treino dividido em 2 partes)

| Ficheiro | Forma | Conteúdo |
| --- | --- | --- |
| `x_train_parte1.npy` | (25000, 32, 32, 3) | imagens de treino, primeira metade |
| `x_train_parte2.npy` | (25000, 32, 32, 3) | imagens de treino, segunda metade |
| `x_test.npy` | (10000, 32, 32, 3) | imagens de teste |
| `y_train.npy` | (50000,) | etiquetas de treino (0-9) |
| `y_test.npy` | (10000,) | etiquetas de teste (0-9) |

Etiquetas (ordem oficial): 0 avião, 1 automóvel, 2 pássaro, 3 gato, 4 veado,
5 cão, 6 rã, 7 cavalo, 8 navio, 9 camião.

## Como carregar (fora do Keras)

```python
import numpy as np
x_train = np.concatenate([np.load('dataset/x_train_parte1.npy'),
                          np.load('dataset/x_train_parte2.npy')])
y_train = np.load('dataset/y_train.npy')
x_test = np.load('dataset/x_test.npy'); y_test = np.load('dataset/y_test.npy')
```

O notebook do projeto carrega o dataset do Keras automaticamente; esta pasta
existe para replicação offline, Jupyter local e anexar como Dataset no Kaggle.
