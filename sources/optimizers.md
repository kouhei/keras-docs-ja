## オプティマイザ（最適化アルゴリズム）の利用方法

オプティマイザ（最適化アルゴリズム）はモデルをコンパイルする際に必要となるパラメータの1つです:

```python
from keras import optimizers

model = Sequential()
model.add(Dense(64, kernel_initializer='uniform', input_shape=(10,)))
model.add(Activation('tanh'))
model.add(Activation('softmax'))

sgd = optimizers.SGD(lr=0.01, decay=1e-6, momentum=0.9, nesterov=True)
model.compile(loss='mean_squared_error', optimizer=sgd)
```

上記の例のように，オプティマイザのインスタンスを `model.compile()` に渡す，もしくは，オプティマイザの名前を渡すことができます．後者の場合，オプティマイザのデフォルトパラメータが利用されます．

```python
# オプティマイザを名前で指定すると，デフォルトパラメータが利用されます
model.compile(loss='mean_squared_error', optimizer='sgd')
```

----

## Kerasのオプティマイザの共通パラメータ

`clipnorm`と`clipvalue`はすべての最適化法についてgradient clippingを制御するために使われます:

```python
from keras import optimizers

# All parameter gradients will be clipped to
# a maximum norm of 1.
sgd = optimizers.SGD(lr=0.01, clipnorm=1.)
```

```python
from keras import optimizers

# All parameter gradients will be clipped to
# a maximum value of 0.5 and
# a minimum value of -0.5.
sgd = optimizers.SGD(lr=0.01, clipvalue=0.5)
```

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L130)</span>
### SGD

```python
keras.optimizers.SGD(lr=0.01, momentum=0.0, decay=0.0, nesterov=False)
```

確率的勾配降下法オプティマイザ．

モーメンタム，学習率減衰，Nesterov momentumをサポートした確率的勾配降下法．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
- __momentum__: 0以上の浮動小数点数．モーメンタム．
- __decay__: 0以上の浮動小数点数．各更新の学習率減衰．
- __nesterov__: 真理値. Nesterov momentumを適用するかどうか．

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L193)</span>
### RMSprop

```python
keras.optimizers.RMSprop(lr=0.001, rho=0.9, epsilon=None, decay=0.0)
```

RMSPropオプティマイザ．

デフォルトパラメータのまま利用することを推奨します．
（ただし，学習率は自由に調整可能です）

RMSPropはリカレントニューラルネットワークに対して良い選択となるでしょう．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
- __rho__: 0以上の浮動小数点数．
- __epsilon__: 0以上の浮動小数点数．微小量．`None`ならばデフォルトで`K.epsilon()`．
- __decay__: 0以上の浮動小数点数．各更新の学習率減衰．

__参考文献__

- [rmsprop: Divide the gradient by a running average of its recent magnitude](http://www.cs.toronto.edu/~tijmen/csc321/slides/lecture_slides_lec6.pdf)

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L260)</span>
### Adagrad

```python
keras.optimizers.Adagrad(lr=0.01, epsilon=None, decay=0.0)
```

Adagradオプティマイザ．

デフォルトパラメータのまま利用することを推奨します．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
- __epsilon__: 0以上の浮動小数点数．`None`ならばデフォルトで`K.epsilon()`．
- __decay__: 0以上の浮動小数点数．各更新の学習率減衰．

__参考文献__

- [Adaptive Subgradient Methods for Online Learning and Stochastic Optimization](http://www.jmlr.org/papers/volume12/duchi11a/duchi11a.pdf)

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L319)</span>
### Adadelta

```python
keras.optimizers.Adadelta(lr=1.0, rho=0.95, epsilon=None, decay=0.0)
```

Adadeltaオプティマイザ．

デフォルトパラメータのまま利用することを推奨します．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
    デフォルト値を推奨します．
- __rho__: 0以上の浮動小数点数．
- __epsilon__: 0以上の浮動小数点数．微小量．`None`ならばデフォルトで`K.epsilon()`．
- __decay__: 0以上の浮動小数点数．各更新の学習率減衰．

__参考文献__

- [Adadelta - an adaptive learning rate method](http://arxiv.org/abs/1212.5701)

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L392)</span>
### Adam

```python
keras.optimizers.Adam(lr=0.001, beta_1=0.9, beta_2=0.999, epsilon=None, decay=0.0, amsgrad=False)
```

Adamオプティマイザ．

デフォルトパラメータは提案論文に従います．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
- __beta_1__: 浮動小数点数, 0 < beta < 1. 一般的に1に近い値です．
- __beta_2__: 浮動小数点数, 0 < beta < 1. 一般的に1に近い値です．
- __epsilon__: 0以上の浮動小数点数．微小量．`None`ならばデフォルトで`K.epsilon()`．
- __decay__: 0以上の浮動小数点数．各更新の学習率減衰．
- __amsgrad__: 論文"On the Convergence of Adam and Beyond"にあるAdamの変種であるAMSGradを適用するかどうか．

__参考文献__

- [Adam - A Method for Stochastic Optimization](http://arxiv.org/abs/1412.6980v8)
- [On the Convergence of Adam and Beyond](https://openreview.net/forum?id=ryQu7f-RZ)

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L481)</span>
### Adamax

```python
keras.optimizers.Adamax(lr=0.002, beta_1=0.9, beta_2=0.999, epsilon=None, decay=0.0)
```

Adamaxは，Adamの提案論文の7節で提案されたAdamaxオプティマイザ．

これは無限ノルムに基づくAdamの拡張です．デフォルトパラメータは提案論文に従います．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
- __beta_1/beta_2__: 浮動小数点数, 0 < beta < 1. 一般的に1に近い値です．
- __epsilon__: 0以上の浮動小数点数．微小量．`None`ならばデフォルトで`K.epsilon()`．
- __decay__: 0以上の浮動小数点数．各更新の学習率減衰．

__参考文献__

- [Adam - A Method for Stochastic Optimization](http://arxiv.org/abs/1412.6980v8)

----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L558)</span>
### Nadam

```python
keras.optimizers.Nadam(lr=0.002, beta_1=0.9, beta_2=0.999, epsilon=None, schedule_decay=0.004)
```

Nesterov Adamオプティマイザ．

よく似たAdamはRMSPropとmomumtumを組み合わせたもので，NadamはRMSPropとNesterov momentumを組み合わせたものです．

デフォルトパラメータは提案論文に従います．
デフォルトパラメータのまま利用することを推奨します．

__引数__

- __lr__: 0以上の浮動小数点数．学習率．
- __beta_1/beta_2__: 浮動小数点数, 0 < beta < 1. 一般的に1に近い値です．
- __epsilon__: 0以上の浮動小数点数．微小量．`None`ならばデフォルトで`K.epsilon()`．

__参考文献__

- [Nadam report](http://cs229.stanford.edu/proj2015/054_report.pdf)
- [On the importance of initialization and momentum in deep learning](http://www.cs.toronto.edu/~fritz/absps/momentum.pdf)
----

<span style="float:right;">[[source]](https://github.com/keras-team/keras/blob/master/keras/optimizers.py#L644)</span>
### TFOptimizer

```python
keras.optimizers.TFOptimizer(optimizer)
```

TensorFlowのオプティマイザのためのラッパークラス．
