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

コメント

```ocaml
(*
    ブロックコメント
    ブロックコメント
    ブロックコメント
*)
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

`^`演算子で文字列を結合できる

```ocaml
# let greeting = fun name -> "Hi " ^ name ^ "!";;
val greeting : string -> string = <fun>
# greeting "makoto-developer";;
- : string = "Hi makoto-developer!"
```

データ型

|type|name|example|note|
|:---|:---|:---|:---|
|int|整数|`1;;`|32bit/64bitで最大値が変わる。`max_int`、`min_int`で確認できる|
|float|実数|`3.1415;;`|`max_float`、`min_float`で確認できる|
|char|1文字(半角英数字(ASCIIコード))|`'a';;`||
|string|文字列|`"abcde";;`||
|bool||||

演算子

|operator|sample|note|
|:---|:---|:---|
|`+` `-` `*` `/`|`1+2;;`|整数の場合|
|`+.` `-.` `*.` `/.`|`1.1 +. 2.2;;`|実数の場合|
|`<(=<)` `>(=>)` `=` `<>` `&&` `||` `not`|not (5 >= 10)|比較|

関数その3

関数式の書き方
(関数名は小文字の英字から開始する必要がある)

```ocaml
(*
  let 関数名 引数 = 式
*)

# let addSum v1 v2 = v1 + v2;;
val addSum : int -> int -> int = <fun>
# addSum 10 19;;
- : int = 29
#
```

グローバル変数

- グローバル変数は関数の外で定義された変数です。
- 寿命としては宣言された位置からそのソースの終端までとなります。
- 対話式コンパイラで「#」の次の位置から宣言した変数はグローバル変数として扱われます。

```ocaml
(*
    let 変数名 = 値
*)

let pi = 3.14;;
```

ローカル変数

- ローカル変数は関数内で宣言された変数
- 寿命は宣言した位置からその関数の終端まで使用することができます。
- 書式は宣言の後ろに「in」と「式」を記述します。
- 数を宣言したい場合は式の後ろに更に「in」と「式」を追加します。

```ocaml
(*
    let 変数名 = 値 in 式
*)

# let circleLength radian =
    let pi = 3.14 in
    let diameter = 2.0 *. pi in
    diameter *. radian;;
val circleLength : float -> float = <fun>
# circleLength 10.0;;
- : float = 62.8000000000000043
```

```ocaml
```

```ocaml
```

```ocaml
```

```ocaml
```


