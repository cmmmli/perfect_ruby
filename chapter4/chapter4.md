# chapter4 クラスとモジュール memos

- クラスメソッドの中では、クラスがselfになる

- initializeメソッドは自動的にprivate

- スーパークラスのメソッドには.サブクラスのメソッド呼び出しで受け取った引数が自動的に渡される

- メソッドのオーバーライドをしたとき、スーパークラスのメソッドにはサブクラスのメソッド呼び出しで受け取った引数が自動的に渡される

### モジュール

#### 特徴

- インスタンスを生成できない
- 継承できない

#### 用途

- 名前空間を作る
- モジュールのメソッドをあるクラスのインスタンスメソッドとして取り組む(Mix-in)
- モジュールのメソッドをあるオブジェクトの特異メソッド(クラスメソッド)として取り込む(extend)
- 特異メソッドやモジュール関数を定義して使う

#### モジュール関数

```
module MyFunctions
  def my_module_function
    puts 'Called!'
  end
  module_function :my_module_function
end


# or


module MyFunctions
  module_function

  def my_first_function
    puts 'first'
  end

  def my_second_function
    puts 'second'
  end
end
```
