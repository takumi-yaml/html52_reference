# 1-9 A quick introduction to HTML

- 基本的なHTML文書は次のようになります。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Sample page</title>
  </head>
  <body>
    <h1>Sample page</h1>
    <p>This is a <a href="demo.html">simple</a> sample.</p>
    <!-- this is a comment -->
  </body>
</html>
```

- HTML文書は、要素とテキストのツリーで構成されています。
- 各要素は、`<body>`などの開始タグと`</body>`などの終了タグによってソース内に表示されます。
    - 特定の開始タグと終了タグは省略され、他のタグによって暗示されることがあります。


- タグは、要素がすべて完全に互いに重なり合うことなく入れ子にされなければなりません。

```html
<!-- ❌ -->
<p>This is <em>very <strong>wrong</em>!</strong></p>

<!-- ⭕ -->
<p>This <em>is <strong>correct</strong>.</em></p>
```

- この仕様では、HTMLで使用できる一連の要素と、その要素が入れ子にされる方法に関する規則を定義しています。
- 要素には要素の仕組みを制御する属性があります。
    - 以下の例では、`<a>`要素とその`href`属性を使用して作成されたハイパーリンクがあります。

```html
<a href="demo.html">simple</a>
```

- 属性は開始タグの内側に置かれ、名前と値で構成され、`=` 文字で区切られます。
- 空白文字または`"`, `'`, ` , `=`, \`, <`, `>` のいずれかが含まれていない場合、属性値は引用符で囲まれません。
    - それ以外の場合は、一重引用符または二重引用符を使用して引用符で囲む必要があります。
- 値が空文字列の場合、値と`=`文字は完全に省略できます。

```html
<!-- empty attributes -->
<input name=address disabled>
<input name=address disabled="">

<!-- attributes with a value -->
<input name=address maxlength=200>
<input name=address maxlength='200'>
<input name=address maxlength="200">
```


- HTMLユーザエージェント（例えば、ウェブブラウザ）は、このマークアップを解析し、それをDOM（Document Object Model）ツリーに変換する。
    - DOMツリーは、ドキュメントのメモリ内表現です。
- DOMツリーには、いくつかの種類のノード、特にDocumentTypeノード、要素ノード、テキストノード、コメントノード、場合によってはProcessingInstructionノード(処理命令ノード)が含まれています。

- このセクションの上部にあるマークアップスニペットは、次のDOMツリーに変換されます。

