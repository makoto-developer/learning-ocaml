# Learning Ocaml

# References

- https://ja.wikipedia.org/wiki/OCaml
- https://ymotongpoo.hatenablog.com/entry/20111105/1320506449

# Ocamlとは

## 公式サイト
- https://ocaml.org/
- https://caml.inria.fr/

## 開発元
- NRIA（フランス国立情報学自動制御研究所）
- 過去40 年間以上に渡ってに開発

## 特徴

信頼性

- プログラムの安全性と信頼性を念頭に置いて設計された汎用プログラミング言語

純粋関数

- 破壊的な操作が一切ないコードは一般的に読み解くのが簡単
- コード内でのやり取りや依存関係を明確で管理が楽
- Ocamlはバランスを保っている

強い静的型付け

- Haskellと同等もしくはHaskell以上に
- C, C++, Javaと比較して速く、エラーを起こしにくい
- テストではかなり見つけにくいようなバグを事前に発見できる

命令型, オブジェクト指向を備えている

- 関数型だけでなく、命令型、およびオブジェクト指向のプログラミング スタイルをサポート

関数型

- 代数データ型とパターンマッチング
    - 複雑なデータ構造を定義および操作可能にする
- 素早くプロトタイプを作るような仕事にとても適している
    - 短いコードは読みやすく、書きやすく、維持管理しやすい、をOcamlは徹底している
    - 小さくて、簡潔で、理解しやすいシステムを作ることに向く。可読性を重要視するならOcamlが向いている。

パフォーマンス

- パフォーマンスはJavaと同等あるいはそれよりも上
    - インクリメンタルGCがある
    - 自動メモリ管理のための世代別ガベージコレクションを備えている
- コンパイラは複雑な最適化を必要としない
    - JITコンパイルの複雑さを必要とせずに、容易にパフォーマンスの高いコードを生成する
    - また、ランタイムはシンプルで高い移植性を備えている

# Version

- 最新 -> `5.1.0`
- LTS -> `4.14.1`

# なぜ関数型プログラミングなのか

- 関数を組み合わせることでアプリケーションを実装できる
- イミュータブルな小さな純粋関数で実装すると、引数と結果が必ず一致してテストしやすくなる。可読性が向上する。

# インストール方法

```shell
$ asdf plugin add ocaml
$ asdf install
```

# 基本文法

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

コメント1

```ocaml
(*
    ブロックコメント
    ブロックコメント
    ブロックコメント
*)
```

コメント2

```ocaml
(**
    Ocamldoc
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
val name : st"ing = "makoto-developer"
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
|char|1文字|`'a';;`|半角英数字(ASCIIコード)|
|string|文字列|`"abcde";;`||
|bool|bool型|`let is_check = true`||
|uint|???(型名が不明)|`();;`|voidと同じ意味|
|tuple|タプル型|`("ok", 200)`||
|list|リスト|`[1; 2; 3;]`|リストは同じ型じゃないとダメ|
|array|配列|`[\|1; 2.5; "foo";\|]`|配列は全ての型が一致しなくていい|

演算子

|operator|sample|note|
|:---|:---|:---|
|`+` `-` `*` `/`|`1+2;;`|整数の場合|
|`+.` `-.` `*.` `/.`|`1.1 +. 2.2;;`|実数の場合|
|`<(=<)` `>(=>)` `=` `<>` `&&` `\|\|` `not`|`not (5 >= 10)`|比較|

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

- グローバル変数は関数の外で定義された変数
- 寿命としては宣言された位置からそのソースの終端まで
- 対話式コンパイラで`#`の次の位置から宣言した変数はグローバル変数となる

```ocaml
(*
    let 変数名 = 値
*)

let pi = 3.14;;
```

ローカル変数

- ローカル変数は関数内で宣言された変数
- 寿命は宣言した位置からその関数の終端まで
- 書式は宣言の後ろに`in`を記述
- 数を宣言したい場合は式の後ろに更に`in`を追加

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

型を定義する

- 型名は小文字から始まる必要がある

```ocaml
type t = float * float
```

`variant`型

- タグをつける事ができる
- タグの名前は大文字で始める
- 名前をつけてあらかじめ宣言をして必要がある
- タグ毎に`|`で区切る

```ocaml
# type day = Mon | Tue | Wed | Thu | Fri | Sat | Sun;;
type day = Mon | Tue | Wed | Thu | Fri | Sat | Sun

# type angle = Degrees of float | Radian of float;;
type angle = Degrees of float | Radian of float

# (** variantを使って再帰を書く*);;
# (** 'a は型変数と呼ばれる *);;
# type 'a bintree = Leaf of 'a | Node of 'a bintree * 'a bintree;;
type 'a bintree = Leaf of 'a | Node of 'a bintree * 'a bintree
# Leaf 3;;
- : int bintree = Leaf 3
# Node ((Leaf "abc"), (Node ((Leaf "def"), (Leaf "ghi"))));;
- : string bintree = Node (Leaf "abc", Node (Leaf "def", Leaf "ghi"))
#
```

`record`型

- いわゆるStruct
- `type 型名 = {フィールド名1:型1; フィールド名2:型2; ...}`で宣言

```ocaml
#  type point = { x:float; y:float; color:int };;
type point = { x : float; y : float; color : int; }
# let p = {x=3.5; y=2.8; color=3};;
val p : point = {x = 3.5; y = 2.8; color = 3}
# p.x *. p.y;;
- : float = 9.79999999999999893#
```

組み込み関数

```ocaml
# (** インクリメント *)
# succ;;
- : int -> int = <fun>
# succ 3;;
- : int = 4
```

引数1個を持つ関数

```ocaml
# let plusFive = function x -> x + 5;;
val plusFive : int -> int = <fun>
# plusFive 11;;
- : int = 16


# (** 省略形 *)
# let plusFile x = x + 5;;
val plusFile : int -> int = <fun>
```

2つ以上の引数を持つ関数

```ocaml
# let add = function x -> function y -> x + y;;
# let add = fun x y -> x + y;;
# let add x y = x + y;;
```

例外型

- これは一応型ということになっているらしい
- `exception`キーワードを使う


```ocaml
# exception Wow of string;;
# let say command =
    if command = "opps" then
      raise (Wow "Be careful!!")
    else
      print_string command;;
# say "opps";;
Exception: Wow "Be careful!!".
# say "hello";;
hello- : unit = ()
#
```

ref 型

- ポインタを取得できる(変数の参照)
- 破壊的、らしい(よくわからん)

```ocaml
# let a = ref 0;;
val a : int ref = {contents = 0}
# a := 13;;
- : unit = ()
# !a;;
- : int = 13
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

