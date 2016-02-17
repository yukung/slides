class: center middle
# CoffeeScript チュートリアル

---
class: center middle
# @yukung

---
# CoffeeScript とは？

* 冗長になりがちな JavaScript をより簡単に書くための言語
* 正確にはトランスパイラと言い、CoffeeScript を元に JavaScript を生成するためのツール
* サイトは[ここ](http://coffeescript.org/)
* 作者は New York Times のエンジニア、Jeremy Ashkenas

---
class: center top
# この人

![Jeremy Ashkenas](http://b.vimeocdn.com/ts/441/643/441643406_1280.jpg)

---
class: center middle
# この人は他にも

* Underscore.js
* Backbone.js

とかを作ったすごい人

---
# 特徴

* Ruby や Python に似てる
* ブロックをインデントで表す
* JavaScript の function を -> で表せる
* 文末のセミコロンが要らない
* 引数の括弧が省略できる（一部できない時もある）
* クラスを作れる
* 記述量が減ってすっきりして読みやすい
* JavaScript よりも誰が書いても書き方がブレない

```coffeescript

```
---
class: center middle
# ということで

---
class: center middle
# CoffeeScript を書こう

---
# 試せます

* [公式サイト](http://coffeescript.org/)から、「Try COFFEESCRIPT」というリンクを押すとブラウザ上でそのまま実行しながら、どういう JavaScript に変換されるかをリアルタイムに見ることができます
* 今日の内容もそのままコードをコピペすれば試せるのでやってみて🎉

---
class: center middle
# それでは GO

--
# まずコメント

```coffeescript
# 行コメント。コンパイル時に消去される

###
  複数行コメント。
  コンパイル時に消去されず、出力先にも残る。
###
```

---
# 変数

```coffeescript
# 変数は var が要らない
# スコープは Ruby と同じ。
hoge = "hoge"

outer = 1
changeNumbers = ->
  inner = -1                # inner は関数内で宣言される。
  outer = 10                # この場合 outer は宣言されず、外のスコープのouterが上書きされる。
inner = changeNumbers()     # inner は10になる
```

---
# 文字列リテラル

```coffeescript
# 文字列リテラル
'this is string'
# "" は #{...} を評価する
"this is #{2 + 3}"

name = 'yukung'
'#{name}'
"my name is #{name}"
```

---
# 文字列リテラル（複数行）

```coffeescript
# 複数行の文字列リテラルは ''' または """ 
text = """
  aaa
  #{'bbb'}
  ccc
"""
```

---
# インデントがずれると

```coffeescript
# インデントが少ない行に他の行が調整される
text = """
    aaa
#{'bbb'}
  ccc
"""```

---
# JavaScript リテラル

```coffeescript
# JavaScript リテラル（JavaScript コードを CoffeeScript に埋め込む）
`
function func() {
  var i = 3;
  return i;
}
`
```

---
# 配列

```coffeescript
# 配列
a = [1, 2, 3]
# インデントを使って表現することもできる
b = [
  1
  2
  3
]
```

---
# レンジ（範囲）

```coffeescript
# レンジ
[1..3]
[0...3]
# for 文で使うと
arr = [0..3]
for i in [0...arr.length]
  console.log i
```

---
# 配列のスライス

```coffeescript
# 配列のスライス
arr = ['a', 'b', 'c', 'd', 'e']
arr[1..3] # => arr.slice(1, 4);
# => [ 'b', 'c', 'd' ]
```

---
# オブジェクトリテラル

```coffeescript
# オブジェクトリテラル
# JavaScript で obj = {a: 1, b: 2, c: 3} はブロックが自明な限り中括弧を省略できる
obj = a: 1, b: 2, c: 3
# インデントを使って表現できる。この場合はカンマを省略できる。
# ネストを深くすることでオブジェクトのネストも表現できる
# インデントでブロックを表現することをオフサイドルールと呼ぶ
obj2 =
  a: 4
  b: 5
  c:
    d: 7
    e: 8
```

--

```coffeescript
# 関数の引数として適用することもできる
###
func({
  a: 1,
  b: 2
})
###
func
  a: 1
  b: 2
```

---
# スコープ上のオブジェクト宣言

```coffeescript
# スコープ上のオブジェクト宣言
a = 3
b = 2
obj = {a, b, c: 1} # => {a: 3, b: 2, c: 1}
# this のメンバに対しても適用可能
# @ は this と同じ意味
f = ->
  @a = 3
  @b = 2
  obj = {@a, @b, c: 1} # => {a: this.a, b: this.b, c: 1}
```

---
# 真偽値

```coffeescript
# 真偽値

console.log true
console.log false
console.log on
console.log off
console.log yes
console.log no
```

---
# 比較演算子

```coffeescript
1 == true # => 1 === true

1 is true # => ===
1 isnt true # => !==
```

---
# 論理演算子

```coffeescript
# 論理演算子

1 is 2 or 3 is 3 # => ||
2 is 2 and 4 isnt 3 # => &&
```

---
# ? 演算子

```coffeescript
# ?演算子

a = null ? true # => true
b = undefined ? true # => true
c = {} ? true # => {}
# CoffeeScript において false は明示的に存在する null ではない値
d = false ? {} # => false
```

---
# 三項演算子

```coffeescript
a = if b then 1 else 2
```

---
# 演算子他にも

| JavaScript | CoffeeScript |
| ---------- | ------------ |
| === | is |
| !== | isnt |
| ! | not |
| && | and |
| || | or |
| true | true,yes,on |
| false | false,no,off |
| of | in |
| ** | Math.pow(a,b) |
| // | Math.floor(a / b) |
| %% | (a % b + b) % b |

なるべく英語の文のように読めるように配慮されてます

---
# if文

```coffeescript
# 1行で書く
if hoge then console.log "hoge"

# 後置if
hoge = 5
console.log "hoge" if hoge is 5 # hogeと出力される

# unless（ifの反対）
unless false
  console.log "hoge" # hogeと出力される
```

---
# switch文

```coffeescript
# case, default ではなくて when と else
switch val
  when 1
    console.log "1"
  when 2 then console.log "2"
  when 3,4,5
    console.log "3,4,5"
  else
    console.log "else"
```

---
# for文

```coffeescript
# range を使って回す
for i in [0..9]
  console.log i

# 要素をスキップ
for i in [0..10] by 2
  console.log i

# 逆からループ
array = [0, 2, 4, 9]
for v, i in array by -1
  console.log "i = " + i + " v = " + v
```

--

```coffeescript
# 配列のループ
array = [
  'one'
  'two'
  'three'
]
for i in [0...array.length]
  console.log array[i]

# こっちのほうが一般的
array = [
  'one'
  'two'
  'three'
]
for value in array
  console.log value

# インデックス（添字）が必要な場合
array = [
  'one'
  'two'
  'three'
]
for value,i in array
  console.log "i=" + i + ",value = " + value
```

--

```coffeescript
# 一行for
for i in [0..9] then console.log i

# 後置for
console.log i for i in [0..9]

# 要素をフィルタリング
array = [0, 1, 2, 3, 4, 5]
array2 = for value in array when value < 3 then value
console.log array2
```

---
# オブジェクトのループ

```coffeescript
# in じゃなくて of を使う
obj =
  'one'   : 1
  'two'   : 2
  'three' : 3
for key,value of obj
    console.log "key=" + key + ",value = " + value
```

---
# while文

```cofffeescript
count = 0
while count < 15
  count++

console.log count  # -> 15

# 後置while
count = 10
console.log "count = #{count}" while count--
```

---
# until文（whileの逆）

```coffeescript
count = 0
count++ until count >= 10
console.log count  #10
```

---
# 関数

```coffeescript
# 返り値は最後に処理した値になる。（関数の最後の行とは限らない）
func = ->
  sum = 1 + 1

# 返り値なしの場合は return を付ける
func = ->
  sum = 1 + 1
  return

# 引数を持つ場合
func = (arg1, arg2) ->
  sum = arg1 + arg2

# デフォルト引数
func = (arg1 = 1, arg2 = 5) ->
  sum = arg1 + arg2

# 可変長引数
func = (x,args...)->
  console.log args
```

---
# クラス

```coffeescript
# 宣言
class Hoge

# インスタンス生成
hoge = new Hoge

# コンストラクタの定義
class Hoge
  fuga : "fuga"
  constructor: (name) ->
    @name = name

# クラスの拡張
class Fuga extends Hoge

# super() でスーパークラスの関数を呼べる
class Hoge
  constructor: (name) ->
    @name = name

class Fuga extends Hoge
  constructor: ->
    super("Fuga")
```

---
class: center middle
# これで Hubot スクリプト書けるようになる！！１

---
class: center middle
# Thankyou for listening!
