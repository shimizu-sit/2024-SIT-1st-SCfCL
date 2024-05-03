---
marp: true
math: katex
paginate: true
---

# コンピュータリテラシ発展 〜Pythonを学ぶ〜

## 第4回：Pythonを始めよう

情報学部 情報学科 情報メディア専攻
清水 哲也 ( shimizu@info.shonan-it.ac.jp )

---

# 今回の授業内容

---

# 今回の授業内容

- 前回の課題解説
- 定義した処理を実行する
- ファイルを機能ごとに分けて再利用する
- 例外処理
- 課題

---

# 前回の課題解説

---

# 前回の課題解説

- 前回の課題の解答例を示します
- 解答例について質問があればご連絡ください

## 解答例

https://drive.google.com/file/d/1gSb19m8exqu6wAeoFPbeYN-YxydPTduO/view?usp=sharing

---

# 定義した処理を実行する

---

# 定義した処理を実行する

- Pythonの関数は「**`def`**」を使って定義することができる
- `def` は，definition(「定義」という意味の英単語)の省略形です
- `if` 文や `while` 文と同じようにインデントが必要です
- 処理が複数行にわたる場合は2行目移行もインデントが必要になります

（図を追加する）

---

# 関数にわたす情報・関数から戻ってくる情報

- **引数** ：関数`f()` の `()` 内にあるオブジェクトを引数と呼びます
- 引数はその関数への入力値（関数にわたす情報）です
- 「`,`」で区切ることで複数の引数を関数にわたすことができます
- 引数をわたす方法は「**位置引数**」と「**キーワード引数**」の2種類があります
- **位置引数**：引数の順番によって引数を関数にわたす
- **キーワード引数**：引数名を指定した形式でわたす

---

# 関数にわたす情報・関数から戻ってくる情報

```python
def f(x, y):
  return 2 * x + y

# 位置引数の場合
i = f(10, 20)       # f(20, 10)は結果が異なる
print(i)

# キーワード引数
j = f(x=10, y=20)   # f(y=20, x=10)でも同じ結果になる
print(j)
```

---

# 関数にわたす情報・関数から戻ってくる情報（オプション引数）

- 引数をあらかじめ指定することで関数を呼び出す時に引数を省略することができます
- こうした引数を **オプション引数** と呼びます
- オプション引数を指定していても関数を呼び出す時に引数を指定することで通常の引数と同じ処理ができます

```python
def double(x = 2):
  return x * 2

# 関数に引数をわたさないとオプション引数が使用される
i = double()
print(i)

# 関数に引数をわたすとその値が使用される
j = double(3)
print(j)
```

---

# 関数にわたす情報・関数から戻って来る情報（戻り値）

- **戻り値** ：関数が何を出力するかをい定義するものです
- `return` の後に書きます
- `return` を定義しない関数は，戻り値がないということになり「**None**」を返します
- Noneは，値が存在しないことを意味します

---

# 変数が使える範囲

- **変数** を関数のブロックないで定義するか，関数のブロック外で定義するかによって，**変数が使える範囲（スコープ）が異なります**
- **グローバル変数** ：関数のブロック外で定義される変数，プログラム内のどこからでも呼び出すことができます
- **ローカル変数** ：関数のブロック内で定義される変数，その関数内でのみ呼び出すことができます

---

# リストからオブジェクトの取り出し

- リストからオブジェクトを取り出すときは「`pop()`」メソッドを使います
- 取り出したいオブジェクトのインデックスを指定して取り出します
- 取り出したあとはリストから取り出したオブジェクトはなくなります
- インデックスを指定しない場合は最後のオブジェクトが取り出されます

### pop()の例
```python
alphabet = ['A', 'B', 'C', 'D'] # リスト作成
char_C = alphabet.pop(2) # アルファベット「C」のインデックスを指定して取り出す
print(char_C) # 中身を確認
print(alphabet) # リストの中身を確認
char_last = alphabet.pop() # インデックスを指定しない場合最後のオブジェクトを取り出す
print(char_last) # 中身を確認
print(alphabet) # リストの中身を確認
```

---

# リストの中のデータを確認する

- 「`オブジェクト in リスト`」の形でリストの中の要素が存在することを判定できます
- 「`オブジェクト not in リスト`」の形でリストの中に要素が存在しないことを判定できます

### データ確認の例
```python
Kanto = ['Tokyo', 'Kanagawa', 'Chiba', 'Saitama', 'Ibaraki', 'Tochigi', 'Gunma'] # リスト作成
if 'Gunma' in Kanto: # GunmaがKantoリスト内に存在するか判定
    print('Gunmaは関東地方です') # 処理
else: # それ以外
    print('Gunmaは関東地方ではありません') # 処理

if 'Yamanashi' not in Kanto: # YamanashiがKantoリスト内に存在しないか判定
    print('Yamanashiは関東地方ではありません') # 処理
else: # それ以外
    print('Yamanashiは関東地方です') # 処理
```

