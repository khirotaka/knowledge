# Transformer

Google AIが2017年に発表した論文"[Attention is all you need.](https://arxiv.org/abs/1706.03762)" で提案されたネットワーク構造。
自然言語界隈で当時一般的であった、RNNやCNNを一切使わずに当時のSoTAを達成。
現在では、BERTやTransformer-XL、GPT-2、ALBERTにRoBERTaなどなど、最新のNLP分野のベースとなっているモデル。
自然言語界隈では知ってて当然なネットワーク構造。

## 構造
Transformerの構造はかなり簡単で、ニューラルネットの基礎と行列の計算さえ分かっていれば理解できるはず。
よく分からないという方は、
  1. ゼロから作るDeep Learning
  1. ゼロから作るDeep Learning ②自然言語処理編
  
で勉強してからまた戻ってきて欲しい。

### Attention
Transformerを語る上で避けて通れないのが、Attention構造である。
前述の通り、TransformerはRNN・CNNを使う代わりにAttentionをふんだんに使っている。

このAttentionについて説明する。

#### Encoder-Decoderモデルを振り返る
ゼロつく2 を学んだ人なら作ったこともあるだろう、いわゆるSeq2Seq構造は
  1. Encoderは受け取った入力 <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{X}\&space;(x_1,&space;x_2,&space;...,&space;x_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{X}\&space;(x_1,&space;x_2,&space;...,&space;x_n)" title="\mathbf{X}\ (x_1, x_2, ..., x_n)" /></a>
  を受け取ると、それを<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{Z}\&space;(z_1,&space;z_2,&space;...,&space;z_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{Z}\&space;(z_1,&space;z_2,&space;...,&space;z_n)" title="\mathbf{Z}\ (z_1, z_2, ..., z_n)" /></a>
  に変換する。
  1. Decoderは<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{Z}\&space;(z_1,&space;z_2,&space;...,&space;z_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{Z}\&space;(z_1,&space;z_2,&space;...,&space;z_n)" title="\mathbf{Z}\ (z_1, z_2, ..., z_n)" /></a>
  を受け取ると、それぞ、<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{Y}\&space;(y_1,&space;y_2,&space;...,&space;y_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{Y}\&space;(y_1,&space;y_2,&space;...,&space;y_n)" title="\mathbf{Y}\ (y_1, y_2, ..., y_n)" /></a>
  に変換する。
  