![スクリーンショット 2018-09-18 23.29.10.png (53.6 kB)](https://img.esa.io/uploads/production/attachments/9099/2018/09/18/36903/5b5e3642-4c21-4fd1-a436-65604576916a.png)

- このツリーのdocument要素はhtml要素です。これはHTML文書のその位置に常にある要素です。
- これには、`<head>`と`<body>`の2つの要素と、それらの間のTextノードが含まれています。
- DOMツリーには、最初に期待するよりも多くのTextノードがあります
    - なぜなら、ソースには、DOM内にTextノードとして終わるいくつかのスペース（ここでは "␣"）と改行（ "⏎"）が含まれているからです。
    - しかし、歴史的な理由から、元のマークアップのスペースや改行がすべてDOMに表示されるわけではありません。
- 特に、先頭の`<head>`の開始タグの前のすべての空白は切り捨てられてしまい、`<body>`の終了タグの後ろのすべての空白は`<body>`の最後に置かれます。
- `<head>`要素にはタイトル要素が含まれ、`<title>`要素にはテキストノード「Sample page」が含まれています。同様に、`<body>`要素には`<h1>`要素、`<p>`要素、およびコメントが含まれます。

---

- このDOMツリーは、ページ内のスクリプトから操作できます。
- スクリプト（通常はJavaScript）は、`<script>`要素を使用して埋め込むか、イベントハンドラのコンテンツ属性を使用して組み込むことができる小さなプログラムです。
- たとえば、フォームの`<output>`要素の値を "Hello World"と設定するスクリプトがあるフォームは次のようになります。

```html
<form name="main">
  Result: <output name="result"></output>
  <script>
    document.forms.main.elements.result.value = 'Hello World';
  </script>
</form>
```

- DOMツリーの各要素はオブジェクトで表され、これらのオブジェクトには操作可能なAPIがあります。
例えば、リンク（例えば、ツリー上の`<a>`要素）は、その`href`属性をいくつかの方法で変更することができます。

```javascript
var a = document.links[0]; // obtain the first link in the document
a.href = 'sample.html'; // change the destination URL of the link
a.protocol = 'https'; // change just the scheme part of the URL
a.setAttribute('href', 'http://example.com/'); // change the content attribute directly
```

- DOMツリーは、HTML文書が処理（特にWebブラウザなどのインタラクティブな実装）によって処理されて表示されるときにHTML文書を表現する方法として使用されるため、この仕様は、上記のマークアップの代わりに、ほとんどがDOMツリーの観点から表現されています。

- HTMLドキュメントは、インタラクティブなコンテンツのメディアに依存しない記述を表します。
- HTML文書は、スクリーン、音声合成装置、または点字ディスプレイにレンダリングされることがあります。
- そのようなレンダリングの仕方に正確に影響を与えるために、著者はCSSなどのスタイリング言語を使用できます。

- 次の例では、CSSを使用してページが青色で黄色になりました。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Sample styled page</title>
    <style>
      body { background: navy; color: yellow; }
    </style>
  </head>
  <body>
    <h1>Sample styled page</h1>
    <p>This page is just a demo.</p>
  </body>
</html>
```

- HTMLの使用方法の詳細については、チュートリアルとガイドを参照することをお勧めします。
- この仕様に含まれているいくつかの例も使用できるかもしれませんが、初心者には、この仕様では最初は理解しにくいレベルの詳細で言語を定義しています。


## 1.9.1. Writing secure applications with HTML

- HTMLを使用して対話型サイトを作成する場合、攻撃者がサイト自体やサイトのユーザーの完全性を損なう可能性のある脆弱性を導入しないよう注意する必要があります。
- この問題に関する包括的な調査はこの文書の範囲を超えており、著者はこの問題をより詳細に研究することを強く推奨します。
- ただし、このセクションでは、HTMLアプリケーション開発の一般的な落とし穴を簡単に紹介しようとしています。

- Webのセキュリティモデルは「起源」の概念に基づいており、それに対応してWeb上の潜在的な攻撃の多くは原点を越えた​​動作を伴います。

### Not validating user input / Cross-site scripting (XSS) / SQL injection

- 信頼できない入力（例えば、テキストコメント、URLパラメータの値、サードパーティのサイトからのメッセージなど）などのユーザ生成コンテンツを受け入れる場合、データは使用前に検証され、表示される際には適切にエスケープされなければなりません。
    - それらをし損なうことで、悪意のあるユーザからの様々な攻撃を許してしまうことになります。
- フィルタを作成してユーザー入力を検証する場合、フィルタは常にセーフリストベースであり、既知の安全な構造を許可し、他のすべての入力を許可しないことが不可欠です。
- ブロックリストベースのフィルタは、既知の悪い入力を許可せず、他のすべてのものを許可することはできません。（例えば、将来的に発明される可能性があるなど）


- たとえば、ページがURLのクエリ文字列を参照して表示する内容を決定した場合、そのサイトはユーザーをそのページにリダイレクトして次のようにメッセージを表示したとします。
- メッセージがエスケープされずにユーザーに表示されただけの場合、敵対的な攻撃者はスクリプト要素を含むURLを作成できます。

```html
<ul>
  <li><a href="message.cgi?say=Hello">Say Hello</a>
  <li><a href="message.cgi?say=Welcome">Say Welcome</a>
  <li><a href="message.cgi?say=Kittens">Say Kittens</a>
</ul>
```

`http://example.com/message.cgi?say=%3Cscript%3Ealert%28%27Oh%20no%21%27%29%3C/script%3E`

- 攻撃者が被害者のユーザーにこのページを訪問することを納得させると、攻撃者が選択したスクリプトがそのページで実行されます。
- そのようなスクリプトは、サイトの作成者しか使えないような、敵対的な行動をいくつでも行うことができます
    - 例えば、ECサイトであれば、そのようなスクリプトはユーザが無意識に多くの望ましくない購入を何度も行う可能性がある。
- これは、クロスサイトスクリプティング攻撃と呼ばれます。

- サイトをトリックしてコードを実行しようとするために使用できる多くの構文があります。
- セーフリストフィルタを作成する際に、著者が検討することをお勧めします。
    - `img`要素のような無害な要素を許可する場合は、提供されている属性をも安全にリストすることが重要です。
        - すべての属性を許可した場合、たとえば、攻撃者はonload属性を使用して任意のスクリプトを実行できます。
    - URLの提供（リンクなど）を許可する場合、各URLのスキームも明示的にセーフリストされている必要があります。
        - 苦しめる可能性がある多くの制度が存在するためです。
        - 最も顕著な例は `javascript:`ですが、ユーザーエージェントは他のユーザーエージェントを実装できます（実際には歴史的に実装しています）。
    - `base`要素の挿入を許可すると、相対リンクを持つページ内の`script`要素がハイジャックされる可能性があり、同様にフォーム送信が敵対的なサイトにリダイレクトされる可能性があります。


### Cross-site request forgery (CSRF)

- ユーザーがサイト固有の副作用を伴ったフォーム送信を可能にする、例えば買い物やパスポートの提出ができるサイトでは、ユーザーが意図せずにリクエストを行ったのではなく、意図的にリクエストを行ったことを検証することが重要です。
- この問題は、HTMLフォームを他のサイトに送信できるために発生します。
- サイトは、フォームにユーザー固有の非表示のトークンを入力したり、すべての要求に対してOriginヘッダーをチェックしたりすることで、このような攻撃を防ぐことができます。


### Clickjacking

- ユーザーが実行したくないアクションを実行するためのインターフェイスをユーザーに提供するページは、ユーザーがインターフェイスをアクティブにすることを騙される可能性を避けるように設計する必要があります。
- ユーザーがそのように騙される可能性のある方法の1つは、敵対的なサイトが攻撃対象のサイトを小さなiframeに配置し、ユーザーに反応ゲームをプレイさせるなどしてユーザーにクリックを促す場合です。
    - ユーザがゲームをプレイすると、敵対的なサイトは、ユーザがクリックしようとしているようにiframeをマウスカーソルの下に素早く置くことができるので、ユーザは攻撃対象のサイトのインターフェースをクリックするようになります。
- これを避けるために、フレーム内で使用されることを予期しないサイトは、フレーム内に存在しないことを検出した場合（例えば、ウィンドウオブジェクトをトップアトリビュートの値と比較することによって）インタフェースを有効にすることが推奨される。


## Common pitfalls to avoid when using the scripting APIs

- HTML内のスクリプトには「実行完了」というセマンティクスがあります。つまり、ブラウザは一般的にスクリプトを実行してからイベントを発生させたり、文書を解析したりするなど、何かを実行する前にスクリプトを実行します。
- 一方、HTMLファイルの解析は段階的に行われます。つまり、パーサーはスクリプトを実行できるように任意の時点で一時停止できます。
- これは一般的には良いことですが、イベントが発生した可能性がある場合は、作成者がイベントハンドラにフックをかけないように注意する必要があります。


- これを確実に行うには2つの方法があります
    - イベントハンドラの`content`属性を使用するか、要素を作成して同じスクリプトでイベントハンドラを追加します。
    - 後者は安全です。前述のように、スクリプトが完了してからイベントが発生する可能性があるからです。

- これが明らかにする1つの方法は、img要素とloadイベントです。
    - 要素が解析されるとすぐに、イベントが発生する可能性があります（特に、イメージがすでにキャッシュされている場合）。

```html
<img src="games.png" alt="Games" onload="gamesLogoHasLoaded(event)">
```

- 要素がスクリプトで追加されている場合、イベントハンドラが同じスクリプトに追加されている限り、イベントは見逃されません。

```html
<script>
var img = new Image();
img.src = 'games.png';
img.alt = 'Games';
img.onload = gamesLogoHasLoaded;
// img.addEventListener('load', gamesLogoHasLoaded, false); // would work also
</script>
```

- しかし、作成者が最初に`img`要素を作成し、別のスクリプトでイベントリスナーを追加した場合、ロードイベントが間に発生し、先行のイベントが発生しない可能性があります。

```html
<!-- Do not use this style, it has a race condition! -->
<img id="games" src="games.png" alt="Games">
<!-- the 'load' event might fire here while the parser is taking a
    break, in which case you will not see it! -->
<script>
var img = document.getElementById('games');
img.onload = gamesLogoHasLoaded; // might never fire!
</script>
```

###  How to catch mistakes when writing HTML: validators and conformance checkers

- 著者はよくある間違いを捉えるために適合性チェッカー（バリデーターとも呼ばれます）を使用することを推奨します。 W3Cは、Nu Markup Validation Serviceを含む多くのオンライン検証サービスを提供しています。
