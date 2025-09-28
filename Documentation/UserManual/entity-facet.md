# エンティティ・ファセット
IFCモデルのすべてのインスタンスは「IFCクラス」（EXPRESSエンティティとしても知られる）を持つ。例えば、壁のインスタンスはIFCクラスIfcWallを持ち、ドアのインスタンスはIFCクラスIfcDoorを持ちます。個々の建築要素を表さないインスタンスもクラスを持ちます。例えば、プロジェクトはIfcProjectクラス、窓タイプはIfcWindowTypeクラス、コスト項目はIfcCostItemクラスを持っています。

クラスはインスタンスを分類するためだけのものではない。どのような種類のプロパティやリレーションシップを持つことができるかを示すものでもある。例えば、IfcWallクラスのインスタンスは耐火等級プロパティを持つことができますが、IfcGridのインスタンスは持つことができません。

仕様書を作成する上で最も重要なことの1つは、その仕様書が適切なIFCクラスに適用されることを確認することです。通常、すべての**仕様**書には、**適用**セクションで使用される**エンティティ・ファセットが**あります。

IFCスキーマのバージョン間には、クラスの違いがあります。最近のIFCスキーマには、より豊富で多様なIFCクラスが含まれています：

- [IFC4X3_ADD2 IFCクラス名のリスト](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/annex-b1.html)
- [IFC4クラス名のリスト](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/link/alphabeticalorder-entities.htm)
- [IFC2X3 IFCクラス名のリスト](https://standards.buildingsmart.org/IFC/RELEASE/IFC2x3/TC1/HTML/alphabeticalorder_entities.htm)

クラスによっては、オプションで「**定義済みタイプ（Predefined Type）**」を持つこともあります。これは、IFCクラス**名に加えて**、さらなるレベルの分類です。例えば、IfcWallのインスタンスは、SHEARまたはPARTITIONINGという**定義済みタイプを**持つことができます。IFCクラス**名が**IFC標準によって指定されるのに対し、**定義済みタイプは**標準によって指定されますが、ユーザーによって定義されたカスタム値を含むこともあります。[IFC定義済みタイプの使い方については](#ifc-predefined-types)、以下をご覧ください。

## パラメータ
| パラメータ | 必須 | 制限あり | 意味 |
| -------------------------------------- | -------- | -------------------- | ------------------------------------------------------------------------------------------------------------- |
| 名前** (`name`) | ✔️ | ✔️ | IFCスキーマの有効なIFCクラス。IFCクラスは正確に一致しなければならない。大文字で表します。 |
| 定義済みタイプ** (`predefinedType`) | ❌ | ✔️ | IFCスキーマの有効な定義済みタイプ、または任意のカスタム・テキスト値。定義済み型は正確に一致しなければならない。大文字で表現する。 |

## エンティティ・ファセットの解釈
### 適用性
| 団体名 | エンティティ定義済みタイプ | IDSの解釈 |
| ----------- | ---------------------- | ------------------------------------------------------- |
| IFCWINDOW | - | すべての*IfcWindow*エンティティに適用されます。 |
| IFCWINDOW | スカイライト | *天窓*タイプのすべての*IfcWindow*エンティティに適用される。 |

### 必要条件
| IDSカーディナリティ | 団体名 | エンティティ定義済みタイプ | コンフィギュレーションを許可しますか？ | IDSの解釈 |
| --------------- | ----------- | ---------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------- |
| 必須 | IFCWINDOW | - | ✅ | 適用可能なオブジェクトはIFCWINDOWエンティティでなければならない。 |
| 必須 | IFCWINDOW | スカイライト | ✅ | 適用可能なオブジェクトは、エンティティIFCWINDOWと定義済みのタイプSKYLIGHTでなければなりません。 |
| オプション | IFCWINDOW |  | ❌ | オプションは意味をなさない。 |
| オプション | IFCWINDOW | スカイライト | ✅ | 該当するオブジェクトがIFCWINDOWエンティティの場合、それはSKYLIGHT定義済みタイプも持っていなければなりません。 |
| 禁止 | IFCWINDOW |  | ✅ | 適用されるオブジェクトはIFCWINDOWエンティティであることはできない。 |
| 禁止 | IFCWINDOW | スカイライト | ✅ | 適用可能なオブジェクトはIFCWINDOWエンティティ（またはそれ以外）であることができるが、SKYLIGHT定義済みタイプである場合は不可。 |

## IFC定義済みタイプ
IFCスキーマのドキュメントには、標準的な定義済み型のリストが含まれています。ここでは、IFC4X3_ADD2スキーマで有効な**定義済み型の**リストを見つける方法を説明します。この手順は、すべてのIFCバージョンで同様です。

 1. 指定するIFCクラスのドキュメント・ページをブラウズします。上記のIFCクラス名の一覧からアクセスできます。例えば、[これはIfcWallのドキュメント・ページ](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm)です。

 1. ドキュメントの**Attributes**セクションまでスクロールダウンし、**PredefinedType**属性を見つけてください。

 1. **PredefinedType**属性の隣にある列挙リンクをクリックすると、有効な値のリストが表示されます。例えば、IfcWallの場合、リンクをクリックすると[IfcWallTypeEnumのドキュメントが](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWallTypeEnum.htm)表示されます。

 1. 有効な**定義済み型の**リストは表に示されている。

**定義済みタイプが**必要な場合は、標準のリストから選択することを強く推奨する。しかし、プロジェクトに適用されない場合は、任意のカスタム値を指定することができます。

### IFC ファイル内の`predefinedType` を識別するためのロジック：
- **IF:** [オブジェクトが](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm) [型によって](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)定義されている ([IfcRelDefinesByType](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelDefinesByType.htm)リレーションを探す)
  - **IF:** [型オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)、値`USERDEFINED` ➡️✅を持つ`PredefinedType` 。事前定義された型の値は、その[型オブジェクトの](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm) `ElementType` 属性にある。
  - **ELSE IF:**その[型オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)、`USERDEFINED` ➡️ ✅以外の値を持つ`PredefinedType` を持つ。事前定義された型の値は、その[型オブジェクトの](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm) `PredefinedType` 属性にある。
  - **ELSE:** [型オブジェクトが](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)定義済みの型を定義していない。⬇️
- **ELSE：**
  - `ObjectType` I**F:** [オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm)、値`USERDEFINED` ➡️ を持つ`PredefinedType` を持つ。
  - **ELSE IF:** [オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm) `USERDEFINED` 以外の値を持つ`PredefinedType` を持つ ➡️ ✅ 定義済みの型の値は、その[オブジェクトの](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm) `PredefinedType` 属性にある。
  - **ELSE:** [オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm)定義済みの型を持たない。🔚

### IFC 定義済みデータ型の使用例
| IDSエンティティ | IDS定義済みタイプ | IFCエンティティ | IFC定義済みタイプ | IFC要素/オブジェクト・タイプ | IFCxIDSの結果 |
| ---------- | ------------------- | ---------- | ------------------- | ----------------------- | -------------- |
| IFCWALL | ユーザー定義 | IFCWALL | ユーザー定義 | - | ✅ |
| IFCWALL | ユーザー定義 | IFCWALL | ユーザー定義 | FOO | ✅ |
| IFCWALL | FOO | IFCWALL | ユーザー定義 | FOO | ✅ |
| IFCWALL | FOO | IFCWALL | FOO | - | ✅ |


## IFC2X3の特殊ケース
IFC2X3のいくつかの出現エンティティは、タイプオブジェクトによってさらに指定される。  
これはIFC2X3では、IfcFlowTerminalの出現インスタンスとIfcAirTerminalTypeの型インスタンスによってエンコードされる。  
エンティティ・ファセットには、タイプ・エンティティ名をさらに指定するパラメータがない。  
この場合、IDSはIFC4で導入された規約に従い、IDSに基づくチェックはスキーマにとらわれないものとなる。  
与えられた例では、チェックされるエンティティの**名前は**IfcAirTerminal（タイプなし）でなければならず、与えられたマッピングテーブルによって解決されなければならない。  
全リストはこの[表に](./Documentation/ImplementersDocumentation/ifc2x3-occurrence-type-mapping-table.md)ある。

## 継承
IDS のエンティティ・ファセット解釈には、自動継承はない。つまり、すべてのエンティティを明示的に列挙する必要がある。これにより、正確で曖昧さのない仕様が可能になる。

たとえば、すべての IfcElement オブジェクトに適用される要件を作成するには、IfcWall や IfcDoor などのすべての IfcElement サブエンティティをリストする必要があります。また、IfcElement は抽象エンティティであり、インスタンス化できないため、モデルには表示されない。

ユーザーやソフトウェア実装者が、IfcElement、IfcBuiltElement、IfcFlowSegment などのよく使われるサブエンティティを指定しやすくするために、以下の表を用意した。

### 異なるIFCバージョンにおけるIfcElementサブエンティティ
|  | IFC2X3 | IFC4 | IFC4X3 |
|-----------------------------------------------------|--------|------|--------|
| ifcElement | ⚠️ | ⚠️ | ⚠️ |
| ──IfcBuildingElement | ⚠️ | ⚠️ |  |
| ──IfcBuiltElement |  |  | ✅ |
| ──IfcBeam | ✅ | ✅ | ✅ |
| ───────────────IfcBeamStandardCase |  | 🚫 | 🚫 |
| ──Ifcベアリング |  |  | ✅ |
| ──────────────IfcBuildingElementProxy | ✅ | ✅ | ✅ |
| ──イフチムニー |  | ✅ | ✅ |
| ──IfcColumn | ✅ | ✅ | ✅ |
| ────────────────IfcColumnStandardCase |  | 🚫 |  |
| ──イフコース |  |  | ✅ |
| ──イフカバー | ✅ | ✅ | ✅ |
| ──イフカーテンウォール | ✅ | ✅ | ✅ |
| ──イフシーディープ財団 |  |  | ✅ |
| ────イフカイソン財団 |  |  | ✅ |
| ────IfcPile | ✅ | ✅ | ✅ |
| ──イフクドア | ✅ | ✅ | ✅ |
| ──────────────IfcDoorStandardCase |  | 🚫 |  |
| ────IfcEarthworksElement |  |  | ✅ |
| ────IfcEarthworksFill |  |  | ✅ |
| ─────────────────────── IfcReinforcedSoil |  |  | ✅ |
| ──IfcFooting | ✅ | ✅ | ✅ |
| ──IfcKerb |  |  | ✅ |
| ──IfcMember | ✅ | ✅ | ✅ |
| ────────────────────IfcMemberStandardCase |  | 🚫 |  |
| ────IfcMooringDevice |  |  | ✅ |
| ────IfcNavigationElement |  |  | ✅ |
| ──IfcPavement |  |  | ✅ |
| ──Ifcプレート | ✅ | ✅ | ✅ |
| ───────────────IfcPlateStandardCase |  | 🚫 |  |
| ──IfcRail |  |  | ✅ |
| ──IfcRailing | ✅ | ✅ | ✅ |
| ──IfcRamp | ✅ | ✅ | ✅ |
| ───IfcRampFlight | ✅ | ✅ | ✅ |
| ──イフクルーフ | ✅ | ✅ | ✅ |
| ────IfcShadingDevice |  | ✅ | ✅ |
| ──IfcSlab | ✅ | ✅ | ✅ |
| ──────────────────────IfcSlabElementedCase |  | 🚫 |  |
| ───────────────IfcSlabStandardCase |  | 🚫 |  |
| ──IfcStair | ✅ | ✅ | ✅ |
| ──IfcStairFlight | ✅ | ✅ | ✅ |
| ────IfcTrackElement |  |  | ✅ |
| ──IfcWall | ✅ | ✅ | ✅ |
| ────────────────IfcWallElementedCase |  | 🚫 |  |
| ───────────────IfcWallStandardCase |  | 🚫 | 🚫 |
| ──IfcWindow | ✅ | ✅ | ✅ |
| ────────────────────IfcWindowStandardCase |  | 🚫 |  |
| ──IfcDistributionElement。 | ✅ | ✅ | ✅ |
| ──────────────────────────IfcDistributionFlowElement | ✅ | ✅ | ✅ |
| ────────────────IfcEnergyConversionDevice | ⚠️ | ✅ |  |
| ────────────IfcCoolingTower |  | ✅ | ✅ |
| ───────────────IfcAirToAirHeatRecovery | ✅ | ✅ |  |
| ─────────IfcBoiler |  | ✅ | ✅ |
| ────────IfcBurner |  | ✅ | ✅ |
| ──────イフチラー |  | ✅ | ✅ |
| ──────イフコイル |  | ✅ | ✅ |
| Ifコンデンサー |  | ✅ | ✅ |
| ──────イフクールドビーム |  | ✅ | ✅ |
| ──────── IfcElectricGenerator |  | ✅ | ✅ |
| ────────────────────────IfcElectricMotor |  | ✅ | ✅ |
| ────────IfcEngine |  | ✅ | ✅ |
| ───────────────────────────────────────────────────────IfcEvaporativeCooler | ✅ | ✅ |  |
| ───────────────IfcEvaporator |  | ✅ | ✅ |
| ──────────────IfcHeatExchanger |  | ✅ | ✅ |
| ───────────────IfcHumidifier |  | ✅ | ✅ |
| ─────────────────────IfcMotorConnection |  | ✅ | ✅ |
| ────────────IfcSolarDevice |  | ✅ | ✅ |
| ───────────────────────IfcTransformer |  | ✅ | ✅ |
| ─────────IfcTubeBundle |  | ✅ | ✅ |
| ────────────────IfcUnitaryEquipment | ✅ | ✅ |  |
| ─────────────────────IfcDistributionChamberElement | ✅ | ✅ |  |
| ────────IfcFlowController | ✅ | ⚠️ | ✅ |
| ────────────────IfcAirTerminalBox |  | ✅ | ✅ |
| ───────────────IfcDamper |  | ✅ | ✅ |
| ─────────────────IfcDistributionBoard |  |  | ✅ |
| ────────────────────────────────────────IfcElectricDistributionBoard | ✅ | 🚫 | 🚫 |
| ─────────────────────────────────────────────────────IfcElectricTimeControl | ✅ | ✅ |  |
| ─────────────────IfcFlowMeter |  | ✅ | ✅ |
| ───────────────IfcProtectiveDevice |  | ✅ | ✅ |
| ────────────────IfcSwitchingDevice |  | ✅ | ✅ |
| ────────────IfcValve |  | ✅ | ✅ |
| ────────IfcFlowFitting | ✅ | ⚠️ | ✅ |
| ─────────────────────────IfcCableCarrierFitting | ✅ | ✅ |  |
| ───────────────────────────────────────────────────────────IfcCableFitting |  | ✅ | ✅ |
| ────────────────IfcDuctFitting |  | ✅ | ✅ |
| ──────────IfcJunctionBox |  | ✅ | ✅ |
| ──────────────────IfcPipeFitting |  | ✅ | ✅ |
| ────────────────IfcFlowMovingDevice | ✅ | ⚠️ | ✅ |
| ───────────────IfcCompressor |  | ✅ | ✅ |
| ──────IfcFan |  | ✅ | ✅ |
| ────────IfcPump |  | ✅ | ✅ |
| ──────────────────────IfcFlowSegment | ✅ | ⚠️ | ✅ |
| ────────────────────────IfcCableCarrierSegment | ✅ | ✅ |  |
| ────────────────────IfcCableSegment |  | ✅ | ✅ |
| ──────────────────────IfcConveyorSegment |  | ✅ |  |
| ────────────────────IfcDuctSegment |  | ✅ | ✅ |
| ────────────────────────IfcPipeSegment |  | ✅ | ✅ |
| ────────────────IfcFlowStorageDevice | ✅ | ⚠️ | ✅ |
| ────────────────────────────────────IfcElectricFlowStorageDevice | ✅ | ✅ |  |
| ────────IfcTank |  | ✅ | ✅ |
| ──────────────IfcFlowTerminal | ✅ | ⚠️ | ✅ |
| ────────────────IfcAirTerminal |  | ✅ | ✅ |
| ───────────────IfcAudioVisualAppliance | ✅ | ✅ |  |
| 通信アプライアンス | ✅ | ✅ |  |
| ────────────────IfcElectricAppliance |  | ✅ | ✅ |
| ─────────────────────────────────IfcFireSuppressionTerminal | ✅ | ✅ |  |
| ────────IfcLamp |  | ✅ | ✅ |
| ──────────────IfcLightFixture |  | ✅ | ✅ |
| ─────────────────────IfcLiquidTerminal |  |  | ✅ |
| ───────────────IfcMedicalDevice |  | ✅ | ✅ |
| ───────────────────IfcMobileTelecommunicationsAppliance |  | ✅ |  |
| ──────────────IfcOutlet |  | ✅ | ✅ |
| ─────────────────IfcSanitaryTerminal |  | ✅ | ✅ |
| ────────IfcSignal |  |  | ✅ |
| ────────IfcSpaceHeater |  | ✅ | ✅ |
| ────────────────IfcStackTerminal |  | ✅ | ✅ |
| ──────────────────IfcWasteTerminal |  | ✅ | ✅ |
| ────────────────IfcFlowTreatmentDevice | ✅ | ⚠️ | ✅ |
| ────────────────IfcDuctSilencer |  | ✅ | ✅ |
| ──────── IfcElectricFlowTreatmentDevice |  | ✅ |  |
| ────────────────IfcFilter |  | ✅ | ✅ |
| ───────────────IfcInterceptor |  | ✅ | ✅ |
| ────────────────────────IfcDistributionControlElement | ✅ | ✅ | ✅ |
| ────Ifcアクチュエーター |  | ✅ | ✅ |
| ──────IfcAlarm |  | ✅ | ✅ |
| ──────IfcController |  | ✅ | ✅ |
| ───────────────IfcFlowInstrument |  | ✅ | ✅ |
| ──────────────────────────────IfcProtectiveDeviceTrippingUnit | ✅ | ✅ |  |
| ────Ifcセンサー |  | ✅ | ✅ |
| ──────────────────────IfcUnitaryControlElement |  | ✅ | ✅ |
| ──イフシビル・エレメント |  | ✅ | 🚫 |
| ──IfcElementAssembly | ✅ | ✅ | ✅ |
| ──IfcBuildingElementComponent。 | ✅ |  |  |
| ──IfcElementComponent |  | ⚠️ | ⚠️ |
| ────────────────────────IfcBuildingElementPart |  | ✅ | ✅ |
| ──イフクリート・アクセサリー |  | ✅ | ✅ |
| ──Ifcファスナー |  | ✅ | ✅ |
| ────IfcImpactProtectionDevice |  |  | ✅ |
| ────────IfcMechanicalFastener |  | ✅ | ✅ |
| ──────────────────IfcReinforcingElement |  | ⚠️ | ⚠️ |
| ───────────────IfcReinforcingBar |  | ✅ | ✅ |
| ──────IfcReinforcingMesh |  | ✅ | ✅ |
| ────IfcTendon |  | ✅ | ✅ |
| ──────IfcTendonAnchor |  | ✅ | ✅ |
| ────IfcTendonConduit |  |  | ✅ |
| ──IfcSign |  |  | ✅ |
| ────IfcVibrationDamper |  |  | ✅ |
| ──IfcVibrationIsolator（イフシー・バイブレーション・アイソレーター |  | ✅ | ✅ |
| ──IfcFeatureElement | ✅ | ⚠️ | ⚠️ |
| ─────────────────IfcFeatureElementAddition | ✅ | ⚠️ | ⚠️ |
| ────────IfcProjectionElement | ✅ | ✅ | ✅ |
| ──IfcFeatureElementSubtraction（イフシー・フィーチャー・エレメント・サブトラクション | ✅ | ⚠️ | ⚠️ |
| ────IfcEarthworksCut |  |  | ✅ |
| ────────────IfcOpeningElement | ✅ | ✅ | ✅ |
| ──────IfcVoidingFeature |  | ✅ | ✅ |
| ────IfcSurfaceFeature |  | ✅ | ✅ |
| ──IfcFurnishingElement | ✅ | ✅ | ✅ |
| ──IfcFurniture |  | ✅ | ✅ |
| ──────────────────────IfcSystemFurnitureElement |  | ✅ | ✅ |
| ──IfcGeographicElement |  | ✅ | ✅ |
| IfcGeotechnicalElement──ジオテクニカル・エレメント |  |  | ⚠️ |
| ───────────────────────────────────IFCGeotechnicalAssembly |  |  | ⚠️ |
| ────IfcBorehole |  |  | ✅ |
| ──────IfcGeomodel |  |  | ✅ |
| ────イフチアスライス |  |  | ✅ |
| ──イフコ・ジオテクニカル・ストラタム |  |  | ✅ |
| ──IfcTransportationDevice（イフシー・トランスポーテーション・デバイス |  |  | ⚠️ |
| ──────────────────────IfcTransportElement | ✅ | ✅ | ✅ |
| ──IfcVehicle |  |  | ✅ |
| ──IfcVirtualElement | ✅ | ✅ | ✅ |
| ──IfcElectricalElement | 🚫 |  |  |
| ──IfcEquipmentElement | ✅ |  |  |

IFC バージョンに含まれています。  
⚠️ - 含まれているが抽象的。  
🚫 - 非推奨

### 異なるIFCバージョンにおけるIfcElementサブ・エンティティのリスト
以下に、IfcElementのサブエンティティのリストを、IDSファイルにコピーペーストしやすい形で示します。簡単のため、このリストにはTypeオブジェクトは含まれていない。

**IFC4X3におけるカンマ区切りのIfcElementサブエンティティ：**
```
IFCACTUATOR,IFCAIRTERMINAL,IFCAIRTERMINALBOX,IFCAIRTOAIRHEATRECOVERY,IFCALARM,IFCAUDIOVISUALAPPLIANCE,IFCBEAM,IFCBEARING,IFCBOILER,IFCBOREHOLE,IFCBUILDINGELEMENTPART,IFCBUILDINGELEMENTPROXY,IFCBUILTELEMENT,IFCBURNER,IFCCABLECARRIERFITTING,IFCCABLECARRIERSEGMENT,IFCCABLEFITTING,IFCCABLESEGMENT,IFCCAISSONFOUNDATION,IFCCHILLER,IFCCHIMNEY,IFCCOIL,IFCCOLUMN,IFCCOMMUNICATIONSAPPLIANCE,IFCCOMPRESSOR,IFCCONDENSER,IFCCONTROLLER,IFCCONVEYORSEGMENT,IFCCOOLEDBEAM,IFCCOOLINGTOWER,IFCCOURSE,IFCCOVERING,IFCCURTAINWALL,IFCDAMPER,IFCDEEPFOUNDATION,IFCDISCRETEACCESSORY,IFCDISTRIBUTIONBOARD,IFCDISTRIBUTIONCHAMBERELEMENT,IFCDISTRIBUTIONCONTROLELEMENT,IFCDISTRIBUTIONELEMENT,IFCDISTRIBUTIONFLOWELEMENT,IFCDOOR,IFCDUCTFITTING,IFCDUCTSEGMENT,IFCDUCTSILENCER,IFCEARTHWORKSCUT,IFCEARTHWORKSELEMENT,IFCEARTHWORKSFILL,IFCELECTRICAPPLIANCE,IFCELECTRICFLOWSTORAGEDEVICE,IFCELECTRICFLOWTREATMENTDEVICE,IFCELECTRICGENERATOR,IFCELECTRICMOTOR,IFCELECTRICTIMECONTROL,IFCELEMENTASSEMBLY,IFCENERGYCONVERSIONDEVICE,IFCENGINE,IFCEVAPORATIVECOOLER,IFCEVAPORATOR,IFCFAN,IFCFASTENER,IFCFILTER,IFCFIRESUPPRESSIONTERMINAL,IFCFLOWCONTROLLER,IFCFLOWFITTING,IFCFLOWINSTRUMENT,IFCFLOWMETER,IFCFLOWMOVINGDEVICE,IFCFLOWSEGMENT,IFCFLOWSTORAGEDEVICE,IFCFLOWTERMINAL,IFCFLOWTREATMENTDEVICE,IFCFOOTING,IFCFURNISHINGELEMENT,IFCFURNITURE,IFCGEOGRAPHICELEMENT,IFCGEOMODEL,IFCGEOSLICE,IFCGEOTECHNICALSTRATUM,IFCHEATEXCHANGER,IFCHUMIDIFIER,IFCIMPACTPROTECTIONDEVICE,IFCINTERCEPTOR,IFCJUNCTIONBOX,IFCKERB,IFCLAMP,IFCLIGHTFIXTURE,IFCLIQUIDTERMINAL,IFCMECHANICALFASTENER,IFCMEDICALDEVICE,IFCMEMBER,IFCMOBILETELECOMMUNICATIONSAPPLIANCE,IFCMOORINGDEVICE,IFCMOTORCONNECTION,IFCNAVIGATIONELEMENT,IFCOPENINGELEMENT,IFCOUTLET,IFCPAVEMENT,IFCPILE,IFCPIPEFITTING,IFCPIPESEGMENT,IFCPLATE,IFCPROJECTIONELEMENT,IFCPROTECTIVEDEVICE,IFCPROTECTIVEDEVICETRIPPINGUNIT,IFCPUMP,IFCRAIL,IFCRAILING,IFCRAMP,IFCRAMPFLIGHT,IFCREINFORCEDSOIL,IFCREINFORCINGBAR,IFCREINFORCINGMESH,IFCROOF,IFCSANITARYTERMINAL,IFCSENSOR,IFCSHADINGDEVICE,IFCSIGN,IFCSIGNAL,IFCSLAB,IFCSOLARDEVICE,IFCSPACEHEATER,IFCSTACKTERMINAL,IFCSTAIR,IFCSTAIRFLIGHT,IFCSURFACEFEATURE,IFCSWITCHINGDEVICE,IFCSYSTEMFURNITUREELEME,IFCTANK,IFCTENDON,IFCTENDONANCHOR,IFCTENDONCONDUIT,IFCTRACKELEMENT,IFCTRANSFORMER,IFCTRANSPORTELEMENT,IFCTUBEBUNDLE,IFCUNITARYCONTROLELEMENT,IFCUNITARYEQUIPMENT,IFCVALVE,IFCVEHICLE,IFCVIBRATIONDAMPER,IFCVIBRATIONISOLATOR,IFCVIRTUALELEMENT,IFCVOIDINGFEATURE,IFCWALL,IFCWASTETERMINAL,IFCWINDOW
```

<details><summary>✂️  IfcElement subentities in IFC4X3 as IDS entity facet</summary>

```
<ids:entity>
    <ids:name>
        <xs:restriction base="xs:string">
            <xs:enumeration value="IFCACTUATOR" />
            <xs:enumeration value="IFCAIRTERMINAL" />
            <xs:enumeration value="IFCAIRTERMINALBOX" />
            <xs:enumeration value="IFCAIRTOAIRHEATRECOVERY" />
            <xs:enumeration value="IFCALARM" />
            <xs:enumeration value="IFCAUDIOVISUALAPPLIANCE" />
            <xs:enumeration value="IFCBEAM" />
            <xs:enumeration value="IFCBEARING" />
            <xs:enumeration value="IFCBOILER" />
            <xs:enumeration value="IFCBOREHOLE" />
            <xs:enumeration value="IFCBUILDINGELEMENTPART" />
            <xs:enumeration value="IFCBUILDINGELEMENTPROXY" />
            <xs:enumeration value="IFCBUILTELEMENT" />
            <xs:enumeration value="IFCBURNER" />
            <xs:enumeration value="IFCCABLECARRIERFITTING" />
            <xs:enumeration value="IFCCABLECARRIERSEGMENT" />
            <xs:enumeration value="IFCCABLEFITTING" />
            <xs:enumeration value="IFCCABLESEGMENT" />
            <xs:enumeration value="IFCCAISSONFOUNDATION" />
            <xs:enumeration value="IFCCHILLER" />
            <xs:enumeration value="IFCCHIMNEY" />
            <xs:enumeration value="IFCCOIL" />
            <xs:enumeration value="IFCCOLUMN" />
            <xs:enumeration value="IFCCOMMUNICATIONSAPPLIANCE" />
            <xs:enumeration value="IFCCOMPRESSOR" />
            <xs:enumeration value="IFCCONDENSER" />
            <xs:enumeration value="IFCCONTROLLER" />
            <xs:enumeration value="IFCCONVEYORSEGMENT" />
            <xs:enumeration value="IFCCOOLEDBEAM" />
            <xs:enumeration value="IFCCOOLINGTOWER" />
            <xs:enumeration value="IFCCOURSE" />
            <xs:enumeration value="IFCCOVERING" />
            <xs:enumeration value="IFCCURTAINWALL" />
            <xs:enumeration value="IFCDAMPER" />
            <xs:enumeration value="IFCDEEPFOUNDATION" />
            <xs:enumeration value="IFCDISCRETEACCESSORY" />
            <xs:enumeration value="IFCDISTRIBUTIONBOARD" />
            <xs:enumeration value="IFCDISTRIBUTIONCHAMBERELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONCONTROLELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONFLOWELEMENT" />
            <xs:enumeration value="IFCDOOR" />
            <xs:enumeration value="IFCDUCTFITTING" />
            <xs:enumeration value="IFCDUCTSEGMENT" />
            <xs:enumeration value="IFCDUCTSILENCER" />
            <xs:enumeration value="IFCEARTHWORKSCUT" />
            <xs:enumeration value="IFCEARTHWORKSELEMENT" />
            <xs:enumeration value="IFCEARTHWORKSFILL" />
            <xs:enumeration value="IFCELECTRICAPPLIANCE" />
            <xs:enumeration value="IFCELECTRICFLOWSTORAGEDEVICE" />
            <xs:enumeration value="IFCELECTRICFLOWTREATMENTDEVICE" />
            <xs:enumeration value="IFCELECTRICGENERATOR" />
            <xs:enumeration value="IFCELECTRICMOTOR" />
            <xs:enumeration value="IFCELECTRICTIMECONTROL" />
            <xs:enumeration value="IFCELEMENTASSEMBLY" />
            <xs:enumeration value="IFCENERGYCONVERSIONDEVICE" />
            <xs:enumeration value="IFCENGINE" />
            <xs:enumeration value="IFCEVAPORATIVECOOLER" />
            <xs:enumeration value="IFCEVAPORATOR" />
            <xs:enumeration value="IFCFAN" />
            <xs:enumeration value="IFCFASTENER" />
            <xs:enumeration value="IFCFILTER" />
            <xs:enumeration value="IFCFIRESUPPRESSIONTERMINAL" />
            <xs:enumeration value="IFCFLOWCONTROLLER" />
            <xs:enumeration value="IFCFLOWFITTING" />
            <xs:enumeration value="IFCFLOWINSTRUMENT" />
            <xs:enumeration value="IFCFLOWMETER" />
            <xs:enumeration value="IFCFLOWMOVINGDEVICE" />
            <xs:enumeration value="IFCFLOWSEGMENT" />
            <xs:enumeration value="IFCFLOWSTORAGEDEVICE" />
            <xs:enumeration value="IFCFLOWTERMINAL" />
            <xs:enumeration value="IFCFLOWTREATMENTDEVICE" />
            <xs:enumeration value="IFCFOOTING" />
            <xs:enumeration value="IFCFURNISHINGELEMENT" />
            <xs:enumeration value="IFCFURNITURE" />
            <xs:enumeration value="IFCGEOGRAPHICELEMENT" />
            <xs:enumeration value="IFCGEOMODEL" />
            <xs:enumeration value="IFCGEOSLICE" />
            <xs:enumeration value="IFCGEOTECHNICALSTRATUM" />
            <xs:enumeration value="IFCHEATEXCHANGER" />
            <xs:enumeration value="IFCHUMIDIFIER" />
            <xs:enumeration value="IFCIMPACTPROTECTIONDEVICE" />
            <xs:enumeration value="IFCINTERCEPTOR" />
            <xs:enumeration value="IFCJUNCTIONBOX" />
            <xs:enumeration value="IFCKERB" />
            <xs:enumeration value="IFCLAMP" />
            <xs:enumeration value="IFCLIGHTFIXTURE" />
            <xs:enumeration value="IFCLIQUIDTERMINAL" />
            <xs:enumeration value="IFCMECHANICALFASTENER" />
            <xs:enumeration value="IFCMEDICALDEVICE" />
            <xs:enumeration value="IFCMEMBER" />
            <xs:enumeration value="IFCMOBILETELECOMMUNICATIONSAPPLIANCE" />
            <xs:enumeration value="IFCMOORINGDEVICE" />
            <xs:enumeration value="IFCMOTORCONNECTION" />
            <xs:enumeration value="IFCNAVIGATIONELEMENT" />
            <xs:enumeration value="IFCOPENINGELEMENT" />
            <xs:enumeration value="IFCOUTLET" />
            <xs:enumeration value="IFCPAVEMENT" />
            <xs:enumeration value="IFCPILE" />
            <xs:enumeration value="IFCPIPEFITTING" />
            <xs:enumeration value="IFCPIPESEGMENT" />
            <xs:enumeration value="IFCPLATE" />
            <xs:enumeration value="IFCPROJECTIONELEMENT" />
            <xs:enumeration value="IFCPROTECTIVEDEVICE" />
            <xs:enumeration value="IFCPROTECTIVEDEVICETRIPPINGUNIT" />
            <xs:enumeration value="IFCPUMP" />
            <xs:enumeration value="IFCRAIL" />
            <xs:enumeration value="IFCRAILING" />
            <xs:enumeration value="IFCRAMP" />
            <xs:enumeration value="IFCRAMPFLIGHT" />
            <xs:enumeration value="IFCREINFORCEDSOIL" />
            <xs:enumeration value="IFCREINFORCINGBAR" />
            <xs:enumeration value="IFCREINFORCINGMESH" />
            <xs:enumeration value="IFCROOF" />
            <xs:enumeration value="IFCSANITARYTERMINAL" />
            <xs:enumeration value="IFCSENSOR" />
            <xs:enumeration value="IFCSHADINGDEVICE" />
            <xs:enumeration value="IFCSIGN" />
            <xs:enumeration value="IFCSIGNAL" />
            <xs:enumeration value="IFCSLAB" />
            <xs:enumeration value="IFCSOLARDEVICE" />
            <xs:enumeration value="IFCSPACEHEATER" />
            <xs:enumeration value="IFCSTACKTERMINAL" />
            <xs:enumeration value="IFCSTAIR" />
            <xs:enumeration value="IFCSTAIRFLIGHT" />
            <xs:enumeration value="IFCSURFACEFEATURE" />
            <xs:enumeration value="IFCSWITCHINGDEVICE" />
            <xs:enumeration value="IFCSYSTEMFURNITUREELEME" />
            <xs:enumeration value="IFCTANK" />
            <xs:enumeration value="IFCTENDON" />
            <xs:enumeration value="IFCTENDONANCHOR" />
            <xs:enumeration value="IFCTENDONCONDUIT" />
            <xs:enumeration value="IFCTRACKELEMENT" />
            <xs:enumeration value="IFCTRANSFORMER" />
            <xs:enumeration value="IFCTRANSPORTELEMENT" />
            <xs:enumeration value="IFCTUBEBUNDLE" />
            <xs:enumeration value="IFCUNITARYCONTROLELEMENT" />
            <xs:enumeration value="IFCUNITARYEQUIPMENT" />
            <xs:enumeration value="IFCVALVE" />
            <xs:enumeration value="IFCVEHICLE" />
            <xs:enumeration value="IFCVIBRATIONDAMPER" />
            <xs:enumeration value="IFCVIBRATIONISOLATOR" />
            <xs:enumeration value="IFCVIRTUALELEMENT" />
            <xs:enumeration value="IFCVOIDINGFEATURE" />
            <xs:enumeration value="IFCWALL" />
            <xs:enumeration value="IFCWASTETERMINAL" />
            <xs:enumeration value="IFCWINDOW" />
        </xs:restriction>
    </ids:name>
</ids:entity>
```
</details>

**IFC4におけるカンマ区切りのIfcElementサブエンティティ：**
```
IFCBEAM,IFCACTUATOR,IFCAIRTERMINAL,IFCAIRTERMINALBOX,IFCAIRTOAIRHEATRECOVERY,IFCALARM,IFCAUDIOVISUALAPPLIANCE,IFCBOILER,IFCBUILDINGELEMENTPART,IFCBUILDINGELEMENTPROXY,IFCBURNER,IFCCABLECARRIERFITTING,IFCCABLECARRIERSEGMENT,IFCCABLEFITTING,IFCCABLESEGMENT,IFCCHILLER,IFCCHIMNEY,IFCCIVILELEMENT,IFCCOIL,IFCCOLUMN,IFCCOMMUNICATIONSAPPLIANCE,IFCCOMPRESSOR,IFCCONDENSER,IFCCONTROLLER,IFCCOOLEDBEAM,IFCCOOLINGTOWER,IFCCOVERING,IFCCURTAINWALL,IFCDAMPER,IFCDISCRETEACCESSORY,IFCDISTRIBUTIONCHAMBERELEMENT,IFCDISTRIBUTIONCONTROLELEMENT,IFCDISTRIBUTIONELEMENT,IFCDISTRIBUTIONFLOWELEMENT,IFCDOOR,IFCDUCTFITTING,IFCDUCTSEGMENT,IFCDUCTSILENCER,IFCELECTRICAPPLIANCE,IFCELECTRICDISTRIBUTIONBOARD,IFCELECTRICFLOWSTORAGEDEVICE,IFCELECTRICGENERATOR,IFCELECTRICMOTOR,IFCELECTRICTIMECONTROL,IFCELEMENTASSEMBLY,IFCENGINE,IFCEVAPORATIVECOOLER,IFCEVAPORATOR,IFCFAN,IFCFASTENER,IFCFILTER,IFCFIRESUPPRESSIONTERMINAL,IFCFLOWINSTRUMENT,IFCFLOWMETER,IFCFOOTING,IFCFURNISHINGELEMENT,IFCFURNITURE,IFCGEOGRAPHICELEMENT,IFCHEATEXCHANGER,IFCHUMIDIFIER,IFCINTERCEPTOR,IFCJUNCTIONBOX,IFCLAMP,IFCLIGHTFIXTURE,IFCMECHANICALFASTENER,IFCMEDICALDEVICE,IFCMEMBER,IFCMOTORCONNECTION,IFCOPENINGELEMENT,IFCOUTLET,IFCPILE,IFCPIPEFITTING,IFCPIPESEGMENT,IFCPLATE,IFCPROJECTIONELEMENT,IFCPROTECTIVEDEVICE,IFCPROTECTIVEDEVICETRIPPINGUNIT,IFCPUMP,IFCRAILING,IFCRAMP,IFCRAMPFLIGHT,IFCREINFORCINGBAR,IFCREINFORCINGMESH,IFCROOF,IFCSANITARYTERMINAL,IFCSENSOR,IFCSHADINGDEVICE,IFCSLAB,IFCSOLARDEVICE,IFCSPACEHEATER,IFCSTACKTERMINAL,IFCSTAIR,IFCSTAIRFLIGHT,IFCSURFACEFEATURE,IFCSWITCHINGDEVICE,IFCSYSTEMFURNITUREELEME,IFCTANK,IFCTENDON,IFCTENDONANCHOR,IFCTRANSFORMER,IFCTRANSPORTELEMENT,IFCTUBEBUNDLE,IFCUNITARYCONTROLELEMENT,IFCUNITARYEQUIPMENT,IFCVALVE,IFCVIBRATIONISOLATOR,IFCVIRTUALELEMENT,IFCVOIDINGFEATURE,IFCWALL,IFCWASTETERMINAL,IFCWINDOW
```

<details><summary>✂️  IfcElement subentities in IFC4 as IDS entity facet</summary>

```
<ids:entity>
    <ids:name>
        <xs:restriction base="xs:string">
            <xs:enumeration value="IFCBEAM" />
            <xs:enumeration value="IFCACTUATOR" />
            <xs:enumeration value="IFCAIRTERMINAL" />
            <xs:enumeration value="IFCAIRTERMINALBOX" />
            <xs:enumeration value="IFCAIRTOAIRHEATRECOVERY" />
            <xs:enumeration value="IFCALARM" />
            <xs:enumeration value="IFCAUDIOVISUALAPPLIANCE" />
            <xs:enumeration value="IFCBOILER" />
            <xs:enumeration value="IFCBUILDINGELEMENTPART" />
            <xs:enumeration value="IFCBUILDINGELEMENTPROXY" />
            <xs:enumeration value="IFCBURNER" />
            <xs:enumeration value="IFCCABLECARRIERFITTING" />
            <xs:enumeration value="IFCCABLECARRIERSEGMENT" />
            <xs:enumeration value="IFCCABLEFITTING" />
            <xs:enumeration value="IFCCABLESEGMENT" />
            <xs:enumeration value="IFCCHILLER" />
            <xs:enumeration value="IFCCHIMNEY" />
            <xs:enumeration value="IFCCIVILELEMENT" />
            <xs:enumeration value="IFCCOIL" />
            <xs:enumeration value="IFCCOLUMN" />
            <xs:enumeration value="IFCCOMMUNICATIONSAPPLIANCE" />
            <xs:enumeration value="IFCCOMPRESSOR" />
            <xs:enumeration value="IFCCONDENSER" />
            <xs:enumeration value="IFCCONTROLLER" />
            <xs:enumeration value="IFCCOOLEDBEAM" />
            <xs:enumeration value="IFCCOOLINGTOWER" />
            <xs:enumeration value="IFCCOVERING" />
            <xs:enumeration value="IFCCURTAINWALL" />
            <xs:enumeration value="IFCDAMPER" />
            <xs:enumeration value="IFCDISCRETEACCESSORY" />
            <xs:enumeration value="IFCDISTRIBUTIONCHAMBERELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONCONTROLELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONFLOWELEMENT" />
            <xs:enumeration value="IFCDOOR" />
            <xs:enumeration value="IFCDUCTFITTING" />
            <xs:enumeration value="IFCDUCTSEGMENT" />
            <xs:enumeration value="IFCDUCTSILENCER" />
            <xs:enumeration value="IFCELECTRICAPPLIANCE" />
            <xs:enumeration value="IFCELECTRICDISTRIBUTIONBOARD" />
            <xs:enumeration value="IFCELECTRICFLOWSTORAGEDEVICE" />
            <xs:enumeration value="IFCELECTRICGENERATOR" />
            <xs:enumeration value="IFCELECTRICMOTOR" />
            <xs:enumeration value="IFCELECTRICTIMECONTROL" />
            <xs:enumeration value="IFCELEMENTASSEMBLY" />
            <xs:enumeration value="IFCENGINE" />
            <xs:enumeration value="IFCEVAPORATIVECOOLER" />
            <xs:enumeration value="IFCEVAPORATOR" />
            <xs:enumeration value="IFCFAN" />
            <xs:enumeration value="IFCFASTENER" />
            <xs:enumeration value="IFCFILTER" />
            <xs:enumeration value="IFCFIRESUPPRESSIONTERMINAL" />
            <xs:enumeration value="IFCFLOWINSTRUMENT" />
            <xs:enumeration value="IFCFLOWMETER" />
            <xs:enumeration value="IFCFOOTING" />
            <xs:enumeration value="IFCFURNISHINGELEMENT" />
            <xs:enumeration value="IFCFURNITURE" />
            <xs:enumeration value="IFCGEOGRAPHICELEMENT" />
            <xs:enumeration value="IFCHEATEXCHANGER" />
            <xs:enumeration value="IFCHUMIDIFIER" />
            <xs:enumeration value="IFCINTERCEPTOR" />
            <xs:enumeration value="IFCJUNCTIONBOX" />
            <xs:enumeration value="IFCLAMP" />
            <xs:enumeration value="IFCLIGHTFIXTURE" />
            <xs:enumeration value="IFCMECHANICALFASTENER" />
            <xs:enumeration value="IFCMEDICALDEVICE" />
            <xs:enumeration value="IFCMEMBER" />
            <xs:enumeration value="IFCMOTORCONNECTION" />
            <xs:enumeration value="IFCOPENINGELEMENT" />
            <xs:enumeration value="IFCOUTLET" />
            <xs:enumeration value="IFCPILE" />
            <xs:enumeration value="IFCPIPEFITTING" />
            <xs:enumeration value="IFCPIPESEGMENT" />
            <xs:enumeration value="IFCPLATE" />
            <xs:enumeration value="IFCPROJECTIONELEMENT" />
            <xs:enumeration value="IFCPROTECTIVEDEVICE" />
            <xs:enumeration value="IFCPROTECTIVEDEVICETRIPPINGUNIT" />
            <xs:enumeration value="IFCPUMP" />
            <xs:enumeration value="IFCRAILING" />
            <xs:enumeration value="IFCRAMP" />
            <xs:enumeration value="IFCRAMPFLIGHT" />
            <xs:enumeration value="IFCREINFORCINGBAR" />
            <xs:enumeration value="IFCREINFORCINGMESH" />
            <xs:enumeration value="IFCROOF" />
            <xs:enumeration value="IFCSANITARYTERMINAL" />
            <xs:enumeration value="IFCSENSOR" />
            <xs:enumeration value="IFCSHADINGDEVICE" />
            <xs:enumeration value="IFCSLAB" />
            <xs:enumeration value="IFCSOLARDEVICE" />
            <xs:enumeration value="IFCSPACEHEATER" />
            <xs:enumeration value="IFCSTACKTERMINAL" />
            <xs:enumeration value="IFCSTAIR" />
            <xs:enumeration value="IFCSTAIRFLIGHT" />
            <xs:enumeration value="IFCSURFACEFEATURE" />
            <xs:enumeration value="IFCSWITCHINGDEVICE" />
            <xs:enumeration value="IFCSYSTEMFURNITUREELEME" />
            <xs:enumeration value="IFCTANK" />
            <xs:enumeration value="IFCTENDON" />
            <xs:enumeration value="IFCTENDONANCHOR" />
            <xs:enumeration value="IFCTRANSFORMER" />
            <xs:enumeration value="IFCTRANSPORTELEMENT" />
            <xs:enumeration value="IFCTUBEBUNDLE" />
            <xs:enumeration value="IFCUNITARYCONTROLELEMENT" />
            <xs:enumeration value="IFCUNITARYEQUIPMENT" />
            <xs:enumeration value="IFCVALVE" />
            <xs:enumeration value="IFCVIBRATIONISOLATOR" />
            <xs:enumeration value="IFCVIRTUALELEMENT" />
            <xs:enumeration value="IFCVOIDINGFEATURE" />
            <xs:enumeration value="IFCWALL" />
            <xs:enumeration value="IFCWASTETERMINAL" />
            <xs:enumeration value="IFCWINDOW" />
        </xs:restriction>
    </ids:name>
</ids:entity>
```
</details>

**IFC2X3におけるカンマ区切りのIfcElementサブエンティティ：**
```
IFCELEMENT,IFCBUILDINGELEMENT,IFCBUILDINGELEMENTPROXY,IFCCOVERING,IFCBEAM,IFCCOLUMN,IFCCURTAINWALL,IFCDOOR,IFCMEMBER,IFCRAILING,IFCRAMP,IFCRAMPFLIGHT,IFCWALL,IFCSLAB,IFCSTAIRFLIGHT,IFCWINDOW,IFCSTAIR,IFCROOF,IFCPILE,IFCFOOTING,IFCBUILDINGELEMENTCOMPONENT,IFCPLATE,IFCFURNISHINGELEMENT,IFCDISTRIBUTIONELEMENT,IFCDISTRIBUTIONFLOWELEMENT,IFCFLOWFITTING,IFCFLOWSEGMENT,IFCFLOWCONTROLLER,IFCFLOWTERMINAL,IFCFLOWMOVINGDEVICE,IFCENERGYCONVERSIONDEVICE,IFCFLOWSTORAGEDEVICE,IFCFLOWTREATMENTDEVICE,IFCDISTRIBUTIONCHAMBERELEMENT,IFCDISTRIBUTIONCONTROLELEMENT,IFCTRANSPORTELEMENT,IFCEQUIPMENTELEMENT,IFCFEATUREELEMENT,IFCFEATUREELEMENTADDITION,IFCPROJECTIONELEMENT,IFCFEATUREELEMENTSUBTRACTION,IFCOPENINGELEMENT,IFCELEMENTASSEMBLY,IFCVIRTUALELEMENT
```

<details><summary>✂️  IfcElement subentities in IFC2X3 as IDS entity facet</summary>

```
<ids:entity>
    <ids:name>
        <xs:restriction base="xs:string">
            <xs:enumeration value="IFCELEMENT" />
            <xs:enumeration value="IFCBUILDINGELEMENT" />
            <xs:enumeration value="IFCBUILDINGELEMENTPROXY" />
            <xs:enumeration value="IFCCOVERING" />
            <xs:enumeration value="IFCBEAM" />
            <xs:enumeration value="IFCCOLUMN" />
            <xs:enumeration value="IFCCURTAINWALL" />
            <xs:enumeration value="IFCDOOR" />
            <xs:enumeration value="IFCMEMBER" />
            <xs:enumeration value="IFCRAILING" />
            <xs:enumeration value="IFCRAMP" />
            <xs:enumeration value="IFCRAMPFLIGHT" />
            <xs:enumeration value="IFCWALL" />
            <xs:enumeration value="IFCSLAB" />
            <xs:enumeration value="IFCSTAIRFLIGHT" />
            <xs:enumeration value="IFCWINDOW" />
            <xs:enumeration value="IFCSTAIR" />
            <xs:enumeration value="IFCROOF" />
            <xs:enumeration value="IFCPILE" />
            <xs:enumeration value="IFCFOOTING" />
            <xs:enumeration value="IFCBUILDINGELEMENTCOMPONENT" />
            <xs:enumeration value="IFCPLATE" />
            <xs:enumeration value="IFCFURNISHINGELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONFLOWELEMENT" />
            <xs:enumeration value="IFCFLOWFITTING" />
            <xs:enumeration value="IFCFLOWSEGMENT" />
            <xs:enumeration value="IFCFLOWCONTROLLER" />
            <xs:enumeration value="IFCFLOWTERMINAL" />
            <xs:enumeration value="IFCFLOWMOVINGDEVICE" />
            <xs:enumeration value="IFCENERGYCONVERSIONDEVICE" />
            <xs:enumeration value="IFCFLOWSTORAGEDEVICE" />
            <xs:enumeration value="IFCFLOWTREATMENTDEVICE" />
            <xs:enumeration value="IFCDISTRIBUTIONCHAMBERELEMENT" />
            <xs:enumeration value="IFCDISTRIBUTIONCONTROLELEMENT" />
            <xs:enumeration value="IFCTRANSPORTELEMENT" />
            <xs:enumeration value="IFCEQUIPMENTELEMENT" />
            <xs:enumeration value="IFCFEATUREELEMENT" />
            <xs:enumeration value="IFCFEATUREELEMENTADDITION" />
            <xs:enumeration value="IFCPROJECTIONELEMENT" />
            <xs:enumeration value="IFCFEATUREELEMENTSUBTRACTION" />
            <xs:enumeration value="IFCOPENINGELEMENT" />
            <xs:enumeration value="IFCELEMENTASSEMBLY" />
            <xs:enumeration value="IFCVIRTUALELEMENT" />
        </xs:restriction>
    </ids:name>
</ids:entity>
```
</details>
