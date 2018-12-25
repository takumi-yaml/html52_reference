### 2.4.4.3. Floating-point numbers

- 文字列が有効な浮動小数点数の場合は、次のようになります

1. オプションで、U+002D HYPHEN-MINUS文字（ - ）。
2. 指定された順序で次のいずれかまたは両方
    1. 一連の1つ以上のASCII数字。
    2. 指定された順序で次の両方
        1. 単一のU+002Eフルストップ文字 `.`
        2. 一連の1つ以上のASCII数字。
3. 必要に応じて
    1. U+0065ラテン小文字E文字（E）またはU+0045ラテン文字大文字E（E）のいずれかです。
    2. オプションで、U+002D HYPHEN-MINUS文字（ - ）またはU+002B PLUS SIGN文字（+）。
    3. 一連の1つ以上のASCII数字。

- 有効な浮動小数点数は、仮数部に指数のべき乗を乗じた数を表します。ここで、仮数部は最初の数字で、10進数として解釈されます
    - 文字列全体がU+002D HYPHEN-MINUS文字（ - ）で始まり、数字がゼロでない場合には、小数点と小数点以下の数字を含む正数を負数として解釈します
- 指数部がEの後ろにある場合はその数
    - Eと数字の間にU+002D HYPHEN-MINUS文字（ - ）があり、数字がゼロでないか、またはEと（+）の間にU+002Bのプラス記号（+）を無視して、もしあれば数値
    - Eがない場合、指数はゼロとして扱われます

- note
    - 無限大および非数（NaN）値は有効な浮動小数点数ではありません。


- 浮動小数点数としてのnの最も良い表現は、ToString（n）を実行して得られた文字列です。
- 抽象操作ToStringは一意に決定されません。
- 特定の値に対してToStringから取得できる可能性のある文字列が複数ある場合、ユーザーエージェントはその値に対して常に同じ文字列を返す必要があります

- 浮動小数点数の値を解析するための規則は、次のアルゴリズムに示されているとおりです。
- このアルゴリズムは、何かを返す最初のステップで中断されなければなりません。
- このアルゴリズムは、数値またはエラーのいずれかを返します。

1. inputを解析対象の文字列とします。
2. positionをinputへのポインタとし、最初は文字列の先頭を指します。
3. valueに値1を設定します。
4. 除数に1を設定します。
5. 指数の値を1とする。
6. 空白を飛ばす
7. positionが入力の終わりを過ぎている場合は、エラーを返します。
8. positionで示された文字がU+002D HYPHEN-MINUS文字（ - ）の場合：
    1. 値と除数を-1に変更します。
    2. 次の文字に前進します。
    3. positionがinputの終わりを過ぎている場合は、エラーを返します。
    - それ以外の場合、position（最初の文字）で示された文字がU+002Bのプラス記号（+）である場合：
        1. 次の文字に前進します。 （ "+"は無視されますが、適合していません）。
        2. positionが入力の終わりを過ぎている場合は、エラーを返します。
9. positionが指している文字がU+002E FULL STOP (.)であり、inputの最後の文字ではなく、positionが指す文字がASCII数字の場合、値をゼロに設定し、分数ラベルのステップにジャンプします。
10. positionが指す文字がASCII数字ではない場合、エラーを返します
11. ASCII数字である一連の文字を収集し、結果のシーケンスを10進数の整数として解釈します。 値にその整数を掛けます。
12. positionが入力の最後を過ぎている場合、変換`conversion`とラベル付けされたステップにジャンプします。
13. fraction: positionで示された文字がU+002E FULL STOP（.）の場合、次のサブステップを実行します。
    1. 次の文字に前進します。
    2. positionが入力の最後を過ぎているか、またはpositionで示された文字がU+0065ラテン小文字E（e）またはU+0045ラテン大文字E（E） ASCII数字でない場合、 変換`conversion`とラベル付けされたステップにジャンプします。
    3. positionで示された文字がU+0065ラテン小文字E文字（E）またはU+0045 LATIN大文字E文字（E）の場合、これらのサブステップの残りの部分はスキップします。
    4. fraction loop：除数に10を掛けます。
    5. positionで指定された文字の値を、基数10桁（0..9）として解釈され、除数で除算された値をvalueに加算します。
    6. 次の文字に前進します。
    7. positionが入力の最後を過ぎている場合、変換`conversion`とラベル付けされたステップにジャンプします。
    8. positionで指定された文字がASCII数字の場合、これらのサブステップではfraction loopというラベルのステップに戻ります。
14, positionで示された文字がU+0065ラテン小文字E（e）またはU+0045ラテン大文字E（E） の場合、以下のステップを実行します
    1. 次の文字に前進します。
    2. positionが入力の最後を過ぎている場合、変換`conversion`とラベル付けされたステップにジャンプします。
    3. positionで示された文字がU+002D HYPHEN-MINUS文字 (-)の場合:
        1. 指数を-1に変更します。
        2. 次の文字に前進します。
        3. positionがinputの最後を過ぎている場合は、変換`conversion`とラベル付けされたステップにジャンプします
    - それ以外の場合、position（最初の文字）で示された文字がU+002Bのプラス記号（+）である場合：
        1. 次の文字に前進します。。
        2. positionがinputの最後を過ぎている場合は、変換`conversion`とラベル付けされたステップにジャンプします
    4. positionが指す文字がASCII数字の場合、変換`conversion`とラベル付けされたステップにジャンプします。
    5. ASCII数字である一連の文字を収集し、結果のシーケンスを10進数の整数として解釈します。 値にその整数を掛けます。
    6. 指数乗に10を掛けた値を掛けます
15. conversion: Sを-0以外の有限のIEEE 754倍精度浮動小数点値のセットとしますが、2つの特別な値が追加されます（2の1024乗と-2の1024乗）。
16. 丸め値を、値に最も近いSの番号とし、等しく近い値が2つある場合は、偶数の仮数で番号を選択します。
    - 2つの特別な値2の1024乗および-2の1024乗は、この目的のために偶数の有意性を有すると考えられる。
17. 丸め値が2の1024乗または-2の1024乗の場合は、エラーを返します。
18. 丸め値を返す

