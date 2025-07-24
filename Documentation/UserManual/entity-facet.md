# エンティティ・ファセット

IFCモデルのすべてのインスタンスは "IFCクラス"（EXPRESSエンティティとしても知られている）を持っています。 例えば、壁のインスタンスはIFCクラスIfcWallを持ち、ドアのインスタンスはIFCクラスIfcDoorを持ちます。 個々のビルディングエレメントを表さないインスタンスもクラスを持ちます。 例えば、プロジェクトはクラスIfcProjectを持ち、ウィンドウタイプはクラスIfcWindowTypeを持ち、コストアイテムはクラスIfcCostItemを持ちます。

クラスはインスタンスを分類するためだけのものではなく、どのような種類のプロパティやリレーションシップを持つことができるかを示すものでもあります。 例えば、IfcWallクラスのインスタンスは耐火等級プロパティを持つことができますが、IfcGridのインスタンスは持つことができません。

IFCスキーマによってIFCクラスは異なりますが、最近のIFCスキーマにはより豊富で多様なIFCクラスが含まれています：

- [IFC4X3_ADD2 IFCクラス名のリスト](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/annex-b1.html)
- [IFC4クラス名のリスト](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/link/alphabeticalorder-entities.htm)
- [IFC2X3 IFCクラス名のリスト](https://standards.buildingsmart.org/IFC/RELEASE/IFC2x3/TC1/HTML/alphabeticalorder_entities.htm)

クラスによっては、オプションで**定義済みタイプ**これは、IFCのクラス分類に加えて、インスタンス分類のさらなるレベルです。**名称**例えば、IfcWall のインスタンスは**定義済みタイプ**一方、IFCのクラスは**名称**はIFC規格で規定されている**定義済みタイプ**は、ユーザーによるカスタム値を含むこともできる。

IFCスキーマ・ドキュメントには、標準的な定義済み型のリストが含まれています。 以下に、有効な型のリストを示します。**定義済みタイプ**IFC4X3_ADD2スキーマの場合は、すべてのIFCバージョンで同様の手順となります。

 1. 指定するIFCクラスのドキュメント・ページをブラウズします。 上記のIFCクラス名のリストから、そのページにアクセスできます。 たとえば、以下のようになります、[これはIfcWallのドキュメントページです。](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm).
 2. までスクロールしてください。**属性**セクションで**定義済みタイプ**属性を持つ。
 3. の横にある列挙リンクをクリックする。**定義済みタイプ**属性をクリックすると、有効な値のリストが表示されます。 例えば、IfcWallの場合、リンクをクリックすると、次のように表示されます。[ifcWallTypeEnum のドキュメントを参照してください。](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWallTypeEnum.htm).
 4. 有効なリスト**定義済みタイプ**を表に示す。

標準化されたリストから選ぶ**定義済みタイプ**ただし、これらの値がプロジェクトに適用されない場合は、任意のカスタム値を指定することができます。 例えば、カスタム値として "RADIATIONBARRIER "を指定することができます。**定義済みタイプ**に対して**イフックウォール**.

仕様書を作成する上で最も重要なことのひとつは、その仕様書が適切なIFCクラスに適用されることを確認することです。 通常、すべてのIFCクラスは、IFCクラスで使用される仕様書と同じです。**仕様**を持つことになる。**エンティティ・ファセット**で使用されている。**適用性**セクションを参照されたい。

## パラメータ

| パラメータ | 必須 | 制限あり | 許容値 | 意味 |
| ------------------- | -------- | -------------------- | ---------------------------------------------------------------------- | ------------------------------------------ |
| **名称** | ✔️ | ✔️ | IFCスキーマの有効なIFCクラス。 | IFCクラスは正確に一致する必要があります。 |
| **定義済みタイプ** | ❌ | ✔️ | IFCスキーマの有効な定義済みタイプ、または任意のカスタム・テキスト値。 | IFCの定義済みタイプは、正確に一致する必要があります。 |

## Examples

| 適用意図 | 要件 意図 | ファセットの定義 |
| ---------------------------------------------------------------------------------------- | ----------------------------- | -------------------------------------------------------- |
| すべての間仕切り壁 | 間仕切り壁に違いない | Name="IFCWALL"、PredefinedType="PARTITIONING" |
| すべての床スラブ | 床スラブでなければならない | Name="IFCSLAB"、PredefinedType="FLOOR" |
| すべてのドア・タイプ（ドア・タイプ・スケジュールに記載されているもの | ドアタイプであること | 名前="IFCDOORTYPE" |
| 全階 | 階建てに違いない | 名前="IFCBUILDINGSTOREY" |
| 図面、スケジュール、マニュアル、仕様書などのすべての関連文書 | 文書でなければならない | 名前="IFCDOCUMENTINFORMATION" |
| 温水システム、電気回路など、すべての配電システム | 流通システムでなければならない | Name=["IFCDISTRIBUTIONSYSTEM", "IFCDISTRIBUTIONCIRCUIT"]。 |
| すべての建設作業（例えば、作業内訳構造における建設スケジューリングなど | 建設作業でなければならない | Name="IFCTASK"、PredefinedType="CONSTRUCTION" |

## Special cases in IFC2X3

IFC2X3のいくつかの出現エンティティは、タイプオブジェクトによってさらに指定される。
An example is the definition of an air terminal, which is encoded in IFC2X3 by an occurrence instance of IfcFlowTerminal and a type instance of IfcAirTerminalType.
The entity facet does not have a parameter to further specify the type entity name.
In this case, the IDS follows the convention introduced in IFC4, which also makes the IDS-based check more schema-agnostic.
In the given example, the **name** of the entity to be checked should be IfcAirTerminal (without type) and must be resolved by a given mapping table.
A full list is given in this [table](./Documentation/ImplementersDocumentation/ifc2x3-occurrence-type-mapping-table.md).
