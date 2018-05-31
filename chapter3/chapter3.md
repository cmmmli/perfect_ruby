# 3章memos

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


