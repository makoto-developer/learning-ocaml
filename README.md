# Learning Ocaml

# References

- https://ja.wikipedia.org/wiki/OCaml
- https://ymotongpoo.hatenablog.com/entry/20111105/1320506449

# Ocamlとは

- 純粋関数
    - 破壊的な操作が一切ないコードは一般的に読み解くのが簡単
    - コード内でのやり取りや依存関係を明確で管理が楽
    - Ocamlはバランスを保っている
- 強い型(Haskellと同等もしくはHaskell以上に) 強い静的型付け
    - C, C++, Javaと比較して速くエラーを起こしにくい
    - テストではかなり見つけにくいようなバグを事前に発見できる
- 素早くプロトタイプを作るような仕事にとても適している
    - 短いコードは読みやすく、書きやすく、維持管理しやすい。Ocamlは徹底している
    - 小さくて、簡潔で、理解しやすいシステムを作ることに向く。可読性を重要視するならOcamlが向いている。
- パフォーマンスはJavaと同等あるいはそれよりも上
    - インクリメンタルGCがある


# なぜ関数型を選ぶか

# 基本文法

## OCamlを実行の実行方法

対話形式で実行

```shell
$ ocaml
```

コンパイルしないで実行

```shell
$ ocaml src/hello.ml
```

コンパイルして実行

```shell
$ ocamlc hello.ml -o hello

$ ./hello
```

クイックソートを実行

```ocaml
# let rec quicksort = function
   | [] -> []
   | pivot :: rest ->
       let is_less x = x < pivot in
       let left, right = List.partition is_less rest in
       quicksort left @ [pivot] @ quicksort right;;
val quicksort : 'a list -> 'a list = <fun>

# quicksort [1;4;5;3;];;
- : int list = [1; 3; 4; 5]
```

足し算

```ocaml
# 1+3;;
- : int = 4
```

変数

```ocaml
# let x = 11;;
val x : int = 11
```

関数

```ocaml
# let double x = x * 2;;
val double : int -> int = <fun>
# double 10;;
- : int = 20
```

文字列


```ocaml
# let name = "makoto-developer";;
val name : string = "makoto-developer"
```

関数その2

```ocaml
# let greeting = fun name -> "Hi " ^ name ^ "!";;
val greeting : string -> string = <fun>
# greeting "makoto-developer";;
- : string = "Hi makoto-developer!"
```

```ocaml
```

```ocaml
```

```ocaml
```

```ocaml
```

```ocaml
```

```ocaml
```

```ocaml
```


