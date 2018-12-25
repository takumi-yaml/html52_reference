# 3.2.8. WAI-ARIA and HTML Accessibility API Mappings

## 3.2.8.1.ARIAのオーサリング要件

- 制作者は、HTMLのARIAで規定されている要件と矛盾する場合を除き、ARIAの仕様に記述されている要件に従って、HTML要素にARIAのroleとaria- *属性を使用することができます。
    - [html-aria](https://www.w3.org/TR/html/references.html#biblio-html-aria)
- これらの例外は、制作者にドキュメントの実際の状態を表さない無意味な状態を支援技術製品が報告させないようにするためのものです。

***
### note
- ほとんどの場合、デフォルトの暗黙のARIAセマンティクスに一致するARIA roleおよび/またはaria-*属性を設定することは不要であり、これらのプロパティはブラウザによってすでに設定されているため推奨されません。
***

***
### note
- 制作者は、HTMLでARIAを使用するためのガイダンスのために、以下のドキュメントを使用することをお勧めします。
    - Using ARIA
        - アクセシブルなリッチインターネットアプリケーション仕様を使用してHTML要素にアクセシビリティ情報を追加する方法に関する開発者向けの実践ガイド
        - [wai-aria-1.1](https://www.w3.org/TR/html/references.html#biblio-wai-aria-11)
    - WAI-ARIA Authoring Practices 1.1
        - アクセシブルなリッチインターネットアプリケーションを理解し実装するための作成者ガイド。
***

## 3.2.8.2 コンフォーマンスチェッカの実装要件
- 適合性チェッカーは、ARIAの役割とHTML要素のaria-*属性を使用するために、HTMLのARIAで定義されているように、文書の適合要件を実装する必要があります。
    - [html-aria](https://www.w3.org/TR/html/references.html#biblio-html-aria)