---

# 中身をあとから変更できないタプル型

- リスト型と同じくオブジェクトを複数格納することができ中の値を読み込むことができる
- リスト型との違いは，一度タプル型をつくると格納されている要素やその順番を一切変更することができない
- 「`()`」で囲むことでタプルをつくることができます

### タプル型の例
```python
() # 空のタプル型の生成
(1,2) # 複数のオブジェクトで構成されたタプル
(1,) # オブジェクトが1つの場合でもカンマをつける
1,2 # ()がなくてもタプル型になる
1, # ()がない場合でオブジェクトが1つの場合もカンマをつけることでタプル型になる
```

---

# 中身をあとから変更できないタプル型

- リスト型と同じように複数のオブジェクトを「`,`」で区切ります
- 1つの要素のときでも「`,`」をつければタプルとなります
- 「`()`」がなくても「`,`」で区切ればタプルとなります

### タプル型の例
```python
sample_tuple = (10, 20) # タプルの生成
x, y = sample_tuple # タプルの中身を展開してx, yに代入
print(x)
print(y)

sample_tuple2 = 'A', 'B', 'C' # タプルの生成
a, b, c = sample_tuple2 # タプルの中身を展開してx, yに代入
print(a)
print(b)
print(c)
```

---

# キーと値をセットで扱う辞書型

- **辞書(dict)型**も同じくオブジェクトを複数格納するためのものです
- **キー** = 変更不可能なオブジェクト（文字列，数値，タプル）
- **値（バリュー）** = オブジェクト
- オブジェクトに対応するキーを指定してバリューを取り出します
- 「`{}`」で囲んで作成します
- キーとバリューの対応は「`キー:バリュー`」と表現します
- 複数のキーとバリューを格納する場合は「`,`」で区切ります

### dict型の例
```python
{} # 空のdict型
{'tea' : 100} # キーとバリューを格納
{'tea' : 100, 'coffee' : 200} # 複数のキーとバリューを格納
```

---

# 辞書型でキーを指定する

- dict（辞書）型のバリュー（値）を参照するには「`辞書名[キー]`」で指定します
- キーを指定するとそれに対応するバリューが出力されます
- 辞書に新しいキー，バリューを追加するには「`辞書名[追加キー]=追加バリュー`」と書きます

### dict型でキーの扱いの例
```python
my_dict = {'tea' : 100, 'coffee' : 200} # dict型の作成
print(my_dict['tea']) # キーを指定して対応するバリューを表示

my_dict['milk'] = 300 # 新たにキーとバリューを追加
print(my_dict) # dict型の中身を確認
```

---

# キーと値をセットで扱う辞書型

- 辞書の中のデータを確認したい場合
- 「`期待するキー名 in 辞書名`」で存在を確認できます
- リストの場合とほぼ同じです

### セットで扱う例
```python
my_dict = {'tea' : 100, 'coffee' : 200, 'milk' : 300} # dict型の作成
'tea' in my_dict # my_dict内に'tea'があるか確認
```

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

- 「 **range(開始する値, 終了する値)** 」と指定すると，開始する値から終了する値を超えない範囲で1ずつカウントアップされます
  - 例： ``range(0, 3)`` を実行してみましょう
- ここで「開始する値」が「0」の場合は省略することができます
  - 例： ``range(0, 3)`` = ``range(3)`` 同じ結果になることを確認してみましょう

```python
print(list(range(0, 3)))
print(list(range(3)))
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

- 条件が成立している限り処理を繰り返すことを考えます
- ``while`` ループを使います

```python
while 条件式:
  ブロック
```
whileの例
```python
i = 0
while i < 10:
  print('hello')
  i += 1 # i += 1 は i = i + 1 と同じ意味です
```
最後の行の ``i += 1`` がないと無限ループになってしまうので注意をしてください

---

# 処理を繰り返す（処理の途中で抜け出す）

- 処理の途中でループを抜け出すことができます
- ``break`` 文をつかうと途中でループを抜け出すことができます
- ``if`` 文などと組み合わせて使用します

```python
fruits = ['apple', 'orange', 'banana', 'grape']
for i, fruit in enumerate(fruits):
  print(i, fruit)
  if i == 2:
    break
```


---

# 課題

---

# 課題3

- Moodleにある「SCfCL-3rd-prac.ipynb」ファイルをダウンロードしてColabにアップロードしてください
- 課題が完了したら「File」>「Download」>「Download .ipynb」で「.ipynb」形式でダウンロードしてください
- ダウンロードした **.ipynbファイル** をMoodleに提出してください
- 提出期限は **5月2日(木) 20時まで** です