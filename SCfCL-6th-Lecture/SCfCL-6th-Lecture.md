---
marp: true
math: katex
paginate: true
---

# コンピュータリテラシ発展 〜Pythonを学ぶ〜

## 第6回：Excel作業を自動化しよう(2)

情報学部 情報学科 情報メディア専攻
清水 哲也 ( shimizu@info.shonan-it.ac.jp )

---

# 今回の授業内容

---

# 今回の授業内容

- 前回の課題解説
- Excelファイルを編集する
- Excelのレイアウトを編集する
- 課題

---

# 前回の課題解説

---

# 前回の課題解説

- 前回の課題の解答例を示します
- 解答例について質問があればご連絡ください

## 解答例

https://colab.research.google.com/drive/1uG8eKYq9ryLH-ght91ojIO4XK-z96mbJ?usp=sharing

---

# Excelファイルを編集する

---

# Excelファイルを新規作成する

- Excelファイル（ワークブック）を新規作成します

```python
import openpyxl as op

wb = op.Workbook()
wb.save('filename.xlsx')
```

- `workbook`の引数を空にすると新しいワークブックを読み込みます
- `save()`メソッドで保存します
- 保存作為を指定したい場合はパスを含めて指定する必要があります

---

# Excelファイルを新規作成する

- Excelファイル（ワークブック）を新規作成します（パスを含む場合）

```python
import openpyxl as op

wb = op.Workbook()
wb.save('/content/drive/MyDrive/???/filename.xlsx')
```

- `workbook`の引数を空にすると新しいワークブックを読み込みます
- `save()`メソッドで保存します
- 保存作為を指定したい場合はパスを含めて指定する必要があります

---

# 新規作成したExcelファイルの確認

（画像を入れる）

---

# Excelシートを追加/削除します

- 新しいシートを追加します

```py
Workbookオブジェクト.create_sheet()
```

- 挿入位置とシート名を指定してシートを追加します

```py
Workbookオブジェクト.create_sheet(index = 数字, title = 'シート名')
```

- Excelシートを削除します

```py
Workbookオブジェクト.remove(Worksheetオブジェクト)
```

---

# Excelシートを追加/削除します

- 新しいシートを追加します

```py
wb = op.Workbook()

wb.create_sheet()
print(wb.sheetnames)
wb.save('/content/drive/MyDrive/???/create_sheet.xlsx')
```

(画像を追加)

---

# Excelシートを追加/削除します

- 挿入位置とシート名を指定して新しいシートを追加します

```py
wb = op.Workbook()

wb.create_sheet(index = 1, title = 'NewSheet')
print(wb.sheetnames)
wb.save('/content/drive/MyDrive/???/create_sheet.xlsx')
```

(画像を追加)

---

# 課題

---

# 課題

- Moodleにある「SCfCL-6th-prac.ipynb」ファイルをダウンロードしてColabにアップロードしてください
- 課題が完了したら「File」>「Download」>「Download .ipynb」で「.ipynb」形式でダウンロードしてください
- ダウンロードした **.ipynbファイル** をMoodleに提出してください
- 提出期限は **5月30日(木) 20時まで** です
