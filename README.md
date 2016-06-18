# RPD-CSSNaming
One of the CSS naming rule. Based on BEM, OOCSS, and SMACSS.

# 概要
__RPD-CSSNaming__（ラピッドCSSネーミング）は、BEM、OOCSS、SMACSSをベースにしたCSSの命名規則です。  

名づけは、
1. ウェブページの構成要素を役割ごとにモジュール化
1. そのモジュールの「役割」「使用範囲」「詳細」の順で単語を選択
の2つに気を付けて行います。

モジュールは主に  
1. Base
1. レイアウト・機能（LF:Layout and Function）
1. 従属
の3種に大別されます。  
これらのクラス名づけを「役割」「使用範囲」「詳細」とします。

これにより
* 悩む時間を減らす
* 概念を理解する時間を減らす
* HTML,CSSのどちらでも修正しやすくする
* CSSのファイルサイズを減らす
* コードの可読性を上げる
ことが可能になると考えています。

----

#詳細

##モジュールの分類

モジュールを抽出するとき、一般的には全体を見て、ブロックに分けて、さらにその中でモジュールを、というように大から小へと分解していきます。しかしこの方法だと小さいモジュールの名称が親モジュールの名前の影響を受け、冗長になる可能性があります。  
モジュールの名称は最小単位のグループから行っていくようにしましょう。

RPD-CSSはCSSのモジュールをBase, LF(Layout/Function)モジュール、従属モジュールに分類します。

###Base
Baseは、SMACSSのBase、HTML要素のリセットや細かい調整用のモジュール、FLOCSSにおけるUtilityをここに入ります。
    例: .mt-10 {margin-top:10px;} など。

###レイアウト・機能モジュール（LFモジュール）
SMACSSに定義されているLayoutとModuleを区別するための名づけルールは設けません（接頭辞l-やm-は使いません）。  
まったく区別しないわけではなく、Moduleに当たるものは「機能モジュール」として再定義しています（Layoutの定義は大体同じ）。一緒くたにして扱うときはLF（Layout/Function）モジュールと呼ぶことにします。  

###従属モジュール
BEMで言うところのModifier、SMACSSで言うところのState、OOCSSで言うところのSkinの役割を担うモジュールです。  
RPD-CSSでは構造と見た目をCSSでも分離しています。  
従属モジュールは常にLFモジュールとセットでないとスタイルが定義されません。というか独立してスタイルを持ってはいけません。  

NG  
    .dep-text-red {...} //単独でスタイルがついてはいけません  
    .module .dep-text-red {...} //入れ子の衝突が発生します  
OK  
    .module.dep-text-red {...}  


LFモジュールとは明確に判別する必要があるため、dep(depend)、js(JavaScript) の接頭辞が付きます。  

接頭辞のあとの命名ルールは他のLFモジュールと同じです。

従属モジュールで指定するCSSプロパティの例
* font、text関連
* 色
* 背景
* 角丸
* CSSアニメーション
* DOM制御関連




##名称の決定方法

個々の名称は、以下のルールで決定します。

1. 最も長い名前でも、__Role-Position-Detail__の構成で3単語に制限されます。
2. 2単語の場合は__Role-Detail__の構成となります。
3. 単語はすべて小文字の英数字とします。
4. 単語の間はハイフン1つでつなぎ、アンダースコア、キャメルケースは使いません。
5. CSSの設定にはクラス属性を用い、ID属性、!important、インラインスタイルは原則として使用禁止です。
6. JavaScriptのセレクタに使う場合、ID属性の使用はOKです。
7. 従属では接頭辞dep-を付けます。
8. 従属のうち、JavaScriptで扱うクラス名には接頭辞js-を付けます。



####Role（役割）
レイアウトでは、header, main, sidebar, footer,　container, contents, row, col など、レイアウトをあらわす単語が入ります。  
機能では、title, lead, btn, form, caption, menu, card, search など、何らかの機能を示す単語が入ります。  
上の例で、Layoutにcontentsがあったり、Moduleにcardがあるなど、「これ逆じゃね？」って思う人もいるでしょう。実際どちらに入れても違和感はないと思います。つまり、LayoutかModuleかを厳密に区別するのは面倒です。RPD-CSSではこの2つをまとめて扱うので悩む必要がありません。

####Position（場所、担当範囲）
レイアウトと機能ではPositionの意味合いが少し異なるものになります。

Layoutに該当するの場合、そのが使われる場所を限定します。すべてのページやメディアで共通であれば、Positionを入れる必要はありません。  
    例： header-home, header-category, header-post, col-sm, col-lg など。

Moduleに該当するの場合、Role内での担当範囲という意味になります。  
    例: menu-item, caption-img, caption-text, card-title, card-excerpt など。

####Detail（詳細）
__DetailはModifierやState,Skinではありません__。装飾や変化する状態は従属が担当します。  
レイアウトや機能の詳細、補足のような情報を入れます。  
例：  
    グリッドの占有量 -> col-sm-6 など  
    モジュールの子要素など　->　contents-inner, sidebar-ad, sidemenu-item



----