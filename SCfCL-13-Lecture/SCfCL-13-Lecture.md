---
marp: true
math: katex
paginate: true
---
<!-- スライドURL：https://docs.google.com/presentation/d/1dn7FdWkffU8nDj9OCnH4pROXePWNSlTzjoZVQL1Xnyo/edit?usp=sharing --->

# コンピュータリテラシ発展 〜Pythonを学ぶ〜

## 第13回：いろんな業務を自動化してみよう(2)

情報学部 情報学科 情報メディア専攻
清水 哲也 ( shimizu@info.shonan-it.ac.jp )

---

# 今回の授業内容

---

# 今回の授業内容

- 前回の課題解説
- 特定のルールに従って，フォルダ構成を整理する
- 作業フォルダにすべてのファイルをコピーする
- すべてのファイルを取得する
- 取得したファイルが請求書ファイルかどうかを判別する
- 新しいファイル名とフォルダ名を取得する
- 新しいフォルダを作成する
- ファイル名変更とフォルダ移動を行う
- 課題

---

# 前回の課題解説

---

# 前回の課題解説

- 前回の課題の解答例を示します
- 解答例について質問があればご連絡ください

## 解答例

（第12回課題の解答例を作成してURLを貼る）

---

# 特定のルールに従って，フォルダ構成を整理する

---

# 問題点と目標

## 問題点
- ファイルとフォルダの管理ルールが不適切
- 請求書のファイル名が不規則かつ，ファイルが分散している

## 目標
- 請求書は「**請求書_会社名+様+YYYY年MM月**」に統一
- お客様の会社ごとにフォルダを作成
- 請求書以外のファイルは移動操作を行わない

---

# データの準備

- これから行う分析のためにデータを準備します
- Moodleにある「**before.zip**」をダウンロードして解凍してください
- 作業場所に「**organize_data**」フォルダを作成してそこの「**before**」フォルダをアップロードしてください
- 「**organize_data**」の中に「**before**」フォルダがあり，その中に「**佐藤**」と「**田中**」フォルダがあります


---

# データの準備

Colab上のフォルダ構成は以下のようになります．

**※Colab上のファイル構造のスクショを貼り付ける**

---

# 「佐藤」フォルダの各ファイルの中身

|    佐藤/タスク管理.xlsx    |    佐藤/請求書_xxxxxxx_DEF商事様.xlsx    |
| -------------------------- | -------------------------- |
| ![h:300](./img/12-002.png) | ![h:300](./img/12-003.png) |


---

# 「田中」フォルダの各ファイルの中身
要修正

|    2024年06月_売上.xlsx    |    取引先流入元.xlsx    |
| -------------------------- | -------------------------- |
| ![h:300](./img/12-004.png) | ![h:300](./img/12-005.png) |

---

# pythonファイルの作成

- 今回はPythonファイル(.ipynb)を先程作成した「**organize_data**」ファルダ内に作成します
- ファイル名は自由に決めてください


---

# 作業用フォルダにすべてのファイルをコピーする

---

# 作業用フォルダにすべてのファイルをコピーする

- ファイル名の変更等作業時にファイル誤削除の危険があるため、まず作業用フォルダを作成します
- 作業用フォルダは「**after**」という名前で作成します
- すべてのファイルをこの作業用フォルダにコピーします
- フォルダのコピーには**shutil**モジュールの**copytree()**関数を使用
- 同じ処理を2回実行すると2回目はフォルダが既に存在するためエラーが発生します
- プログラムを何度実行してもエラーで処理が終了しないように例外処理を組み込みます

---

# 作業用フォルダにすべてのファイルをコピーする

```py
import shutil
 
org_path = '/content/drive/MyDrive/???/organize_data/' 
 
try:
  shutil.copytree(org_path + 'before', org_path + 'after')
except FileExistsError as e:
  print('すでにafterフォルダが存在します')
```

---

# 作業用フォルダにすべてのファイルをコピーする

