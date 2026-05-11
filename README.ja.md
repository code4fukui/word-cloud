# word-cloud

D3.jsとkuromoji.jsを使用した、日本語対応のワードクラウドを生成するためのシンプルなWebコンポーネントです。

- **[ライブデモ](https://code4fukui.github.io/word-cloud/)**

## 機能

-   **シンプルなWebコンポーネント:** HTML内で直接`<word-cloud>`要素を使用できます。
-   **日本語の形態素解析:** `kuromoji.js`を利用して日本語テキストを正確に形態素解析（トークン化）し、名詞を抽出します。
-   **複数のデータソース:** インラインテキスト、外部JSONファイル、またはRSSフィードからワードクラウドを生成します。
-   **スマートなフィルタリング:** 「の」「こと」「さん」などの一般的な日本語の単語を自動的に除外し、より洗練された結果を出力します。
-   **動的なSVGレンダリング:** D3.jsを使用してカラフルなSVGをレンダリングし、単語のサイズは出現頻度の順位に基づいて決定されます。

## 使い方

### 1. スクリプトのインポート

HTMLファイルに以下のスクリプトタグを追加してください。

```html
<script type="module" src="https://code4fukui.github.io/word-cloud/word-cloud.js"></script>
```

### 2. コンポーネントの追加

`<word-cloud>`タグを使用し、データソースを指定します。**注意:** コンポーネントを表示するには、CSSでサイズ（幅と高さ）を定義する必要があります。

#### 例1: インラインテキストから

テキストをコンポーネント内に直接配置します。

```html
<word-cloud style="display: block; width: 100%; height: 500px;">
中高生向けのサイバーセキュリティ教育プログラム「CyberSakura」でもご協力いただいている、株式会社日立ソリューションズ・クリエイトさん、RENEW視察と合わせて企業研修に来ていただきました。
</word-cloud>
```

#### 例2: 外部JSONファイルから

`src`属性を使用してJSONファイルを指定します。ファイルは`title`と`body`プロパティを持つオブジェクトの配列である必要があります。

```html
<word-cloud src="https://taisukef.github.io/create-every-day/blog_2022.json" 
            style="display: block; width: 100%; height: 500px;"></word-cloud>
```

#### 例3: RSSフィードから

`src`属性を使用してRSSフィード（`.xml`）を指定します。コンポーネントは最初の100件の`<item>`エントリの`title`と`description`を解析します。

```html
<word-cloud src="https://fukuno.jig.jp/rss.xml" 
            style="display: block; width: 100%; height: 500px;"></word-cloud>
```

## 設定

### コンポーネント属性

-   `src` (オプション): 外部データソースのURL。`.json`および`.xml`（RSS）ファイルをサポートします。この属性を省略した場合、コンポーネントは内部のテキストコンテンツを使用します。

### テキスト処理

-   **トークン化:** テキストは`kuromoji.js`によって処理され、品詞が識別されます。
-   **フィルタリング:** **名詞**として識別されたトークンのみがワードクラウドに含まれます。
-   **ストップワード:** `ignoreWords.js`で定義された一般的な単語のリスト（例: 「こと」「ため」「さん」）は除外されます。
-   **サイズ調整:** 単語のサイズは出現頻度の**順位**に基づいて決定されます。最も頻出する単語が最大サイズ、2番目に頻出する単語が2番目に大きいサイズ、というように続きます。

## 依存関係

このコンポーネントは以下のライブラリを使用して構築されており、これらを読み込みます。

-   [d3@7](https://cdn.skypack.dev/d3@7)
-   [d3-cloud-es](https://code4fukui.github.io/d3-cloud-es/) (d3-cloudのESモジュール版)
-   [kuromoji-es](https://code4fukui.github.io/kuromoji-es/) (kuromoji.jsのESモジュール版)

## ライセンス

[MIT](https://github.com/code4fukui/word-cloud/blob/main/LICENSE)
