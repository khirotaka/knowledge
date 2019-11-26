# Transformer

Google AIが2017年に発表した論文"[Attention is all you need.](https://arxiv.org/abs/1706.03762)" で提案されたネットワーク構造。 自然言語界隈で当時一般的であった、RNNやCNNを一切使わずに当時のSoTAを達成。 現在では、BERTやTransformer-XL、GPT-2、ALBERTにRoBERTaなどなど、最新のNLP分野のベースとなっているモデル。 自然言語界隈では知ってて当然なネットワーク構造。

### 構造

Transformerの構造はかなり簡単で、ニューラルネットの基礎と行列の計算さえ分かっていれば理解できるはず。 よく分からないという方は、 1. ゼロから作るDeep Learning 1. ゼロから作るDeep Learning ②自然言語処理編

で勉強してからまた戻ってきて欲しい。

#### Attention

Transformerを語る上で避けて通れないのが、Attention構造である。 前述の通り、TransformerはRNN・CNNを使う代わりにAttentionをふんだんに使っている。

このAttentionについて説明する。

**Encoder-Decoderモデルを振り返る**

ゼロつく2 を学んだ人なら作ったこともあるだろう、いわゆるSeq2Seq構造は

1. Encoderは受け取った入力 **X** を受け取ると、それを **Z** に変換する。
2. Decoderは **Z** を受け取ると、それを、Y に変換する。





書き途中



