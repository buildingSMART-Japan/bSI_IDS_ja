# 特性ファセット

国際金融公社**プロパティ**は、IFCのオブジェクトにデータを添付する最も一般的な方法であり、おそらく最も使用されるIDSファセットであろう。

**プロパティ**は名前 (**ベース名**IDSでは "FireRating"）に分類される。**プロパティセット**Pset_WallCommon" のように、類似の主題ごとに整理することができます。 IFC プロパティには、次のようなものがあります。**価値観**これは特定の型であり、関連性があれば単位を表す。

buildingSMARTは標準化された**プロパティセット**そして**プロパティ**のように、名前、セット、データタイプを義務付けることで、シームレスなデータ交換を支援する。 例えば、以下のようなものだ：

| ベース名 | プロパティセット | データ型 |
| -------------------- | ---------------------- | ------------------------------ |
| 熱貫流率 | Pset_WallCommon | 熱貫流率測定 |
| ファイアレイティング | Pset_WallCommon | IFCLABEL |
| 長さ | Qto_WallBaseQuantities | イフクロングスメジャー |

Users can also define custom **Properties** and **Property Sets**, which may be unique to the project or distributed using the **Property Set** templates feature of IFC. Naturally, it is encouraged to require **Properties** that are standardised by buildingSMART before inventing custom ones.

すべて標準化**プロパティセット**これらの接頭辞はカスタムプロパティでは禁止されています。

標準化**プロパティ**などのプロパティは異なるエンティティに適用される。**耐荷重**壁、柱、梁には適用できるが、家具、ダクト、ケーブルには適用できない。
This is known as the **Applicable Entity**.
When specifying **Properties** in an IDS, it is important to consider which objects they can apply to.
All sorts of objects can have **Properties** applied, not only physical objects like doors, windows, and slabs, but also non-physical objects like tasks, materials, structural profile cross sections, or labour resources.

特別な**プロパティ**として知られている。**数量**一方**プロパティ**オブジェクトに関する任意の情報を指す、**数量**とは、長さ、幅、高さ、表面積、正味体積など、物体の計算上の寸法のことである。
IFC makes a distinction between **Properties** and **Quantities**, but in IDS they are interchangeable, and you are allowed to specify **Quantities** just the same as a **Property** with this facet.
Just like **Properties**, **Quantities** are grouped into **Quantity Sets** and have a **Value**.

何を見るか**プロパティ**はbuildingSMARTによって標準化されているので、以下のリストを確認してください。
You will see a list of **Property Sets**. Clicking on a **Property Set** will bring you to its page,
which will show the **Applicable Entity** just below the page title, as well as a table of **Property Names** and expected data types for the **Values** and have an **Applicable Entity**.

- [IFC4X3_ADD2 プロパティと数量セット](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/annex-b3.html)
- [IFC4 プロパティセット](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/link/alphabeticalorder-property-sets.htm)
- [IFC4数量セット](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/link/alphabeticalorder-quantity-sets.htm)
- [IFC2X3 プロパティセット](https://standards.buildingsmart.org/IFC/RELEASE/IFC2x3/TC1/HTML/psd/psd_index.htm)

IFC2X3は、buildingSMARTの標準化されたプロパティのみを持っており、数量は持っていないことに注意してください。

ドキュメントをチェックする代わりに、IDSオーサリングソフトウェアが有効な候補をリストアップしてくれるかもしれません。**プロパティセット**.

## 対応物件タイプ

IFC には様々なタイプのプロパティがあります。 IDS では、単純なプロパティを指定できます。[単一の値](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertySingleValue.htm),[境界値](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertyBoundedValue.htm),[リスト](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertyListValue.htm),[テーブル](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertyTableValue.htm)そして[列挙](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertyEnumeratedValue.htm)一方[](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcComplexProperty.htm)そして[~~参考値](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcPropertyReferenceValue.htm)はIDSがサポートしていない。

リスト、テーブル、バウンデッド、列挙プロパティの解釈は、IDS要件によって以下のように変わる：

- IDS値が単一値の場合、少なくとも1つのIFC値が一致しなければならない。
- IDS値が制限（minExclusive,maxExclusive,minInclusive,maxInclusiveを持つ）である場合、すべてのIFC値はその範囲を尊重すべきである。

IFCのバウンデッド・バリュー・プロパティは、一端のみを制限することができるため、IDSの要件を満たすためには、それらがすべてIDSの制限範囲内になければならない。 例えば、以下のような場合である：

| IDS値 | IFC下限 | IFC上限 | 期待される結果 | 理由 |
| :-------: | :-------------: | :-------------: | :-------------: | ------------------------------------------------------------------------------------ |
| >2と≦5 | 3 | 4 | ✔️ | 下限と上限の両方が指定された範囲内にある |
| >2と≦5 |  | 4 | ❌ | 下限は、制限の最小値より下に広がる可能性がある。 |
| >2と≦5 | 3 |  | ❌ | 上限は、制限の最大値を超える可能性がある。 |
| >2と≦5 | 2 | 3 | ❌ | 下限は無効である。 |
| >2と≦5 | 3 | 5 | ✔️ | この制限は最大範囲を含むので、上限は有効である。 |
| 3 | 2 | 4 | ✔️ | 下限値と上限値は指定された値を含む |
| 2 | 2 | 4 | ✔️ | 下限は指定された値と一致する |
| 2 | 2 |  | ✔️ | 提供される唯一のバウンドは、指定された値と互換性がある |
| 2 |  | 2 | ✔️ | 提供される唯一のバウンドは、指定された値と互換性がある |
| 5 | 2 | 4 | ❌ | 下限値と上限値は指定された値を除く |
| 5 |  | 4 | ❌ | 提供された唯一のバウンドが、指定された値と互換性がない。 |
| >2と≦5 |  |  | ❌ | 下限と上限の少なくとも一方が必要 |
| 3 |  |  | ❌ | 下限と上限の少なくとも一方が必要 |
|  | 2 |  | ✔️ | 値の比較は行われず、少なくとも1つの値が提供される |

## Property data types

IDSファセットでは、**プロパティ**は、プロパティが格納される予想される形式（テキスト値、ブール値、数値など）を制限するデータ型を持つことができます。
If it is a number, the value will be unit-less, such as a count of a value and the unit dependent on the measure associated with the specified `dataType`.
Our [unit documentation](units.md) provides the list of acceptable measures and the SI unit used for their expression. For more information, consult the IFC documentation at the following links:

- [IFC4X3_ADD2のデータタイプ](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/annex-b2.html)
- [IFC4データ型](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/link/alphabeticalorder-defined-types.htm)
- [IFC2X3のデータ型](https://standards.buildingsmart.org/IFC/RELEASE/IFC2x3/TC1/HTML/alphabeticalorder_definedtype.htm)

便宜上、一般的なデータ型の短いリストをここに示す：

| データ型 | 使用シナリオ |
| ---------------- | ------------------------------------------------------------------------------------------ |
| IFCLABEL | ほとんどの単純なテキストは、人間が読むことを意図している。 |
| IFCIDENTIFIER | コンピュータによって読み取られることを意図した識別コードで、通常はコンピュータによって生成される。 |
| IFCTEXT | 人間が読むための長い説明文 |
| IFCBOOLEAN | 真か偽かの選択（「はい」「いいえ」とも呼ばれることがある |
| IFCINTEGER | 1、2、3などの任意の整数。 |
| イフクリアル | 1、2、3.14などの任意の数字 |
| イフカウントメジャー | 何かの量を数えるのに使われる整数 |
| イフクロングスメジャー | 何かの物理的な長さを測るために使われる浮動小数点数。 |
| IFCAREAMEASURE | 何かの物理的な面積を測定するために使われる浮動小数点数。 |
| 容積測定 | 何かの物理的な体積を測るのに使われる浮動小数点数。 |
| IFCDATE | 2020-01-01のように、何かが起こる、または起こった日付。 |
| IFCDURATION | 3ヶ月、1週間、4日、1時間などの期間。 |

IDS currently specifies all measure-based values based on SI units. You can see the full list of units specified for each data type in the [IDS units table](units.md).
Note that although you can use a data type to request a particular measurement (e.g. an IFCLENGTHMEASURE), you cannot use IDS to request that the length is measured with a particular unit (e.g. meters, inches, or millimetres).

プロパティは、モデル内のオブジェクトに補足情報を提供する上で非常に重要です。

buildingSMARTの標準化に従うことが推奨される。**プロパティ**可能な限り、データが高度に構造化され、予測可能な検索ができるようにする。

## パラメータ

| パラメータ | 必須 | 制限あり | 許容値 | 意味 |
| ---------------- | -------- | -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **プロパティセット** | ✔️ | ✔️ | カスタムまたはbuildingSMARTで標準化されたプロパティセット名。 標準化された名前は "Pset_"または "Qto_"で始まる必要があり、IFCドキュメントに記載されている。 | オブジェクトに指定されたプロパティが設定されている。 |
| **ベース名** | ✔️ | ✔️ | 任意のテキストプロパティ名。 buildingSMARTの標準プロパティ名は、buildingSMARTのドキュメントに記載されています。 | このプロパティは、指定されたプロパティセットの中に存在し、空でない値を持たなければならない。 |
| **データ型** | ❌ | ✔️ | 参照されるスキーマ・バージョンと互換性のある有効なデータ型。 | IDSで指定される単位は[IDS単位表](units.md)を使用しますが、プロジェクトではどの単位を使用してもよいため、プロジェクトの値は比較の前にSI単位に変換する必要があります。 ユーザー・インターフェースでは、開発者やユーザーが好む単位を表示することが許可されています。 |
| **価値** | ❌ | ✔️ | プロパティのデータ型に適した任意の値。 指定がない場合は、空でない任意の値が許可されます。 メジャー・タイプの値は、[IDS 単位テーブル](units.md) で定義されている単位に従って格納されます。 | 詳細は[DataType documentation](../ImplementersDocumentation/DataTypes.md#xml-base-types)を参照。 |
| **ウリ** | ❌ | ❌ | このリソースは、名前と定義を含み、ISO 23386に準拠することが望ましい。 | 有効なURIのソースの一つは[the bSDD](https://search.bsdd.buildingsmart.org/)である。"Fire Rating "のURIの例は、[https://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/prop/FireRating](https://identifier.buildingsmart.org/uri/buildingsmart/ifc/4.3/prop/FireRating)である。 |

## Examples

| 適用意図 | 要件 意図 | ファセットの定義 |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| 遮音等級を持つ壁材 | 実体（壁など）には音響等級が必要である。 | プロパティ Set="Pset_WallCommon", Name="AcousticRating" |
| 耐火等級「2HR」の柱体 | 実体（柱など）は、耐火等級「2HR」でなければならない。 | プロパティ Set="Pset_ColumnCommon", Name="FireRating", value="2HR" |
| 正味容積が20～100立方メートルのスラブ事業体 | 実体（スラブなど）の正味容積が20～100立方メートルであること。 | Property Set="Qto_SlabBaseQuantities", Name="NetVolume", Value="[20<=Value<=100](restrictions.md)" |
| 現場打ちまたはプレキャストコンクリートのあらゆる要素 | 実体（スラブなど）は、鋳造方法が現場打ちまたはプレキャストに設定されていなければならない。 | プロパティ Set="Pset_ConcreteElementGeneral", Name="CastingMethod", value=["INSITU", "PRECAST"]. |
| MyCompany_Concreteプロパティセットに格納されているA、B、Cから選択されたConcreteMixというカスタムプロパティを持つエンティティ | エンティティは、MyCompany_Concrete というプロパティセットに格納された、A、B、または C から選択された値を持つ ConcreteMix というカスタムプロパティを持つ必要があります。 | Property Set="MyCompany_Concrete", Name="ConcreteMix", value=["A", "B", "C"]]. |

