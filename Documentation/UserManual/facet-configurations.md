# ファセットの妥当性

この作業文書では、さまざまなファセットとその構成について、可能な構成と意図を定義する。

## エンティティ

IDSウォール - SubType マルコ
IDS Wall - SubType USERDEFINED

壁 - パラペット
WALL - USERDEFINED -> Claudio's Type
WALL - USERDEFINED -> Marco's Type

名前は必須である。

| 入力フィールド | 必須 | オプション | 禁止 | 適用性 |
| ---------------- | -------- | -------- | ---------- | ------------- |
| 名前 | ✅ | ❌ | ❌ | ✅ |
| 名前 / [サブタイプ］ | ✅ | ❌ | ❌ | ✅ |

Optional Entity requirements have no meaning? An Applicable Element is a IFCDOOR or it is not.

実体は常に肯定的な言葉で表現する。
Disallowed IFC types can be expressed prohibiting their applicability.

SUBTYPEの値を識別するためのロジックは、値の列挙を返すことである：

1. 型がIfcRelDefinesByType関係で定義されている場合
  the PredefinedType of the type overrides the entity's PredefinedType (which should be empty according to IFC documentation)
  1.1 if Type's PredefinedType is .USERDEFINED.
    -> IfcElementType.ElementType
    -> .USERDEFINED.
  1.2 else Type's PredefinedType (if not null)
    -> Type's - PredefinedType
2. 直接属性PredefinedTypeの値。
  2.1 if the attribute PredefinedType == .USERDEFINED. then the value of the attribute IfcElement/ObjectType is used
  2.2 else entity's PredefinedType (if not null)
3. TODO ElementTypeとProcessTypeについても同様のドキュメントを作成する。

TODO: IFCのバリデーション・サービスにより、typeの型が指定されているときにエンティティ・レベルの型が定義できないかどうかを確認する。

-> ユーザー定義
-> whatever the value is in the ifc

必須

Name: エンティティ名は制約と一致しなければならない（列挙/正規表現を含む）。
Name and PREDEFINEDTYPE:
  IDS: IFCWALL/.USERDEFINED. -> IFC Wall with PREDEFINEDTYPE = .userdefined. -> Pass
  IDS: IFCWALL/.USERDEFINED. -> IFC Wall with PREDEFINEDTYPE = .userdefined. with ObjectType = "FOO" -> Pass
  IDS: IFCWALL/FOO -> IFC Wall with PREDEFINEDTYPE = .userdefined. with ObjectType = "FOO" -> Pass

適用範囲

両方が制約（列挙/正規表現を含む）と一致しなければならない。

## 属性

名前は必須である。

| 入力フィールド | 必須 | オプション | 禁止 | 適用性 |
| -------------- | -------- | -------- | ---------- | ------------- |
| 名前 | ✅ | ❌ | ✅ | ✅ |
| 名前 / [値］ | ✅ | ✅ | ✅ | ✅ |

### Attribute facet interpretation

必須

NAME： Attributeは入力されるべきである（すなわち、NULLではない）（これは、NULLを受け付けるPropertyファセットとは異なる）。
NAME/VALUE: all matching attributes must match the value constraints (excludes null)

禁止

- NAME: 属性は入力されるべきではありません。
- NAME / [VALUE]: すべての一致する属性は、値の制約と一致しない（NULLは有効！）。
  - 名前 = レッド IFC: NULL -> パス
  - 名前 = レッド IFC: グリーン -> パス
  - 名前 = 赤 IFC: 赤 -> 失敗

オプション

NAME / [VALUE]: 属性値はNULLか、制約にマッチする。

適用範囲

- NAME: 属性が NULL ではない任意のエンティティ
- NAME/VALUE：属性制約と値制約を満たすエンティティ（NULLは評価されない）

## プロパティ

PSETとNAMEは必須。

| 入力フィールド | 必須 | オプション | 禁止 | 適用性 |
| ---------------------------------- | -------- | -------- | ---------- | ------------- |
| PSET / 氏名 | ✅ | ❌ | ✅ | ✅ |
| pset / name / [datatype］ | ✅ | ✅ | ❌ | ✅ |
| pset / 名前 / [データ型] / [値］ | ✅ | ✅ | ❌ | ✅ |
| セット / 名前 / [値］ | ❌ | ❌ | ❌ | ❌ |

⚠️TODO: should we discuss the case of multiple PSET / NAME matches that is possible with patterns?

その根拠についての評価は、以下を参照のこと。[議事録](https://github.com/buildingSMART/IDS/issues/206#issuecomment-1820696088).

⚠️TODO: IFCLABEL($)は有効なIFCですか？

### プロパティのファセット解釈

必須

- IDSはPSET/PNAMEを持つ：pset/pnameが存在しなければならない（nullはパスとして受け入れられ、どのようなデータ型の値でも受け入れられる）。可能な限り、dataTypeを指定することが推奨される。
- IDS HAS PSET/PNAME/DATATYPE: pset pnameが存在しなければならない。 IFC値は必要なIDSデータ型でなければならない（バリデーションで空の値をチェックする）。
- IDS HAS PSET/PNAME/DATATYPE/VALUE：前述と同様、プラス：IFCの値はIDSの制限に準拠する必要がある。

オプション

IDSは：PSET/PNAME：これは役に立たない→ツールで禁止されている
IDS HAS PSET/PNAME/DATATYPE: We might not have the property at all -> pass. If we have the property: the value has got to be non null and of correct data type
IDS HAS PSET/PNAME/DATATYPE/VALUE: We might not have the property at all -> pass. If we have the property: the value has got to be non null and of correct data type. The IFC value must comply with the IDS VALUE restriction

禁止

IDS has: PSET/PNAME: 値に関係なく、IFCファイルにpset/pnameの組み合わせを持つことはできません。
IDS HAS PSET/PNAME/DATATYPE: This does not sound like a valid use case -> Prohibited by the tool
IDS HAS PSET/PNAME/DATATYPE/VALUE: This does not sound like a valid use case -> Prohibited by the tool (there are ways to limit the values accepted in the positive by the REQUIRED/OPTIONAL branches)

適用範囲

IDS has: PSET/PNAME : pset/pnameが存在する(nullはパスとして受け入れられ、任意のデータ型の任意の値が受け入れられる)
IDS HAS PSET/PNAME/DATATYPE: A pset pname exists. The IFC value type has to match the required IDS datatype (null values fail)
IDS HAS PSET/PNAME/DATATYPE/VALUE: Like the previous, PLUS: the IFC value needs to comply with the IDS restriction

## 分類

SYSTEMが必須となるように仕様を変更したい（スキーマの変更！！）。

| 入力フィールド | 必須 | オプション | 禁止 | 適用性 | 備考 |
| ---------------- | -------- | -------- | ---------- | ------------- | ---------------------------------------------------- |
|  | ❌ | ❌ | ❌ | ❌ | スキーマで禁止されている、空文字列を除外する監査 |
| 価値 | ❌ | ❌ | ❌ | ❌ | スキーマで禁止されている、空文字列を除外する監査 |
| システム | ✅ | ❌ | ✅ | ✅ |  |
| SYSTEM / [VALUE] | ✅ | ✅ | ✅ | ✅ |  |

Optional = If the applicable element has classifications at least one should match the value/system.

必須

- システム：任意のIFC値→パス
  - エンティティ -> テストされるエンティティの少なくとも1つの分類がシステムと一致し、その値がNULLであってはならない。
- システム/値
  - SYSTEM AND VALUE一致：ifcファイルに少なくとも1つの分類項目があり、システムとバリューの両方に一致する。
    entity -> at least one classifications for the entity being tested must match system and value

オプション

- SYSTEM：これは絶対に失敗しない。失敗しない要件を持つべきでは決してないので、その解決策は、代わりに広範な包括的値を提供することである（例：正規表現）。
- システム/値：
  - エンティティ -> テストされるエンティティに分類システムが存在する場合、その値は一致しなければならない。
    - 藤堂：ヌルでも構わない

禁止

- SYSTEM：エンティティの仕様がシステムと一致することはない
- システム/値
  - UNICLASS/EF_25_10: UNICLASS/EF_25_10 -> 失敗
  - UNICLASS/EF_25_10：OMNICLASS/EF_25_10→合格
  - UNICLASS/EF_25_10：UNICLASS/EF_25_30_25→合格
  - UNICLASS/EF_25_10：OMNICLASS/EF_25_30_25→合格

適用範囲

- システム：任意のIFC値→パス
  - エンティティ -> テストされるエンティティの少なくとも1つの分類がシステムと一致し、その値がNULLであってはならない。
- システム/値
  - SYSTEM AND VALUE一致：ifcファイルに少なくとも1つの分類項目があり、システムとバリューの両方に一致する。
    entity -> at least one classifications for the entity being tested must match system and value

## 素材

- 要求事項の中で、禁止/任意を有効にするために複数の材料を許可しなければならない（すでに可能）。
- 適用性において、ANDで複数の素材を持つ要素をターゲットにするために、複数の素材を許可する必要があります（すでに可能です）。

| 入力フィールド | 必須 | オプション | 禁止 | 適用性 |
| -------------- | -------- | -------- | ---------- | ------------- |
|  | ✅ | ❌ | ✅ | ✅ |
| 価値 | ✅ | ✅ | ✅ | ✅ |

Optional is intended to help provide a closed list of values (useful for bim authors).

オプション = 該当する要素に材料がある場合、少なくとも1つは値と一致する必要があります。

必須

- 値がない：NULLでなく、任意の値の素材関連が少なくとも1つ見つからなければならない
- value：IDSの値制約に一致する、少なくとも1つの材料関連が見つからなければならない（NULLは許されない）
  - バリューは、ある要素に関連するさまざまな形の素材定義の名前をすべて調べます：
    e.g. MaterialLayerSet -> Name + all the associated material names

オプション

- 値なし：絶対に失敗しないので、IDSでは許可されない（監査ツールはエラーとしてフラグを立てる）
- 値: 材料が存在する場合、少なくとも1つの材料が値の制約に一致する必要があります。

禁止

- 値なし：エンティティに関連付けられる材料がない。
- 値: 値に一致する材料はない（材料はnull値を持つことができる）
  - IDS：木材、IFC素材なし→合格
  - IDS: Wood, IFC = null name -> パス
  - IDS：ウッド、IFCストーン→パス
  - IDS：ウッド、IFCウッド→失敗

適用範囲

- 値なし：NULLではなく、任意の値の重要な関連付けが少なくとも1つ、エンティ ティに見つかった。
- 値：IDSの値制約に一致する材料関連が少なくとも1つ見つかった（ヌルを除く）
  - バリューは、ある要素に関連するさまざまな形の素材定義の名前をすべて調べます：
    e.g. MaterialLayerSet -> Name + all the associated material names

### 実施

⚠️TODO: マテリアルの評価を目的としたIfcRelDecompositionのトラバースは1.0では実装されないことをドキュメントで明示します。

IfcRelDecompositionと材料の伝播に関して、どのような振る舞いをするのかを定義する必要がある。
The relevant conversation issue is [#198](https://github.com/buildingSMART/IDS/issues/198)

## パート

リレーションはリストになるべきでしょうか？ いいえ！1つの値を持つ属性のままにしておきましょう。なぜなら、タイプによってフィルタリング（例えばセンサー／ドア）を区別できるからです。
We encourage a smart use of type filtering to avoid false positives and negatives (⚠️TODO: document this meaningfully)

| 入力フィールド | 必須 | オプション | 禁止 | 適用性 |
| ------------------- | -------- | -------- | ---------- | ------------- |
| エンティティ | ✅ | ❌ | ✅ | ✅ |
| エンティティ／［関係］ | ✅ | ❌ | ✅ | ✅ |

REQUIRED:

- エンティティ：必要とされるエンティティのタイプとの関係が必要（有効な関係をすべてたどる）
- Entity/Relation: 必要なエンティティのタイプに対するリレーションが必要（定義されたリレーションタイプのみをトラバースする）

オプション：

- IDS Entity: IfcWall: 要素に一致する関係がある場合、ターゲットはEntityに一致する必要がある。
  - IFC ENtityはリレーションを持ち、それは壁でなければならない（ただし、リレーションは任意）。
  - IFCのスラブ開口部→失敗（エンティティが壁にぶつかることとは無関係）
  - 壁のIFC開口部→パス

禁止されている：

- エンティティ：必要なエンティティのタイプに必要な関係は存在できない（有効な関係をすべてたどる）
- エンティティ/リレーション：必要なエンティティのタイプにリレーションが存在できない（定義されたリレーションタイプのみをトラバースする）。

適用：

- Entity: 必要なエンティティのタイプに関係が存在する（有効な関係をすべてたどる）
- エンティティ/リレーション：必要なエンティティのタイプにリレーションが存在する（定義されたリレーションタイプのみをトラバースする）

## 質問

### 制限クローン

自分たちで紡ぐ`xs:restriction`代替案として、ベースタイプと埋め込み xml エンティティに関するいくつかの問題を取り除くことができる。

値に対する制限の特別なケースは、次のようないくつかのシナリオを明示的に許可／不許可にする機会を与えてくれる。

- ゼロ
  - ヌルでなければならない
  - NULLは不可
  - NULLは可能な値の1つとして受け入れられる。
- 該当なし？
- 利用できないとして該当なし？

このような論理的なケースをインチェックで明示的に処理することで、おそらくシナリオはよりわかりやすくなる。

しかし、これは適用可能なケースと要求されるケースの両方について慎重に評価する必要がある。