Google Drive上に新しく「after」フォルダが生成されたスクショを貼る

---

# すべてのファイルを取得する

---

# すべてのファイルを取得する

- 「**after**」フォルダ内のすべてのファイルを取得します
- 請求書ファイルは「**佐藤**」と「**田中**」のフォルダに分かれています
- `os`モジュールの`listdir()`関数を使用するとフォルダ名のみ取得しファイル名は一度に取得できません
- 今回の場合`glob`モジュールを用いた再帰的な検索を行います

---

# すべてのファイルを取得する

取得したファイルリストを表示します

```py
import glob
 
files = glob.glob(org_path + 'after/**', recursive=True)
 
files
```

---

# 取得したファイルが請求書ファイルかどうか判別する

---

# 取得したファイルが請求書ファイルかどうか判別する

-  「請求書以外のファイルは移動しない」というルールに従いファイルが請求書かどうかを判別する処理が必要になります
-  請求書ファイルかどうかを判断するためExcelファイルのシート名に「請求書」が含まれているかを確認します
-  この確認作業には`OpenPyXL`ライブラリを利用する


---

# 拡張子が「.xlsx」かどうかの確認

- OpenPyXLを使用するにはファイルの拡張子が「**.xlsx**」である必要があります
- OpenPyXLを使用して開けるファイルかどうかを確認する処理を実施します

```py
def check_excel_file(file):
  if '.xlsx' in file:
    return True
  else:
    return False
 
for file in files:
  if check_excel_file(file):
    print('「' + file + '」はExcelです．')
  else:
    print('「' + file + '」はExcelではないです．')
```

---

# シート名が「請求書」かどうかを確認

- 請求書かどうかを判断する処理を行います
- Excelファイルのシート名を取得する`sheetnames`属性を指定します

---

# Excelファイルに集計データを出力する

- 出力先は「**sales_analysis**」フォルダに指定します
- `output_path`に出力先フォルダを設定します

---

# Excelファイルに集計データを出力する

```py
import openpyxl
 
invoice_sheet_name = '請求書'
 
def check_invoice_excel_file(wb):
  if invoice_sheet_name in wb.sheetnames:
    return True
  else:
    return False
 
for file in files:
  if check_excel_file(file):
    wb = openpyxl.load_workbook(file)
    if check_invoice_excel_file(wb):
      print('「' + file + '」は請求書です．')
    else:
      print('「' + file + '」は請求書ではないです．')
  else:
    print('「' + file + '」はExcelではないです．')

```

---

# 新しいファイル名とフォルダ名を取得する

---

# 新しいファイル名とフォルダ名を取得する

- 新しい請求書ファイル名のフォーマットは「**請求書_会社名+様_YYYY年MM月**」とします
- 「**YYYY年MM月**」は請求書の発行年月を表します
- **会社名**と**請求書発行年月**はExcelファイルの**B2セル**と**B5セル**からそれぞれ取得します

---

# 会社名を取得する

- OpenPyXLで請求書シートの**B2セル**の値を`name`と名付けてとりだします

```py
corporate_name_cell = 'B2'
 
def get_invoice_corporate_name(wb):
  name = wb[invoice_sheet_name][corporate_name_cell].value
  return name
 
for file in files:
  if check_excel_file(file):
    wb = openpyxl.load_workbook(file)
    if check_invoice_excel_file(wb):
      name = get_invoice_corporate_name(wb)
      print(name)

```

---

# 請求書の発行年月を取得する

- 請求書発行月の取得はExcelファイルのB5セルから取得します
- B5セルの値は「**日付YYYY/MM**」というフォーマットになっています
- 正規表現「`\d\d\d\d/\d\d`」を用いて「**YYYY/MM**」という必要な情報のみを「`date`」という名前で取り出します

---

# 請求書の発行年月を取得する

