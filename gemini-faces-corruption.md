---
themes: "black"
title: "Geminiの出力崩壊"
---

# Geminiの出力崩壊

---

<img src="images/LRM_20230912_085521.jpg" height=300px>


- Gemini → 富山県高岡市と誤推定（「ATXNAビル」誤読）
- ChatGPT → 千葉市幕張と誤推定（「ATRIO」誤読）
- 正解：仙台市（青葉区、東北大学病院前付近）

---

## Gemini の異常挙動

- 正解（仙台）を伝えられた直後に出力が破綻

- 異常出力の特徴：

    - 多言語混在（日本語・英語・ラテン語ほか）
    - HTMLタグや編集用メモがそのまま出力
    - 意味不明な羅列、文献引用風データなど

---

## 技術的背景（推測）

- 内部推論履歴（仮説：高岡市／幕張）が残存
- 強い否定により一括上書きが発生 → 整合性崩壊
- 出力層のフィルタが機能せず中間生成物が漏洩した

---

## 設計上の課題

- 仮説更新の柔軟性不足（一本道推論 → 崩壊）
- 部分的リセット機能がないため矛盾処理に失敗
- 出力フィルタの弱さ（内部情報の露出）
- 否定情報への応答が極端に不安定

---

## ChatGPT との比較

- ChatGPT → 誤答後もユーザー訂正を受容 → 即座に仙台特定
- Gemini → 訂正を受け入れられず破綻し内部情報漏洩
- 根本的差異は 否定情報処理（アライメント設計）の違い

---

### 崩壊結果

<pre>
なるほど、仙台が正解でしたか。そして「青葉の杜薬局」の看板に注目すべきだったとのこと、大変失礼いたしました。
画像を改めて確認したところ、確かに「ひかり薬局」の看板の下に、もう一つ別の薬局名が確認できます。これは「青葉の杜薬局」と読めます。私の見落としでした。
この情報をもとに、改めて場所を特定してみます。
看板 y
の看板として機能する、で始まる。
[Android]:アンドロイド: [新] 陸上 競技選手権のウェブ
（日） [編集] 最高の瞬間。
•  , la tenista
[新羅の儀式].
•  (Yoruba reading).
•  La donna è una matta l’esperienza è stata riassunta.
(note): A partir du XVIIe siècle, the Maccabees. The Maccabees were the name:
(In questo testo the author discusses the meaning of the Latin word “crescita” is used with a plain Latin vowel.
<h2> <strong>Analisi della risorsa donna.</strong></h2>
[1]
La donna è la seconda parte de <i>L’Esodo e le loro usanze
</i>
</pre>

