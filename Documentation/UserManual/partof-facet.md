# パートオブファセット
このファセットは、一部のオブジェクトを識別するか（適用性）、あるいは、一部のオブジェクトを要求する（要件）。

IFC のオブジェクトは、他のオブジェクトに対して複数の関係を持つことができます。IDS part-of は、以下の型を再帰的にナビゲートして、あるエンティティが他のエンティティの part-of であるかどうかを判断します：

- リレーションシップは **IFCRELAGGREGATES**リレーションシップは、複数の小さなサブオブジェクトをひとつの大きなオブジェクトに集約する方法を説明する。例えば、多くの建物の階は建物を構成する。あるいは、多くの梁、床板、ジョイントがスラブを構成する。あるいは、多くのブラケット、マリオン、鋼板がアセンブリを構成する。
- リレーションシップとは **IFCRELASSIGNSTOGROUP**関係は、複数のオブジェクトをどのようなユースケースでオブジェクトの集合体にグループ化できるかを記述する。例えば、ダクト、AHU、ファン、ルーバーはすべて1つの配電システムにグループ化できる。あるいは、ケーブル、分電盤、GPOを1つの回路にグループ化することもできる。あるいは、スペースはゾーンにグループ化され、保守可能な資産はインベントリーにグループ化される。
- リレーションシップは **IFCRELCONTAINEDINSPATIALSTRUCTURE**リレーションシップは、複数のオブジェクトが特定の場所にどのように配置されるかを記述する。例えば、ポンプはスペースに、柱はレベル 2 の建物の階上に、またはいくつかのストリートファニチャーは建物の敷地内にあるかもしれない。すべてのオブジェクトは、IFC に単一のプライマリ・ロケーション・コンテナを持たなければならない。たとえ、（複数階の柱など）複数の場所で参照される可能性があってもである。この関係は、プライマリ・ロケーション・コンテナのみを対象とする。
- この関係は **IFCRELNESTS**関係は、物理的なオブジェクトが、より大きなホストオブジェクトに、通常、あらかじめ開けられた穴や接続端子のような物理的な接続を介して、どのように接続されるかを記述する。ホストが移動すると、接続されたネストされたオブジェクトも一緒に移動する。
- この **IFCRELVOIDSELEMENT**関係は、空白が要素にどのように属するかを記述する。
- この **IFCRELFILLSELEMENT**の関係は、要素がどのように空隙を埋め、空隙の一部になるかを説明する。

`relation` パラメータが指定されていない場合、6つすべてを(再帰的に)考慮し、包含実体を特定する。そうでない場合は、指定された関係タイプだけを(再帰的に)考慮する。

![Example of part of identification](Graphics/partof-Relations.png)

## パラメータ
| Parameter    | Required | Type            | Meaning                                                                                                                                                                                                                                                                                     |
| ------------ | -------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Entity**   | ✔️     | An entity facet | Any valid IDS `entityType`, nested in the XML (e.g. "IFCSYSTEM"). The IFC class of the larger object matches the required entity. Expressed in UPPERCASE.                                                                                                                                   |
| **Relation** | ❌       | string          | One relationship chosen from the 6 supported types listed above. If omitted any valid IFC relationship structure that directly or indirectly, and transitively (recursively) has to be evaluated, if specified only the given type must be evaluated (recursively). Expressed in UPPERCASE. |
                                                                                                                                                                                                       

## 一部の'ファセット解釈
### 適用性
| <nobr>PartOf</nobr>エンティティ | PartOf<nobr>関係*。</nobr> | IDSの<nobr>解釈</nobr>         |
| ------------- | --------------------------------- | ----------------------------------------------------- |
| IFCSPACE | -　　　　　　 | の一部であるすべてのオブジェクトに適用される。 *IfcSpace*. |
| IFCSPACE | IFCRELCONTAINEDINSPATIALSTRUCTURE | に含まれるすべてのオブジェクトに適用される。 *IfcSpace*に含まれるすべてのオブジェクトに適用される。 *IfcRelContainedInSpatialStructure*関係で定義されている |

### 必要条件
| IDS<nobr>カーディナリティ</nobr> | <nobr>PartOf</nobr>エンティティ | PartOf<nobr>関係*。</nobr> | <nobr>コンフィギュレーションを</nobr>許可しますか？ | IDSの<nobr>解釈</nobr>         |
| --------------- | ------------- | --------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------- |
| 必須　　　　　 | IFCSPACE | -　　　　　　 | ✅　　　　　　 | 該当するオブジェクトは *IfcSpace*エンティティとの関係を持っていなければならない（有効なすべての関係を走査する）。 |
| 必須 | IFCSPACE | IFCRELCONTAINEDINSPATIALSTRUCTURE | ✅ | 該当するオブジェクトは *IfcRelContainedInSpatialStructure*オブジェクトと *IfcSpace*エンティティでなければならない。 |
| オプション | IFCSPACE | - | ❌ | 許されない。一部の部品になるかどうかを指定することに付加価値はない。 |
| オプション | IFCSPACE | IFCRELCONTAINEDINSPATIALSTRUCTURE | ❌ | 許されない。一部の部品になるかどうかを指定することに付加価値はない。 |
| 禁止 | IFCSPACE | - | ✅ | 該当するオブジェクトは *IfcSpace*に関連付けられてはならない。 |
| 禁止 | IFCSPACE | IFCRELCONTAINEDINSPATIALSTRUCTURE | ✅ | 該当するオブジェクトは *IfcRelContainedInSpatialStructure*との関係 *IfcSpace*に関連付けられてはならない。 |

\* フィールドは XML 属性です。


## 例
| <nobr>適用</nobr>意図          | <nobr>要件</nobr>意図        | ファセットの<nobr>定義</nobr>   |
| ---------------------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------------- |
| カーテン・ウォールを直接構成するあらゆる実体 | 実体（マリオンなど）はカーテンウォールの一部でなければならない。 | 関係"IFCRELAGGREGATES"エンティティ"IFCCURTAINWALL |
| カーテンウォールの直接的または間接的な一部の事業体 | 実体（マリオンなど）はカーテンウォールの一部でなければならない。 | エンティティ"IFCCURTAINWALL |
| 流通システムの一部の事業体 | 実体（ダクトなど）が配電システムの一部であること。 | 関係"IFCRELASSIGNSTOGROUP"エンティティ"IFCDISTRIBUTIONSYSTEM |
| 空間に存在するあらゆる実体 | エンティティ（ポンプなど）は、スペースに配置されていなければならない。 | 関係"IFCRELCONTAINEDINSPATIALSTRUCTURE"エンティティ"IFCSPACE |
| ウォールによってホストされるすべてのエンティティ | エンティティ（窓など）は壁に固定されていなければならない。 | 関係"IFCRELNESTS"エンティティ"IFCWALL |


