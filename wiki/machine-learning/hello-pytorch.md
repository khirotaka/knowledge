---
description: PyTorch入門
---

# Hello, PyTorch

## PyTorchによる機械学習 & 自動微分 with GPU

![](https://dev.infohub.cc/wp-content/uploads/2019/04/PyTorch.jpg)

[`PyTorch`](https://pytorch.org) はGPUアクセラレーションをサポートした **自動微分** ・ **最適化** ライブラリです。

### 自動微分

ニューラルネット は偏微分を多用するので `PyTorch` にも自動微分機能がついています

例えば、

$$
y = x^2
$$

を微分してみましょう。

`class torch.Tenosr` が持つ `.backward()` メソッドを使う事で微分を行なってくれます。

```python
import torch

x = torch.tensor(5.0, requires_grad=True)
y = x ** 2    # <- y = x^2
y.backward()   # 微分

print("dy/dx = ", x.grad.numpy())
```

二階微分だって出来ます。

```python
x = torch.tensor(5.0, requires_grad=True)
y = x ** 2    # <- y = x^2
z = torch.autograd.grad(y, x, create_graph=True)    # <- z = 2x

print("dy/dx = ", z[0].detach().numpy())
z[0].backward()
print("dz/dx = ", x.grad.numpy())    # <- dz/dx = 2
```

当然、偏微分だって出来ます。 

$$
z = x^2y + 3xy^5 + x^3 \\ \frac{\partial z}{\partial x} = 2xy + 3y^5 + 3x^2 \\ \frac{\partial z}{\partial y} = x^2 + 15xy^4
$$

```python
x = torch.tensor(1.0, requires_grad=True)
y = torch.tensor(1.0, requires_grad=True)

z = x**2 * y + 3*x*y**5 + x ** 3

z.backward()

print("dz/dx = {}".format(x.grad))
print("dz/dy = {}".format(y.grad))

```

### 最適化

ニューラルネットの学習には最適化の計算が必須です。 当然、PyTorchにも様々な最適化アルゴリズムが実装されています。

例えば、この式の最小値を求めてみましょう。

$$
y = 3x^2 + 6x - 9
$$

```python
import torch.optim as optim
import matplotlib.pyplot as plt


def f(x):
    return 3 * x ** 2 + 6 * x - 9
    
a = torch.tensor(10.0, requires_grad=True)
optimizer = optim.SGD([a], lr=0.1)

for step in range(20):
    optimizer.zero_grad()
    out = f(a)
    out.backward()
    optimizer.step()

print(a)

plt.figure(figsize=(15, 10), facecolor="azure")
plt.plot(tmp, f(tmp), ms=10)
plt.plot(a.detach().numpy(), f(a.detach().numpy()), marker="^", ms=20)
plt.xticks(torch.arange(-5.0, 6.0, 1))
plt.grid()
plt.show()
```

### PyTorch with GPU

PyTorchで、どうやってGPUを使うかを見ていきましょう。  
まずは、CPUで行列の積を求めてみます。  
そもそも、行列積の計算は オーダ $O\(n^3\) $ です。 愚直にCPUでやると遅い。

```python
import time

a = torch.randn(512, 1024)    # 正規分布から値をサンプリング。512 × 1024 の2次元配列を生成。
b = torch.randn(1024, 512)    # 1024 × 512 の2次元配列を生成。

start = time.time()

c = torch.mm(a, b)    # 2次元の行列同士の積を計算

print("処理時間: {:.4f}s ".format(time.time() - start))
```

次にGPUにデータを送って計算させてみます。

GPUにデータを載せるには、`torch.Tensor` オブジェクトが持つ `.cuda()` メソッドを使います。 さらに一般化したメソッドに、 `.to(device)`もあります。

```python
a_gpu = torch.randn(512, 1024).cuda()
b_gpu = torch.randn(1024, 512).cuda()

start = time.time()

c_gpu = torch.mm(a_gpu, b_gpu)

print("処理時間: {:.4f}s ".format(time.time() - start))

```

ちなみに、CPUとGPU別々にデータが格納されているなら、同じ場所にデータを置いてあげないと計算できません。

```python
cpu = torch.tensor([10])
gpu = torch.tensor([10]).cuda()

cpu + gpu # <- Errorが起こる

```

{% hint style="info" %}
GPUが管理するメモリ上にあるデータをCPUが管理するメモリー上に移すには

```text
x = torch.tensor(...)
x = x.cpu()
```

CPUが管理するメモリ上にあるデータをGPUが管理するメモリ上に移すには

```python
x = torch.tensor(...)
x = x.cuda()
```

を実行します。

また、GPUが実行可能なら自動的に変数をGPUに載せていきたいのなら

```python
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
x = torch.tensor(...)
x = x.to(device)
```

とすれば、OKです。
{% endhint %}



`一通り`PyTorch`の使い方を学んだので次から早速ニューラルネットを実装してみましょう`

