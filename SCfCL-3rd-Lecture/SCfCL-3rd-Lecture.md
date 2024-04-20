---
marp: true
math: katex
paginate: true
---

# コンピュータリテラシ発展 〜Pythonを学ぶ〜

## 第3回：Pythonを始めよう

情報学部 情報学科 情報メディア専攻
清水 哲也 ( shimizu@info.shonan-it.ac.jp )

---

# 今回の授業内容

---

# 今回の授業内容

- 前回の課題解説
- 同じ処理を繰り返し行う
- 課題

---

# 前回の課題解説

---

# 前回の課題解説

- 前回の課題の解答例を示します
- 解答例について質問があればご連絡ください

## 解答例

（後でURLを貼り付ける）

---

# 同じ処理を繰り返し行う

---

# 要素の数だけ処理を繰り返す

- あるデータ構造に格納されている要素（オブジェクト）の数だけ，繰り返し処理をする = **forループ**
- 繰り返し（イテレート）可能なオブジェクトを **イテラブル** と呼ぶ

```python
for 変数 in イテラブル:
    ブロック
```

**注意点**
- イテラブルの後には必ず「:（コロン）」をつけてください
- ブロック（処理）の前にはインデントを入れてください

---

# 要素の数だけ処理を繰り返す（リストのforループ）

- リストを用いたforループ
- リストオブジェクトに格納されている要素の数だけ繰り返します

```python
number = [1, 2, 3, 4, 5]
for i in number:
    print('test')
```

- 要素の数だけ繰り返すのでリストの要素を扱うこともできます

```python
number = [1, 2, 3, 4, 5]
for i in number:
  print(i)
```

- リストは数値だけでなく文字列でも要素数分を繰り返すことができます

```python
fruits = ['apple', 'orange', 'banana']
for fruit in fruits:
  print(fruit)
```

---

# 要素の数だけ処理を繰り返す（range()関数）

- 「 **range(開始する値, 終了する値)** 」と指定すると，開始する値から終了する値を変えない範囲で1ずつカウントアップされます
  - 例： ``range(0, 3)`` を実行してみましょう
- ここで「開始する値」が「0」の場合は省略することができます
  - 例： ``range(0, 3)`` = ``range(3)`` 同じ結果になることを確認してみましょう

```python
list(range(0, 3))
list(range(3))
```

- ``range()`` 関数とforループを使ってみましょう

```python
for count in range(3):
    print(count)
```

---

# 要素の数だけ処理を繰り返す（インデックスと要素）

- リスト型では **インデックス** で値を参照できます
- インデックスをforループで同時に取り出すことができます
- `enumerate()`関数を使うことでインデックスと要素を同時に取り出すことできます

```python
fruits = ['apple', 'orange', 'banana', 'grape']
for i, fruit in enumerate(fruits):
  print(i, fruit)
```

---

# 要素の数だけ処理を繰り返す（辞書のforループ）

- 辞書のforループの使い方には3つの方法があります
  - **キーだけ** を取り出す方法： `keys()`
  - **バリューだけ** を取り出す方法： `values()`
  - **キー** と **バリュー** を取り出す方法： `items()`

```python
fruits = {'apple':100, 'orange':200}
print(fruits.keys())
print(fruits.values())
print(fruits.items())
```

---

# 要素の数だけ処理を繰り返す（辞書のforループ）

- キーを取り出す方法
```python
fruits = {‘apple’:100,‘orange’:200,’banana’:300}
for fruit in fruits.keys():
  print(fruit)
```
- バリューを取り出す方法
```python
fruits = {‘apple’:100,‘orange’:200,’banana’:300}
for money in fruits.values():
  print(money)
```
- キーとバリューを取り出す方法
```python
fruits = {‘apple’:100,‘orange’:200,’banana’:300}
for fruit, money in fruits.items():
  print(fruit, money)
```

---

# 処理を繰り返す（条件が続く限り）



---

# 課題

---

# 課題2-1

- Moodleにある「SCfCL-2nd-prac.ipynb」ファイルをダウンロードしてColabにアップロードしてください
- 課題が完了したら「File」>「Download」>「Download .ipynb」で「.ipynb」形式でダウンロードしてください
- ダウンロードした.ipynbファイルをMoodleに提出してください
- 提出期限は **4月25日(木) 20時まで** です