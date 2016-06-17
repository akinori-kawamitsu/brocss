# rpd-css
One of the CSS naming rule. Based on BEM, OOCSS, and SMACSS.
__RPD-CSS__（ラピッドCSS）は、BEM、OOCSS、SMACSSをベースにしたCSSの命名規則です。  
名づけで悩まないようにするのがBROCSSの主な目的となっています。

----

#命名規則
1. 最も長い名前でも、__Role-Position-Detail__の構成で3単語に制限されます。
2. 2単語の場合は__Role-Detail__の構成となります。
3. 単語はすべて小文字の英数字とします。
4. 単語の間はハイフン1つでつなぎ、アンダースコア、キャメルケースは使いません。
5. CSSの設定にはクラス属性を用い、ID属性、!important、インラインスタイルは原則として使用禁止です。
6. JavaScriptのセレクタに使う場合、ID属性の使用はOKです。
7. 従属セレクタでは接頭辞dep-を付けます。
8. JavaScriptでクラスをセレクタに使う場合、該当するクラス名には接頭辞js-を付けます。

#分類
RPD-CSSはCSSのセレクタをBase, レイアウト・機能セレクタ（LFセレクタ）、従属セレクタに分類します。

##Base
Baseは、SMACSSのBase、HTML要素のリセットや細かい調整用のセレクタ、FLOCSSにおけるUtilityをここに入ります。
    例: .mt-10 {margin-top:10px;} など。

##レイアウト・機能セレクタ（LFセレクタ）
SMACSSに定義されているLayoutとModuleを区別するための名づけルールは設けません（接頭辞l-やm-は使いません）。  
まったく区別しないわけではなく、Moduleに当たるものは「機能セレクタ」として再定義しています（Layoutの定義は大体同じ）。一緒くたにして扱うときはLFセレクタ（Layout/Function selector）と呼ぶことにします。  
LFセレクタはRole-Position-Detailのルールに基づいて名づけを行います。レイアウトセレクタと機能セレクタではPositionの意味合いが少し異なるものになります。

###Role（役割）
レイアウトセレクタでは、header, main, sidebar, footer,　container, contents, row, col など、レイアウトをあらわす単語が入ります。  
機能セレクタでは、title, lead, btn, form, caption, menu, card, search など、何らかの機能を示す単語が入ります。  
上の例で、Layoutにcontentsがあったり、Moduleにcardがあるなど、「これ逆じゃね？」って思う人もいるでしょう。実際どちらに入れても違和感はないと思います。つまり、LayoutかModuleかを厳密に区別するのは面倒です。RPD-CSSではこの2つをまとめて扱うので悩む必要がありません。

###Position（場所、担当範囲）
Layoutに該当するセレクタの場合、そのセレクタが使われる場所を限定します。すべてのページやメディアで共通であれば、Positionを入れる必要はありません。  
    例： header-home, header-category, header-post, col-sm, col-lg など。

Moduleに該当するセレクタの場合、Role内での担当範囲という意味になります。  
    例: menu-item, caption-img, caption-text, card-title, card-excerpt など。

###Detail（詳細）
__DetailはModifierやState,Skinではありません__。装飾や変化する状態は従属セレクタが担当します。  
レイアウトや機能の詳細、補足のような情報を入れます。  
例：  
    グリッドの占有量 -> col-sm-6 など  
    モジュールの子要素など　->　contents-inner, sidebar-ad, sidemenu-item

##従属セレクタ
BEMで言うところのModifier、SMACSSで言うところのState、OOCSSで言うところのSkinの役割を担うセレクタです。  
RPD-CSSでは構造と見た目をCSSでも分離しています。  
従属セレクタは常にLFセレクタとセットでないとスタイルが定義されません。というか独立してスタイルを持ってはいけません。  
LFセレクタとは明確に判別する必要があるため、dep(depend)、js(JavaScript) の接頭辞が付きます。  
接頭辞のあとに、Role-Position-Detail と続き、そのルールはLFセレクタと同じです。

NG  
    .dep-text-red {...} //単独でスタイルがついてはいけません  
    .module .dep-text-red {...} //入れ子の衝突が発生します  
OK  
    .module.dep-text-red {...}  

従属セレクタで指定するCSSプロパティの例
* font、text関連
* 色
* 背景
* 角丸
* CSSアニメーション
* DOM制御関連

----