```py
import re
 
invoice_created_date_cell = 'B5'
 
def get_invoice_created_date(wb):
  value = wb[invoice_sheet_name][invoice_created_date_cell].value
 
  invoice_created_date_regex = re.compile(r'\d\d\d\d/\d\d')
  invoice_created_date_match = invoice_created_date_regex.search(value)
 
  date = invoice_created_date_match.group()
  return date
 
for file in files:
  if check_excel_file(file):
    wb = openpyxl.load_workbook(file)
    if check_invoice_excel_file(wb):
      date = get_invoice_created_date(wb)
      print(date)
```

---

# 請求書ファイル名をフォーマット通りの形にする

- 会社名と請求書発行月を取得した後`format()`メソッドを使用してこれらの情報を結合します
- `get_invoice_created_date()`関数で取得した日付のフォーマット（例：2020/02）を最終的なフォーマット（例：2020年02月）に変換します
- 日付フォーマットの変換には**スライス記法**を利用します

---

# 請求書ファイル名をフォーマット通りの形にする

```py
def get_new_invoice_file_name(wb):
  invoice_corporate_name = get_invoice_corporate_name(wb)
  invoice_created_date = get_invoice_created_date(wb)
 
  formatted_date='{0}年{1}月'.format(invoice_created_date[0:4],invoice_created_date[5:7])
 
  file_name='請求書_{0}様_{1}'.format(invoice_corporate_name,formatted_date)
  file_name_with_ext=file_name+'.xlsx'
  return file_name_with_ext,invoice_corporate_name
 
for file in files:
  if check_excel_file(file):
    wb = openpyxl.load_workbook(file)
    if check_invoice_excel_file(wb):
      new_file_name,new_dir_name=get_new_invoice_file_name(wb)
      print(new_file_name, new_dir_name)
```

---

# 新しいフォルダを作成する

---

# 新しいフォルダを作成する

- 会社名のフォルダ作成には`os`モジュールの`makedirs()`関数を使用します
- フォルダ作成処理は請求書ファイルの数だけ複数回実行されます
- 既に存在するフォルダで処理が失敗しないように引数`exist_ok`を`True`に設定します

---

# 新しいフォルダを作成する

```py
import os
 
def make_new_invoice_dir(invoice_corporate_name):
  dir_path = org_path + 'after/' + invoice_corporate_name
  os.makedirs(dir_path,exist_ok=True)
  return dir_path
 
for file in files:
  if check_excel_file(file):
    wb = openpyxl.load_workbook(file)
    if check_invoice_excel_file(wb):
      new_file_name,new_dir_name=get_new_invoice_file_name(wb)
      new_dir_path = make_new_invoice_dir(new_dir_name)
 
new_dir = os.listdir(org_path + 'after/')
new_dir
```

---

# ファイル名変更とフォルダ移動を行う

---

# ファイル名変更とフォルダ移動を行う

- ファイル名変更とフォルダ移動は`shutil`モジュールの`move()`関数で同時に実行できます

```py
for file in files:
  if check_excel_file(file):
    wb = openpyxl.load_workbook(file)
    if check_invoice_excel_file(wb):
      new_file_name,new_dir_name=get_new_invoice_file_name(wb)
      new_dir_path = make_new_invoice_dir(new_dir_name)
      shutil.move(file, new_dir_path+'/'+new_file_name)
```

---

# プログラムをまとめる

- Google Colabを利用している場合はまとめてもまとめまなくてもいいと思います
- 自分のパソコンでpythonファイルを作成して実行する場合は1つのファイルにまとめた方がいいです
- 一連の処理は関数にまとめると処理の内容がわかりやすいです
- （まとめたプログラムのURLを貼り付ける）


---

# 課題

---

# 課題13

- 今回の授業でやったことを提出してください
- 実行したら，「File」>「Download」>「Download .ipynb」で「.ipynb」形式でダウンロードしてください
- ダウンロードした **.ipynbファイル** をMoodleに提出してください
- 提出期限は **7月18日(木) 20時まで** です
