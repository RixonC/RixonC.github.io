---
title: "NewtonCG"
excerpt: "
<img src='https://img.shields.io/static/v1?label=PyTorch&message=v1.5&color=yellow&style=flat&logo=pytorch&logoColor=white' href='/'>
<img src='https://img.shields.io/static/v1?label=Jupyter&message=v6&color=yellow&style=flat&logo=jupyter&logoColor=white' href='/'>
<img src='https://img.shields.io/static/v1?label=Python&message=v3.7&color=blueviolet&style=flat&logo=python&logoColor=white' href='/'>
<img src='https://img.shields.io/github/license/RixonC/NewtonCG' href='/'>
<img src='https://img.shields.io/github/stars/RixonC/NewtonCG' href='/'>
<img src='https://img.shields.io/github/forks/RixonC/NewtonCG' href='/'>
<br>Implementation of Newton-CG algorithm with backtracking line-search"
collection: code
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.2'
      jupytext_version: 1.6.0
  kernelspec:
    display_name: 'Python 3.8.3 64-bit (''torch'': virtualenv)'
    name: python_defaultSpec_1599019555120
---

<img src='https://img.shields.io/static/v1?label=PyTorch&message=v1.5&color=yellow&style=flat&logo=pytorch&logoColor=white' href='/'>
<img src='https://img.shields.io/static/v1?label=Jupyter&message=v6&color=yellow&style=flat&logo=jupyter&logoColor=white' href='/'>
<img src='https://img.shields.io/static/v1?label=Python&message=v3.7&color=blueviolet&style=flat&logo=python&logoColor=white' href='/'>
<img src='https://img.shields.io/github/license/RixonC/NewtonCG' href='/'>
<img src='https://img.shields.io/github/stars/RixonC/NewtonCG' href='/'>
<img src='https://img.shields.io/github/forks/RixonC/NewtonCG' href='/'>

<a href="https://github.com/RixonC/NewtonCG" class="btn">Repository</a>

Implementation of
[Newton-CG](https://en.wikipedia.org/wiki/Newton%27s_method_in_optimization)
algorithm with
[backtracking line-search](https://en.wikipedia.org/wiki/Backtracking_line_search),
for [PyTorch](https://pytorch.org/) as a 
[`torch.optim.Optimizer`](https://pytorch.org/docs/stable/optim.html). 
CG refers to the 
[conjugate gradient method](https://en.wikipedia.org/wiki/Conjugate_gradient_method), 
which is the optimizer's sub-problem solver.

# An example use case of NewtonCG optimizer

```python
import torch
import torch.nn as nn
import torchvision
from newton_cg import NewtonCG
from torch.utils.data import DataLoader
from torchvision import datasets, transforms
```

## Load data
### We use MNIST

```python
transform = transforms.ToTensor()
train_set = datasets.MNIST("~/Downloads/", transform=transform)
test_set = datasets.MNIST("~/Downloads/", transform=transform, train=False)
train_loader = DataLoader(train_set, batch_size=len(train_set))
test_loader = DataLoader(test_set, batch_size=len(test_set))
```

### NewtonCG assumes optimization steps are performed over the full dataset

```python
device = torch.device('cuda' if torch.cuda.is_available() else 'cpu')
train_inputs, train_targets = iter(train_loader).next()
train_inputs = train_inputs.reshape(-1, 784).to(device)
train_targets = train_targets.to(device)
test_inputs, test_targets = iter(test_loader).next()
test_inputs = test_inputs.reshape(-1, 784).to(device)
test_targets = test_targets.to(device)
```

## Define model, loss function and optimizer
### We use softmax regression with cross entropy loss, as it's convex

```python
weights = torch.zeros(784, 10, requires_grad=True, device=device)
criterion = nn.CrossEntropyLoss()
optimizer = NewtonCG([weights])
```

## Train the model

```python
num_epochs = 10
for epoch in range(num_epochs):
    # compute test accuracy
    correct = 0
    total = 0
    outputs = torch.mm(test_inputs, weights)
    _, predicted = torch.max(outputs.data, 1)
    total += test_targets.size(0)
    correct += (predicted == test_targets).sum().item()
    accuracy = 100 * correct / total

    # optimizer step
    optimizer.zero_grad()
    outputs = torch.mm(train_inputs, weights)
    loss = criterion(outputs, train_targets)
    loss.backward()
    closure = lambda : criterion(torch.mm(train_inputs, weights), train_targets)
    loss = optimizer.step(closure)

    print("epoch: {},  loss: {:.2e},  "
          "test accuracy: {:.2f}".format(epoch, loss, accuracy))
```

```python
epoch: 0,  loss: 2.30e+00,  test accuracy: 9.80
epoch: 1,  loss: 5.14e-01,  test accuracy: 85.49
epoch: 2,  loss: 3.65e-01,  test accuracy: 90.25
epoch: 3,  loss: 3.15e-01,  test accuracy: 91.45
epoch: 4,  loss: 2.88e-01,  test accuracy: 92.03
epoch: 5,  loss: 2.78e-01,  test accuracy: 92.18
epoch: 6,  loss: 2.73e-01,  test accuracy: 92.31
epoch: 7,  loss: 2.68e-01,  test accuracy: 92.31
epoch: 8,  loss: 2.65e-01,  test accuracy: 92.37
epoch: 9,  loss: 2.62e-01,  test accuracy: 92.38
```
