# Attribute Modules for CSS仕様

Attribute Modules (AM)はHTML要素を装飾するためにクラスではなく**属性**を使うテクニックです。

## コンセプト

他のCSS設計規約と同様に、AMはあなたのCSSを論理的に分類して記述するために、いくつかの規約を提供します。それは、モジュールとバリエーションとトレイトです。

### モジュール

モジュールは、BEMにおけるブロックとエレメントに似ており、HTMLのクラスを使った書き方を一番最初に直接置き換えることができます。モジュールは、HTMLの**属性**によって記述されます。

### バリエーション

BEMのモディファイヤーに似ていますが、バリエーションは属性の**値**によって表現されます。バリエーションは、モジュールのスタイルを上書きしたり拡張します。

### トレイト

1つの責務を持った**値**のコレクションであり、**属性**による名前空間で隔離(grouped into)されます。例えば、タイポグラフィのためのスタイルのコレクションは `type` トレイトに分類されます。これはSuitCSSの[utils](https://github.com/suitcss/utils)に似ています。

## HTMLでの書き方

### 接頭句

組み込みのHTML属性と区別するために、全てのAM属性には接頭句を付けなければいけません。この文書では、接頭句には `am-` が使われますが、短い文字列であればなんでも良いでしょう。もし接頭句が`data-`から始まるようにすれば、全てのAM属性はvalidなHTML属性になるでしょう。AMのHTMLマークアップの例は以下です。

```html
<tag am-traitName="one two mobile:three">
<tag am-BlockName>
<tag am-BlockName-ChildElement>
<tag am-BlockName="variant">
```

### 属性

属性による書き方はSuitやBEMに似たコンセプトに従って記述されます。トレイト名にはローワーキャメルを使い、モジュール名にはアッパーキャメルを使い、モジュールの親子関係を表現するのにハイフン(-)で区切ります。

Note: HTMLの属性名には大文字小文字の区別は無いので、大文字の利用は純粋にHTMLマークアップの可読性を高めるためのものです。

### 値

値は、クラスの値と同様にスペースで区切られます。クラスの場合と少し違うのは、AMで利用する値の場合は、利用できる文字列がより多いことです。これはAMがもたらす柔軟性のひとつです。簡単に何か実験できます。

## CSSでの書き方

属性と値の一対には、スペースで区切られた属性セレクタである`~=`を使います。これは、クラスのセレクタを使うのと全く同じ振る舞いをします。それぞれの属性は、その属性自身の *名前空間* により効果的に宣言できます。これはあなたがCSSスタイルを分類するのに優れた柔軟性と独立性を与えてくれます。以下がCSSでのAMの書き方の例になります。

```css
[am-traitName~="value"] { /* styles */ }
[am-traitName~="two"] { /* styles */ }
[am-traitName~="three"], .breakpoint-mobile [am-traitName~="breakpoint:three"] { /* styles */ }

[am-BlockName] {
  /* Block Styles */
}
[am-BlockName~="modifier"] {
  /* Variant Styles */
}

[am-BlockName-ChildElement] {
  /* Child Block Styles */
}
```

スタイルの記述のために土台となる属性セレクタを使う際の注意: そこで宣言したスタイルはその属性を含む全ての要素で共有されることに注意して下さい。バリエーションは土台となるモジュール無しに存在できないので、これはモジュールとバリエーションの標準的な振る舞いです。トレイトの場合は対照的に、ベースとなる属性のスタイルに宣言を加えるわけではなく、他のと混ぜたり協調できる個別のスタイルのシリーズを提供します。