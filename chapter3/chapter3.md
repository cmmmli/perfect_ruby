# 3章(制御構造/メソッド/組み込み関数) memos

- || よりも && のほうが優先度が高い

- 'alice' === /a/ と /a/ === 'alice' では結果が異なる
  レシーバが文字列であるか正規表現であるかで===メソッドの振る舞いが変わるため

- [begin...end]で囲んで後置whileやuntilを使うと最初に必ずbeginの中が実行される
```
begin
  process1
  process2
end while needed?
```

- 繰り返しの中で使えるやつたち
  - break
  - next
  - redo

- `if $0 == __FILE__ と return unless $0 == __FILE__ が同じ`

### 例外処理基本

```
raise 'error!'                 # RuntimeError: error!
raise StandardError, 'error!'  # StandardError: error!

begin
  do\_process                   # 例外が発生する可能性のある何らかの処理
rescue => e
  puts "Error occurred (#{e.class})"
end

e.class         # => StandardError
e.message       # => "例外が発生しました"
e.backtrace     # => ["sample.rb:4:in `meth'", "sample.rb:9:in `<main>'"]
```

- begin節で
  - ensure \- 例外が発生してもしなくても必ず実行される
  - else   \- 例外が発生しなかった場合実行される

- ensure節は実行されるが戻り値にはならない

- 大域脱出 => catch/throw

### [&.]メソッド呼び出し(lonely operator)

```
people = %w(alice bob calol)

person_0th = people[0]      # 'alice'
person_9th = people[9]      # nil

person_0th&.capitalize      # "Alice"
person_0th.capitalize       # "Alice"

person_9th&.capitalize      # nil
person_9th.capitalize       # NoMethodError: undefined method `capitalize' for nil:NilClass
```

- メソッドの定義で仮引数の頭に\*を付けるとそのメソッドは任意の数の引数を配列として受け取れるようになる

- メソッドに対してブロックが与えられたかどうかを知るのは'block\_given?'メソッドを使う(yield if block\_given?)

```
p1 = Proc.new {|val| val.upcase }
p2 = :upcase.to_proc

p1.call('hi')     # => "HI"
p2.call('hi')     # => "HI"
```

```
頭に**をつけた仮引数は仮引数にないキーワード引数を1つのハッシュにまとめて受け取る

?> def keywords_with_options(alice: nil, bob: nil, **others)
>>   {alice: alice, bob: bob, others: others}
>> end
>>
?> keywords_with_options alice: 'アリス', bob: 'ボブ', charlie: 'チャーリー', dave: 'デイブ'
=> {:alice=>"アリス", :bob=>"ボブ", :others=>{:charlie=>"チャーリー", :dave=>"デイブ"}}
>>
?> keywords_with_options alice: 'アリス', bob: 'ボブ'
=> {:alice=>"アリス", :bob=>"ボブ", :others=>{}}
```

#### 仮引数の順序

1. 通常の引数/省略可能な引数
1. \*で指定できる可変長の引数
1. キーワード引数
1. \*\*で指定できるハッシュの引数
1. &で指定できるブロックの引数


### 外部コマンドの実行

- Kernel.#`
  戻り値は外部コマンドの標準出力
- Kernel.#system
  外部コマンドの終了ステータスが0 or 1でtrue or falseが戻り値になる
- Kernel.#exec
  実行中のRubyプロセスは外部コマンドのプロセスに変わる(制御が戻ってこない)
- Kernel.#spawn
  外部コマンドの終了を待たずに子プロセスIDを即座に返す。返り値はRubyの標準出力or標準エラー出力
- Process.#waitpid
  与えられたpidのプロセスが終了するのを待つ
