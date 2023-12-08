# Learning Ocaml

# References

- https://ja.wikipedia.org/wiki/OCaml
- https://ymotongpoo.hatenablog.com/entry/20111105/1320506449

# Ocamlとは

- 純粋関数
    - 破壊的な操作が一切ないコードは一般的に読み解くのが簡単
    - コード内でのやり取りや依存関係を明確で管理が楽
    - Ocamlはバランスを保っている
- 強い型(Haskellと同等もしくはHaskell以上に)
    - 強い静的型付け
    - C, C++, Javaと比較して速くエラーを起こしにくい
    - テストではかなり見つけにくいようなバグを事前に発見できる
- 素早くプロトタイプを作るような仕事にとても適している
    - 短いコードは読みやすく、書きやすく、維持管理しやすい。Ocamlは徹底している
    - 小さくて、簡潔で、理解しやすいシステムを作ることに向く。可読性を重要視するならOcamlが向いている。
- パフォーマンスはJavaと同等あるいはそれよりも上
    - インクリメンタルGCがある


# なぜ関数型を選ぶか

# 基本文法

`.ml`ファイルを実行

```shell
ocaml src/hello.ml
```

```shell
$ ocamlc hello.ml -o hello
```


