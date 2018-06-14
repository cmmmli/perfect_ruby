# 主な組み込みクラス/モジュール

## Numeric

```
1 <=> 2 # => -1
1 <=> 1 # => 0
1 <=> 0 # => 1
```

- `Enumerable#sort`はブロックでソート方法をカスタマイズ出来る

```
%w(alice bob charlie).sort {|a, b|
  a.length <=> b.length
}   # => ["bob", "alice", "charlie"]
```

### 丸め操作

- ceil: 自身と等しいか、自身より大きい整数のうち最小のものを返す
- floor: 自身と等しいか、自身より小さい整数のうち最大のものを返す
- round: 自身に近い整数に丸める。2.3以前は四捨五入を行い、2.4以降はhalfオプションで偶数丸めが選択可能
- truncate: 自身と0の間で、自身に最も近い整数を返す

---

### Integer

- `'123'.to_i` or `Integer('456')`
Kernel.#Integerは例外を発生させる

---

```
20180604.digits  # => [4, 0, 6, 0, 8, 1, 0, 2]

7.digits(2)  # => [1, 1, 1]
31.digits(16)  # => [15, 1]
# Integer#digitsは、正の数値に対してのみ呼び出すことが可能。負の数には例外発生
```

## String

- `String#slice`のショートハンドとして`String#[]`を用いることも出来る

### 文字列の整形

```
str.strip   # 両端から除去
str.rstrip  # 右端から除去
str.lstrip  # 左端から除去
str.chomp   # 文字列の末尾にある改行コードを1つ取り除いた文字列を返す
str.chop    # 文字種にかかわらず文字列の末尾の1文字を取り除いた文字列を返す
str.squeeze # 文字列の中で連続した文字を1つにまとめる

str.downcase
str.upcase
str.swapcase
str.capitalize

str.sub(/regexp/, 'x')    # 最初に正規表現にマッチした部分を第二引数の文字列と置き換える
str.gsub(/regexp/, 'x')   # 全部置き換える

```

### 文字列の内部バッファサイズを指定する

```
s = String.new(capaciry: 10_000)

2_000.times do
  s << 'hello'
end
```

文字列をString.newで作成する際、内部バッファサイズを指定できる(Ruby2.4から)。
これによって、文字列への追記を繰り返すようね処理でメモリのアロケーションの頻発を抑えられる。
内部バッファのサイズはcapacityキーワード引数で指定する。

## Regexp

### グルーピングと後方参照/部分式呼び出し

```
/(B) to \1/ === 'B to B'  # => true

# $1 で直前にマッチしたグルーピングの文字列を取得できる
$1  # => "B"
```


`(?<label>pattern)`のように記述することで、ラベル付けできる。

```
/(?<number>[0-9]+)/ === 'abc-123'

Regexp.last_match[:number]  # => "123"
```

### オプションの指定

| オプション | 意味 |
| :----: | :---- |
| i | 大文字小文字の区別を行わない |
| o | 正規表現リテラルが最初に評価された際、一度だけ式展開を行う |
| x | 正規表現中の空白を無視し、 ＃をコメントとみなす |
| m | .に改行もマッチする。複数行モード |
| u | 正規表現をUTF-8として解釈する |
| s | 正規表現をShift-JISとして解釈する |
| e | 正規表現をEUC-JPとして解釈する |
| n | 正規表現をASCⅡとして解釈する |


## Comparable

比較演算のためのメソッドを提供

## Enumerable

ArrayやHash、Rangeなど、オブジェクトの集まりを表現するクラスにはEnumerableがincludeされている。


