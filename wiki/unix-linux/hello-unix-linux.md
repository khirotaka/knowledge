---
description: A 15 minute blitz
---

# Hello, Unix/Linux

多くの学生が1年生のプログラミング入門の授業でUnix/Linux likeな環境に触れたことがあります。そう、Cygwinです。しかし、公開されている論文実装やライブラリの多くは本物のUnix/Linux環境での動作を前提としている事が非常に多いです。ここでは、Unix/Linux初心者相手に基本的なコマンドを説明していきます。

### Terminal

まずターミナル\(端末\)を開いてみましょう。懐かしいウィンドウが開くはずです。

```text
user@machine:~$ 
```

まず、この文の意味を説明します。最初の `user` の部分は現在ログインしているユーザ名、`machine` は現在ログインしているコンピュータの名前、`~` の位置にはカレントディレクトリが入ります。ちなみに、`~` はホームディレクトリを意味します。

では、今いるディレクトリに何が含まれているを見てみましょう。

```text
user@machine:~$ ls
```

と入力してください。すると、

```bash
user@machine:~$ ls
Documents/    Downloads/    Desktop/    ....
```

といった結果が出てくるはずです。\(環境によっては日本語で表示されることがあります\)  
では、`Documents` ディレクトリに移ってみましょう。

```bash
user@machine:~$ ls
Documents/    Downloads/    Desktop/    ....
user@machine:~$ cd Documents/
user@machine:Documents$  
```

ディレクトリを移動できました。折角なので新しいディレクトリを作成してその中に入ってみましょう。

```bash
user@machine:Documents$ mkdir hello
user@machine:Documents$ cd hello
```

では、新しいファイルを作成してみましょう。Unix/Linux界隈では様々な宗教戦争が繰り広げられています。例えばエディタ戦争です。皆さん一度はVimやEmacsという名前を聞いた事があると思いますが、筆者はVim派なのでVimで説明していきたと思います。

```bash
user@machine:Documents$ vim hello.txt
```



