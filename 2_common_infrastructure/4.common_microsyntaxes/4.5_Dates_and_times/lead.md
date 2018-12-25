# 2.4.5. Dates and times


- note
    - この仕様は、日付の[ISO8601]標準の共通サブセットに従って日付と時刻をエンコードします。
        - [ISO8601](https://www.w3.org/TR/html/references.html#biblio-iso8601)
    - つまり、エンコードされた日付は1582-03-01、0033-03-27、または2016-03-01のようになり、datetimeは1929-11-13T19:00Z、0325-06-03T00:21+10:30のようになる。
    - フォーマットは約YYYY-MM-DDTHH:MM:SS.DD±HH:MMですが、誕生日のような月日を表す場合や、タイムゾーン情報のない時間などを表現する場合など、いくつかの部分はオプションです。
    - 時刻は24時間制で表されており、うるう秒を表すのは誤りです。
    - 日付は、予期的年の0000年と9999年の間の先発グレゴリオ暦で表される。他の年はエンコードできない。
    - 先発グレゴリオ暦は、1950年ごろから世界中で最も一般的なカレンダーであり、1950年から9999年の間のほとんどの人、そして過去数十年または数世紀の多くの人々にとって理解されています。
    - グレゴリオ暦は、異なる時代に異なる国で公式に採択され、ユリウス暦の代わりに教皇グレゴリー13世が提出した1582年の間に、そしてそれが1949年には中国で採用されました。
    - 現在、最近の過去、または数千年後のことを扱う最も実用的な目的のために、これは問題なく動作します。
    - グレゴリオ暦が採用される以前は、例えばロシアやトルコでは1917年以前、英国またはアメリカの英国の植民地では1752年以前に、スペインまたはアメリカのスペイン植民地では1582年より前に、その他の地域でも現在の日付は当時の日付と合いません。
    - 基本的なエンコーディングとしてのグレゴリオ暦の使用は、やや恣意的な選択です。
    - 他の多くのカレンダーが使用されていたか、使用されており、関心のある読者はWeb上の情報を探す必要があります。
    - 制作者向けのフォームの日付、時刻、および数値書式のディスカッション、フォームコントロールのローカライズに関する実装ノート、および`time`要素の説明も参照してください。


- 以下のアルゴリズムでは、年月の日数とは次のようになります。これには、グレゴリオ暦のうるう年が考慮されます。
    - 1, 2, 5, 7, 8, 12月は 31日
    - 4, 6, 9, 11月は 30日
    - 年が400で割り切れるか、4で割り切れるが100では割り切れない場合、2月は 29日
        - そうではない場合28日
    - [GREGORIAN](https://www.w3.org/TR/html/references.html#biblio-gregorian)
- このセクションで定義されている日付と時刻の構文でASCII数字が使用されている場合、数値は基数10で表されます。

- note
    - ここに記述されている形式は、対応するISO8601形式のサブセットを意図していますが、この仕様では、ISO8601よりもはるかに詳細な解析規則を定義しています。
    - したがって、実装者は、以下に説明する解析ルールを実装するために使用する日付解析ライブラリを注意深く調べることをお勧めします。
    - ISO8601ライブラリは日付と時刻をまったく同じ方法で解析しないことがあります。
    - [ISO8601](https://www.w3.org/TR/html/references.html#biblio-iso8601)

- この仕様書が先発グレゴリオ暦を参照する場合、それは現代のグレゴリオ暦を意味し、外挿法によって西暦1年を推定する。
- 先発グレゴリオ暦の日付は、時に明示的に先発グレゴリオ暦の日付と呼ばれ、そのカレンダーがその時（またはその場所で）使用されていなくても記述されます。
    - [GREGORIAN](https://www.w3.org/TR/html/references.html#biblio-gregorian)