# word-cloud

> 日本語のREADMEはこちらです: [README.ja.md](README.ja.md)

A simple web component for generating Japanese-supported word clouds using D3.js and kuromoji.js.

- **[Live Demo](https://code4fukui.github.io/word-cloud/)**

## Features

-   **Simple Web Component:** Use the `<word-cloud>` element directly in your HTML.
-   **Japanese Morphological Analysis:** Utilizes `kuromoji.js` to accurately tokenize Japanese text and extract nouns.
-   **Multiple Data Sources:** Generates clouds from inline text, an external JSON file, or an RSS feed.
-   **Smart Filtering:** Automatically ignores common Japanese words (e.g., "の", "こと", "さん") for a cleaner result.
-   **Dynamic SVG Rendering:** Renders a colorful SVG using D3.js, with word size based on frequency rank.

## How to Use

### 1. Import the script

Add the following script tag to your HTML file.

```html
<script type="module" src="https://code4fukui.github.io/word-cloud/word-cloud.js"></script>
```

### 2. Add the component

Use the `<word-cloud>` tag and provide a data source. **Note:** The component requires a defined size (width and height) via CSS to be visible.

#### Example 1: From Inline Text

Place your text directly inside the component.

```html
<word-cloud style="display: block; width: 100%; height: 500px;">
中高生向けのサイバーセキュリティ教育プログラム「CyberSakura」でもご協力いただいている、株式会社日立ソリューションズ・クリエイトさん、RENEW視察と合わせて企業研修に来ていただきました。
</word-cloud>
```

#### Example 2: From an External JSON File

Use the `src` attribute to point to a JSON file. The file should be an array of objects, each with `title` and `body` properties.

```html
<word-cloud src="https://taisukef.github.io/create-every-day/blog_2022.json" 
            style="display: block; width: 100%; height: 500px;"></word-cloud>
```

#### Example 3: From an RSS Feed

Use the `src` attribute to point to an RSS feed (`.xml`). The component will parse the `title` and `description` from the first 100 `<item>` entries.

```html
<word-cloud src="https://fukuno.jig.jp/rss.xml" 
            style="display: block; width: 100%; height: 500px;"></word-cloud>
```

## Configuration

### Component Attributes

-   `src` (optional): The URL for an external data source. Supports `.json` and `.xml` (RSS) files. If this attribute is omitted, the component will use its inner text content.

### Text Processing

-   **Tokenization:** Text is processed with `kuromoji.js` to identify parts of speech.
-   **Filtering:** Only tokens identified as **nouns** (`名詞`) are included in the word cloud.
-   **Stop Words:** A predefined list of common words in `ignoreWords.js` (e.g., "こと", "ため", "さん") is excluded.
-   **Sizing:** Words are sized based on their frequency **rank**. The most frequent word is the largest, the second most frequent is the second largest, and so on.

## Dependencies

This component is built with and loads the following libraries:

-   [d3@7](https://cdn.skypack.dev/d3@7)
-   [d3-cloud-es](https://code4fukui.github.io/d3-cloud-es/) (ES module version of d3-cloud)
-   [kuromoji-es](https://code4fukui.github.io/kuromoji-es/) (ES module version of kuromoji.js)

## License

[MIT](https://github.com/code4fukui/word-cloud/blob/main/LICENSE)