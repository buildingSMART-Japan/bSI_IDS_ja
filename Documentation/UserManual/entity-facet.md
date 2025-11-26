# エンティティ・ファセット
IFC モデル内のすべてのインスタンスは、"IFC クラス"（EXPRESS エンティティとしても知られる）を持つ。例えば、壁のインスタンスはIFC クラスIfcWall を持ち、ドアのインスタンスはIFC クラスIfcDoor を持つ。個々の建物要素を表さないインスタンスもクラスを持ちます。例えば、プロジェクトはクラスIfcProject を持ち、窓タイプはクラスIfcWindowType を持ち、コスト項目はクラスIfcCostItem を持ちます。

クラスはインスタンスを分類するためだけのものではない。クラスは、どのような種類のプロパティや関係を持つことができるかを示すものでもある。例えば、IfcWall クラスのインスタンスは耐火等級プロパティを持つことができますが、IfcGrid のインスタンスは持つことができません。

仕様書を作成する上で最も重要なことの1つは、その仕様書が適切なIFC クラスに適用されることを確認することです。通常、すべての**仕様**書には、**適用**セクションで使用される**エンティティ・ファセットが**あります。

IFC スキーマのバージョン間にはクラスの違いがあります。最近のIFC スキーマには、より豊富で多様なIFC クラスが含まれています：

- [IFC4X3_ADD2 IFC クラス名一覧](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/annex-b1.html)
- [IFC4 IFC クラス名一覧](https://standards.buildingsmart.org/IFC/RELEASE/IFC4/ADD2_TC1/HTML/link/alphabeticalorder-entities.htm)
- [IFC2X3 IFC クラス名一覧](https://standards.buildingsmart.org/IFC/RELEASE/IFC2x3/TC1/HTML/alphabeticalorder_entities.htm)

いくつかのクラスは、オプションで「**定義済みタイプ**」を持つこともできる。これは、IFC Class**Name（**クラス**名**）に加えて、さらなるレベルの分類です。例えば、IfcWall のインスタンスは、SHEAR または PARTITIONING の**Predefined Type**を持つことができる。IFC Class**Nameが** IFC 標準によって指定されるのに対し、**Predefined Typeは**標準によって指定されるだけでなく、ユーザーによって定義されたカスタム値を含むこともできます。[ IFC Predefined Typeの使い方については](#ifc-predefined-types)、以下をご覧ください。

## パラメータ
| <nobr>パラメータ</nobr>     | <nobr>必須</nobr>       | <nobr>制限</nobr>あり         | <nobr>意味</nobr> |
| -------------------------------------- | -------- | -------------------- | ------------------------------------------------------------------------------------------------------------- |
| **氏名**(`name`) | ✔️　　　　　 | ✔️　　　　　 | IFC スキーマの有効なIFC クラス。IFC クラスは正確に一致しなければならない。大文字で表現します。 |
| **定義済みタイプ**(`predefinedType`) | ❌ | ✔️ | IFC スキーマの有効な定義済みタイプ、または任意のカスタム・テキスト値。Predefined Typeは正確に一致しなければならない。大文字で表現する。 |

## エンティティ・ファセットの解釈
### 適用性
| <nobr>団体</nobr>名 | エンティティ<nobr>定義済み</nobr>タイプ | IDSの<nobr>解釈</nobr>         |
| ----------- | ---------------------- | ------------------------------------------------------- |
| IFCWINDOW | -　　　　　　 | すべての事業体に適用される。 *IfcWindow*すべての事業体に適用されます。 |
| IFCWINDOW | スカイライト | すべての *IfcWindow*タイプのすべてのエンティティに適用される。 |

### 必要条件
| IDS<nobr>カーディナリティ</nobr> | <nobr>団体</nobr>名 | エンティティ<nobr>定義済み</nobr>タイプ | <nobr>コンフィギュレーションを</nobr>許可しますか？ | IDSの<nobr>解釈</nobr>         |
| --------------- | ----------- | ---------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------- |
| 必須　　　　　 | IFCWINDOW | -　　　　　　 | ✅　　　　　　 | 該当するオブジェクトは、IFCWINDOW のエンティティでなければならない。 |
| 必須 | IFCWINDOW | スカイライト | ✅ | 適用可能なオブジェクトは、エンティティIFCWINDOW 、定義済みのタイプSKYLIGHTでなければならない。 |
| オプション | IFCWINDOW |  | ❌ | オプションは意味をなさない。 |
| オプション | IFCWINDOW | スカイライト | ✅ | 該当するオブジェクトがIFCWINDOW エンティティの場合、SKYLIGHTの定義済みタイプも持っていなければならない。 |
| 禁止 | IFCWINDOW |  | ✅ | 適用されるオブジェクトは、IFCWINDOW エンティティであることはできない。 |
| 禁止 | IFCWINDOW | スカイライト | ✅ | 適用可能なオブジェクトは、IFCWINDOW （またはそれ以外）のエンティティにすることができますが、SKYLIGHTの定義済みタイプである場合はできません。 |

## IFC 定義済みタイプ
IFC スキーマ・ドキュメントには、標準的な定義済み型のリストが含まれています。以下は、スキーマで有効な**定義済み**型のリストを見つける方法です。 IFC4X3_ADD2スキーマで有効な定義済み型のリストを見つける方法を示します。この手順は、すべてのIFC バージョンで同様です。

 1. 指定するIFC クラスのドキュメント・ページを参照する。上記のIFC クラス名の一覧からアクセスできます。例えば、[これはIfcWall のドキュメント・ページ](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWall.htm)です。

 1. ドキュメントの**Attributes**セクションまでスクロールダウンし、**PredefinedType**属性を見つけてください。

 1. **PredefinedType**属性の隣にある列挙リンクをクリックすると、有効な値のリストが表示されます。例えば、IfcWall の場合、リンクをクリックすると、[ IfcWallTypeEnum のドキュメントが](http://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcWallTypeEnum.htm)表示されます。

 1. 有効な**定義済み型の**リストは表に示されている。

**定義済みタイプが**必要な場合は、標準のリストから選択することを強く推奨する。しかし、プロジェクトに適用されない場合は、任意のカスタム値を指定することができます。

### IFC ファイルの`predefinedType` を識別するためのロジック：
- **IF**: [オブジェクトが](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm) [型によって](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)定義されている（relationshipを探す [IfcRelDefinesByType](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcRelDefinesByType.htm)関係)
  - **IF**: [型オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)、値`USERDEFINED` ➡️✅を持つ`PredefinedType` 。事前定義された型の値は、その[型オブジェクトの](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm) `ElementType` 属性にある。
  - **ELSE IF**:その[型オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)、`USERDEFINED` ➡️ ✅以外の値を持つ`PredefinedType` を持つ。事前定義された型の値は、その[型オブジェクトの](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm) `PredefinedType` 属性にある。
  - **ELSE**: [型オブジェクトが](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcTypeObject.htm)定義済みの型を定義していない。⬇️
- **ELSE**：
  - **IF：** `ObjectType` [オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm)、値`USERDEFINED` ➡️ を持つ`PredefinedType` を持つ。
  - **ELSE IF**: [オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm) `USERDEFINED` 以外の値を持つ`PredefinedType` を持つ ➡️ ✅ 定義済みの型の値は、その[オブジェクトの](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm) `PredefinedType` 属性にある。
  - **ELSE**: [オブジェクトは](https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcObject.htm)定義済みの型を持たない。🔚

### IFC 定義済みタイプの使用例
| IDS<nobr>エンティティ</nobr> | IDS<nobr>定義済み</nobr>タイプ | IFC <nobr>エンティティ</nobr> | IFC <nobr>定義済み</nobr>タイプ | IFC <nobr>要素/オブジェクトの</nobr>タイプ | <nobr>IFCxIDS</nobr>結果 |
| ---------- | ------------------- | ---------- | ------------------- | ----------------------- | -------------- |
| IFCWALL | ユーザー定義　 | IFCWALL | ユーザー定義　 | -　　　　　　 | ✅　　　　　　 |
| IFCWALL | ユーザー定義 | IFCWALL | ユーザー定義 | FOO | ✅ |
| IFCWALL | FOO | IFCWALL | ユーザー定義 | FOO | ✅ |
| IFCWALL | FOO | IFCWALL | FOO | - | ✅ |


## 特別なケースIFC2X3
IFC2X3 のいくつかの出現エンティティは、そのタイプオブジェクトによってさらに指定される。  
この定義は、IfcFlowTerminal の出現インスタンスと、IfcAirTerminalType の型インスタンスによって、IFC2X3 でエンコードされている。  
エンティティ・ファセットには、タイプ・エンティティ名をさらに指定するパラメータがない。  
この場合、IDSはIFC4 で紹介されている慣例に従う。  
指定された例では、チェックされるエンティティの**名前は** IfcAirTerminal （タイプなし）でなければならず、指定されたマッピングテーブルによって解決されなければならない。  
全リストはこの[表に](./Documentation/ImplementersDocumentation/ifc2x3-occurrence-type-mapping-table.md)ある。

## 継承
IDS のエンティティ・ファセット解釈には、自動継承はない。つまり、すべてのエンティティを明示的に列挙する必要がある。これにより、正確で曖昧さのない仕様が可能になる。

たとえば、すべてのIfcElement オブジェクトに適用される要件を作成するには、IfcWall やIfcDoor など、すべてのIfcElement サブエンティティをリストする必要があります。また、IfcElement は抽象エンティティであり、インスタンス化できないため、モデルには表示されない。

ユーザーやソフトウェア実装者が、IfcElement 、IfcBuiltElement 、IfcFlowSegment などのよく使われるサブエンティティをすべて指定できるように、以下の表を用意した。

### IfcElement IFC 、異なるバージョンのサブ・エンティティ
|  | <nobr>IFC2X3</nobr> | <nobr>IFC4</nobr> | <nobr>IFC4X3</nobr> |
|-----------------------------------------------------|--------|------|--------|
| IfcElement | ⚠️　　　　　 | ⚠️　　　　　 | ⚠️　　　　　 |
| ── IfcBuildingElement | ⚠️ | ⚠️ |  |
| ── IfcBuiltElement |  |  | ✅ |
| ──── IfcBeam | ✅ | ✅ | ✅ |
| ────── IfcBeamStandardCase |  | 🚫 | 🚫 |
| ──── IfcBearing |  |  | ✅ |
| ──── IfcBuildingElementProxy | ✅ | ✅ | ✅ |
| ──── IfcChimney |  | ✅ | ✅ |
| ──── IfcColumn | ✅ | ✅ | ✅ |
| ──────   IfcColumnStandardCase |  | 🚫 |  |
| ──── IfcCourse |  |  | ✅ |
| ──── IfcCovering | ✅ | ✅ | ✅ |
| ──── IfcCurtainWall | ✅ | ✅ | ✅ |
| ──── IfcDeepFoundation |  |  | ✅ |
| ────── IfcCaissonFoundation |  |  | ✅ |
| ────── IfcPile | ✅ | ✅ | ✅ |
| ──── IfcDoor | ✅ | ✅ | ✅ |
| ────── IfcDoorStandardCase |  | 🚫 |  |
| ──── IfcEarthworksElement |  |  | ✅ |
| ────── IfcEarthworksFill |  |  | ✅ |
| ────── IfcReinforcedSoil |  |  | ✅ |
| ──── IfcFooting | ✅ | ✅ | ✅ |
| ──── IfcKerb |  |  | ✅ |
| ──── IfcMember | ✅ | ✅ | ✅ |
| ──────   IfcMemberStandardCase |  | 🚫 |  |
| ──── IfcMooringDevice |  |  | ✅ |
| ──── IfcNavigationElement |  |  | ✅ |
| ──── IfcPavement |  |  | ✅ |
| ──── IfcPlate | ✅ | ✅ | ✅ |
| ────── IfcPlateStandardCase |  | 🚫 |  |
| ──── IfcRail |  |  | ✅ |
| ──── IfcRailing | ✅ | ✅ | ✅ |
| ──── IfcRamp | ✅ | ✅ | ✅ |
| ──── IfcRampFlight | ✅ | ✅ | ✅ |
| ──── IfcRoof | ✅ | ✅ | ✅ |
| ──── IfcShadingDevice |  | ✅ | ✅ |
| ──── IfcSlab | ✅ | ✅ | ✅ |
| ────── IfcSlabElementedCase |  | 🚫 |  |
| ────── IfcSlabStandardCase |  | 🚫 |  |
| ──── IfcStair | ✅ | ✅ | ✅ |
| ──── IfcStairFlight | ✅ | ✅ | ✅ |
| ──── IfcTrackElement |  |  | ✅ |
| ──── IfcWall | ✅ | ✅ | ✅ |
| ────── IfcWallElementedCase |  | 🚫 |  |
| ────── IfcWallStandardCase |  | 🚫 | 🚫 |
| ──── IfcWindow | ✅ | ✅ | ✅ |
| ──────   IfcWindowStandardCase |  | 🚫 |  |
| ── IfcDistributionElement | ✅ | ✅ | ✅ |
| ────   IfcDistributionFlowElement | ✅ | ✅ | ✅ |
| ──────   IfcEnergyConversionDevice | ⚠️ | ✅ |  |
| ──────── IfcCoolingTower |  | ✅ | ✅ |
| ────────   IfcAirToAirHeatRecovery | ✅ | ✅ |  |
| ──────── IfcBoiler |  | ✅ | ✅ |
| ──────── IfcBurner |  | ✅ | ✅ |
| ──────── IfcChiller |  | ✅ | ✅ |
| ──────── IfcCoil |  | ✅ | ✅ |
| ──────── IfcCondenser |  | ✅ | ✅ |
| ──────── IfcCooledBeam |  | ✅ | ✅ |
| ────────   IfcElectricGenerator |  | ✅ | ✅ |
| ──────── IfcElectricMotor |  | ✅ | ✅ |
| ──────── IfcEngine |  | ✅ | ✅ |
| ────────   IfcEvaporativeCooler | ✅ | ✅ |  |
| ──────── IfcEvaporator |  | ✅ | ✅ |
| ──────── IfcHeatExchanger |  | ✅ | ✅ |
| ──────── IfcHumidifier |  | ✅ | ✅ |
| ────────   IfcMotorConnection |  | ✅ | ✅ |
| ──────── IfcSolarDevice |  | ✅ | ✅ |
| ──────── IfcTransformer |  | ✅ | ✅ |
| ──────── IfcTubeBundle |  | ✅ | ✅ |
| ────────   IfcUnitaryEquipment | ✅ | ✅ |  |
| ──────   IfcDistributionChamberElement | ✅ | ✅ |  |
| ────── IfcFlowController | ✅ | ⚠️ | ✅ |
| ──────── IfcAirTerminalBox |  | ✅ | ✅ |
| ──────── IfcDamper |  | ✅ | ✅ |
| ────────   IfcDistributionBoard |  |  | ✅ |
| ────────   IfcElectricDistributionBoard | ✅ | 🚫 | 🚫 |
| ────────   IfcElectricTimeControl | ✅ | ✅ |  |
| ──────── IfcFlowMeter |  | ✅ | ✅ |
| ────────   IfcProtectiveDevice |  | ✅ | ✅ |
| ────────   IfcSwitchingDevice |  | ✅ | ✅ |
| ──────── IfcValve |  | ✅ | ✅ |
| ────── IfcFlowFitting | ✅ | ⚠️ | ✅ |
| ────────   IfcCableCarrierFitting | ✅ | ✅ |  |
| ──────── IfcCableFitting |  | ✅ | ✅ |
| ──────── IfcDuctFitting |  | ✅ | ✅ |
| ──────── IfcJunctionBox |  | ✅ | ✅ |
| ──────── IfcPipeFitting |  | ✅ | ✅ |
| ────── IfcFlowMovingDevice | ✅ | ⚠️ | ✅ |
| ──────── IfcCompressor |  | ✅ | ✅ |
| ──────── IfcFan |  | ✅ | ✅ |
| ──────── IfcPump |  | ✅ | ✅ |
| ────── IfcFlowSegment | ✅ | ⚠️ | ✅ |
| ────────   IfcCableCarrierSegment | ✅ | ✅ |  |
| ──────── IfcCableSegment |  | ✅ | ✅ |
| ────────   IfcConveyorSegment |  | ✅ |  |
| ──────── IfcDuctSegment |  | ✅ | ✅ |
| ──────── IfcPipeSegment |  | ✅ | ✅ |
| ────── IfcFlowStorageDevice | ✅ | ⚠️ | ✅ |
| ────────   IfcElectricFlowStorageDevice | ✅ | ✅ |  |
| ──────── IfcTank |  | ✅ | ✅ |
| ────── IfcFlowTerminal | ✅ | ⚠️ | ✅ |
| ──────── IfcAirTerminal |  | ✅ | ✅ |
| ────────   IfcAudioVisualAppliance | ✅ | ✅ |  |
| ────────   IfcCommunicationsAppliance | ✅ | ✅ |  |
| ────────   IfcElectricAppliance |  | ✅ | ✅ |
| ────────   IfcFireSuppressionTerminal | ✅ | ✅ |  |
| ──────── IfcLamp |  | ✅ | ✅ |
| ──────── IfcLightFixture |  | ✅ | ✅ |
| ──────── IfcLiquidTerminal |  |  | ✅ |
| ──────── IfcMedicalDevice |  | ✅ | ✅ |
| ────────   IfcMobileTelecommunicationsAppliance |  | ✅ |  |
| ──────── IfcOutlet |  | ✅ | ✅ |
| ────────   IfcSanitaryTerminal |  | ✅ | ✅ |
| ──────── IfcSignal |  |  | ✅ |
| ──────── IfcSpaceHeater |  | ✅ | ✅ |
| ──────── IfcStackTerminal |  | ✅ | ✅ |
| ──────── IfcWasteTerminal |  | ✅ | ✅ |
| ──────   IfcFlowTreatmentDevice | ✅ | ⚠️ | ✅ |
| ──────── IfcDuctSilencer |  | ✅ | ✅ |
| ────────   IfcElectricFlowTreatmentDevice |  | ✅ |  |
| ──────── IfcFilter |  | ✅ | ✅ |
| ──────── IfcInterceptor |  | ✅ | ✅ |
| ────   IfcDistributionControlElement | ✅ | ✅ | ✅ |
| ────── IfcActuator |  | ✅ | ✅ |
| ────── IfcAlarm |  | ✅ | ✅ |
| ────── IfcController |  | ✅ | ✅ |
| ────── IfcFlowInstrument |  | ✅ | ✅ |
| ──────   IfcProtectiveDeviceTrippingUnit | ✅ | ✅ |  |
| ────── IfcSensor |  | ✅ | ✅ |
| ──────   IfcUnitaryControlElement |  | ✅ | ✅ |
| ── IfcCivilElement |  | ✅ | 🚫 |
| ── IfcElementAssembly | ✅ | ✅ | ✅ |
| ──   IfcBuildingElementComponent | ✅ |  |  |
| ── IfcElementComponent |  | ⚠️ | ⚠️ |
| ──── IfcBuildingElementPart |  | ✅ | ✅ |
| ──── IfcDiscreteAccessory |  | ✅ | ✅ |
| ──── IfcFastener |  | ✅ | ✅ |
| ────   IfcImpactProtectionDevice |  |  | ✅ |
| ──── IfcMechanicalFastener |  | ✅ | ✅ |
| ──── IfcReinforcingElement |  | ⚠️ | ⚠️ |
| ────── IfcReinforcingBar |  | ✅ | ✅ |
| ────── IfcReinforcingMesh |  | ✅ | ✅ |
| ────── IfcTendon |  | ✅ | ✅ |
| ────── IfcTendonAnchor |  | ✅ | ✅ |
| ────── IfcTendonConduit |  |  | ✅ |
| ──── IfcSign |  |  | ✅ |
| ──── IfcVibrationDamper |  |  | ✅ |
| ──── IfcVibrationIsolator |  | ✅ | ✅ |
| ── IfcFeatureElement | ✅ | ⚠️ | ⚠️ |
| ────   IfcFeatureElementAddition | ✅ | ⚠️ | ⚠️ |
| ────── IfcProjectionElement | ✅ | ✅ | ✅ |
| ────   IfcFeatureElementSubtraction | ✅ | ⚠️ | ⚠️ |
| ────── IfcEarthworksCut |  |  | ✅ |
| ────── IfcOpeningElement | ✅ | ✅ | ✅ |
| ────── IfcVoidingFeature |  | ✅ | ✅ |
| ──── IfcSurfaceFeature |  | ✅ | ✅ |
| ── IfcFurnishingElement | ✅ | ✅ | ✅ |
| ──── IfcFurniture |  | ✅ | ✅ |
| ────   IfcSystemFurnitureElement |  | ✅ | ✅ |
| ── IfcGeographicElement |  | ✅ | ✅ |
| ── IfcGeotechnicalElement |  |  | ⚠️ |
| ──── IfcGeotechnicalAssembly |  |  | ⚠️ |
| ────── IfcBorehole |  |  | ✅ |
| ────── IfcGeomodel |  |  | ✅ |
| ────── IfcGeoslice |  |  | ✅ |
| ──── IfcGeotechnicalStratum |  |  | ✅ |
| ── IfcTransportationDevice |  |  | ⚠️ |
| ──── IfcTransportElement | ✅ | ✅ | ✅ |
| ──── IfcVehicle |  |  | ✅ |
| ── IfcVirtualElement | ✅ | ✅ | ✅ |
| ── IfcElectricalElement | 🚫 |  |  |
| ── IfcEquipmentElement | ✅ |  |  |

✅ - IFC バージョンに含まれる。  
⚠️ - 含まれているが抽象的。  
🚫 - 非推奨

### 異なるIFC バージョンにおけるIfcElement サブ・エンティティのリスト
以下に、IfcElement のサブエンティティのリストを、IDSファイルにコピーペーストしやすい形で示します。このリストには、わかりやすくするためにタイプオブジェクトは含まれていません。

**コンマで区切られたIfcElement のサブエンティティIFC4X3**：
```
IFCACTUATOR,IFCAIRTERMINAL,IFCAIRTERMINALBOX,IFCAIRTOAIRHEATRECOVERY,IFCALARM,IFCAUDIOVISUALAPPLIANCE,IFCBEAM,IFCBEARING,IFCBOILER,IFCBOREHOLE,IFCBUILDINGELEMENTPART,IFCBUILDINGELEMENTPROXY,IFCBUILTELEMENT,IFCBURNER,IFCCABLECARRIERFITTING,IFCCABLECARRIERSEGMENT,IFCCABLEFITTING,IFCCABLESEGMENT,IFCCAISSONFOUNDATION,IFCCHILLER,IFCCHIMNEY,IFCCOIL,IFCCOLUMN,IFCCOMMUNICATIONSAPPLIANCE,IFCCOMPRESSOR,IFCCONDENSER,IFCCONTROLLER,IFCCONVEYORSEGMENT,IFCCOOLEDBEAM,IFCCOOLINGTOWER,IFCCOURSE,IFCCOVERING,IFCCURTAINWALL,IFCDAMPER,IFCDEEPFOUNDATION,IFCDISCRETEACCESSORY,IFCDISTRIBUTIONBOARD,IFCDISTRIBUTIONCHAMBERELEMENT,IFCDISTRIBUTIONCONTROLELEMENT,IFCDISTRIBUTIONELEMENT,IFCDISTRIBUTIONFLOWELEMENT,IFCDOOR,IFCDUCTFITTING,IFCDUCTSEGMENT,IFCDUCTSILENCER,IFCEARTHWORKSCUT,IFCEARTHWORKSELEMENT,IFCEARTHWORKSFILL,IFCELECTRICAPPLIANCE,IFCELECTRICFLOWSTORAGEDEVICE,IFCELECTRICFLOWTREATMENTDEVICE,IFCELECTRICGENERATOR,IFCELECTRICMOTOR,IFCELECTRICTIMECONTROL,IFCELEMENTASSEMBLY,IFCENERGYCONVERSIONDEVICE,IFCENGINE,IFCEVAPORATIVECOOLER,IFCEVAPORATOR,IFCFAN,IFCFASTENER,IFCFILTER,IFCFIRESUPPRESSIONTERMINAL,IFCFLOWCONTROLLER,IFCFLOWFITTING,IFCFLOWINSTRUMENT,IFCFLOWMETER,IFCFLOWMOVINGDEVICE,IFCFLOWSEGMENT,IFCFLOWSTORAGEDEVICE,IFCFLOWTERMINAL,IFCFLOWTREATMENTDEVICE,IFCFOOTING,IFCFURNISHINGELEMENT,IFCFURNITURE,IFCGEOGRAPHICELEMENT,IFCGEOMODEL,IFCGEOSLICE,IFCGEOTECHNICALSTRATUM,IFCHEATEXCHANGER,IFCHUMIDIFIER,IFCIMPACTPROTECTIONDEVICE,IFCINTERCEPTOR,IFCJUNCTIONBOX,IFCKERB,IFCLAMP,IFCLIGHTFIXTURE,IFCLIQUIDTERMINAL,IFCMECHANICALFASTENER,IFCMEDICALDEVICE,IFCMEMBER,IFCMOBILETELECOMMUNICATIONSAPPLIANCE,IFCMOORINGDEVICE,IFCMOTORCONNECTION,IFCNAVIGATIONELEMENT,IFCOPENINGELEMENT,IFCOUTLET,IFCPAVEMENT,IFCPILE,IFCPIPEFITTING,IFCPIPESEGMENT,IFCPLATE,IFCPROJECTIONELEMENT,IFCPROTECTIVEDEVICE,IFCPROTECTIVEDEVICETRIPPINGUNIT,IFCPUMP,IFCRAIL,IFCRAILING,IFCRAMP,IFCRAMPFLIGHT,IFCREINFORCEDSOIL,IFCREINFORCINGBAR,IFCREINFORCINGMESH,IFCROOF,IFCSANITARYTERMINAL,IFCSENSOR,IFCSHADINGDEVICE,IFCSIGN,IFCSIGNAL,IFCSLAB,IFCSOLARDEVICE,IFCSPACEHEATER,IFCSTACKTERMINAL,IFCSTAIR,IFCSTAIRFLIGHT,IFCSURFACEFEATURE,IFCSWITCHINGDEVICE,IFCSYSTEMFURNITUREELEME,IFCTANK,IFCTENDON,IFCTENDONANCHOR,IFCTENDONCONDUIT,IFCTRACKELEMENT,IFCTRANSFORMER,IFCTRANSPORTELEMENT,IFCTUBEBUNDLE,IFCUNITARYCONTROLELEMENT,IFCUNITARYEQUIPMENT,IFCVALVE,IFCVEHICLE,IFCVIBRATIONDAMPER,IFCVIBRATIONISOLATOR,IFCVIRTUALELEMENT,IFCVOIDINGFEATURE,IFCWALL,IFCWASTETERMINAL,IFCWINDOW
```

<details><summary>✂️  IDS エンティティ・ファセットとしての IFC4X3 の IfcElement サブエンティティ。</summary>

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

**コンマで区切られたIfcElement のサブエンティティIFC4**：
```
IFCBEAM,IFCACTUATOR,IFCAIRTERMINAL,IFCAIRTERMINALBOX,IFCAIRTOAIRHEATRECOVERY,IFCALARM,IFCAUDIOVISUALAPPLIANCE,IFCBOILER,IFCBUILDINGELEMENTPART,IFCBUILDINGELEMENTPROXY,IFCBURNER,IFCCABLECARRIERFITTING,IFCCABLECARRIERSEGMENT,IFCCABLEFITTING,IFCCABLESEGMENT,IFCCHILLER,IFCCHIMNEY,IFCCIVILELEMENT,IFCCOIL,IFCCOLUMN,IFCCOMMUNICATIONSAPPLIANCE,IFCCOMPRESSOR,IFCCONDENSER,IFCCONTROLLER,IFCCOOLEDBEAM,IFCCOOLINGTOWER,IFCCOVERING,IFCCURTAINWALL,IFCDAMPER,IFCDISCRETEACCESSORY,IFCDISTRIBUTIONCHAMBERELEMENT,IFCDISTRIBUTIONCONTROLELEMENT,IFCDISTRIBUTIONELEMENT,IFCDISTRIBUTIONFLOWELEMENT,IFCDOOR,IFCDUCTFITTING,IFCDUCTSEGMENT,IFCDUCTSILENCER,IFCELECTRICAPPLIANCE,IFCELECTRICDISTRIBUTIONBOARD,IFCELECTRICFLOWSTORAGEDEVICE,IFCELECTRICGENERATOR,IFCELECTRICMOTOR,IFCELECTRICTIMECONTROL,IFCELEMENTASSEMBLY,IFCENGINE,IFCEVAPORATIVECOOLER,IFCEVAPORATOR,IFCFAN,IFCFASTENER,IFCFILTER,IFCFIRESUPPRESSIONTERMINAL,IFCFLOWINSTRUMENT,IFCFLOWMETER,IFCFOOTING,IFCFURNISHINGELEMENT,IFCFURNITURE,IFCGEOGRAPHICELEMENT,IFCHEATEXCHANGER,IFCHUMIDIFIER,IFCINTERCEPTOR,IFCJUNCTIONBOX,IFCLAMP,IFCLIGHTFIXTURE,IFCMECHANICALFASTENER,IFCMEDICALDEVICE,IFCMEMBER,IFCMOTORCONNECTION,IFCOPENINGELEMENT,IFCOUTLET,IFCPILE,IFCPIPEFITTING,IFCPIPESEGMENT,IFCPLATE,IFCPROJECTIONELEMENT,IFCPROTECTIVEDEVICE,IFCPROTECTIVEDEVICETRIPPINGUNIT,IFCPUMP,IFCRAILING,IFCRAMP,IFCRAMPFLIGHT,IFCREINFORCINGBAR,IFCREINFORCINGMESH,IFCROOF,IFCSANITARYTERMINAL,IFCSENSOR,IFCSHADINGDEVICE,IFCSLAB,IFCSOLARDEVICE,IFCSPACEHEATER,IFCSTACKTERMINAL,IFCSTAIR,IFCSTAIRFLIGHT,IFCSURFACEFEATURE,IFCSWITCHINGDEVICE,IFCSYSTEMFURNITUREELEME,IFCTANK,IFCTENDON,IFCTENDONANCHOR,IFCTRANSFORMER,IFCTRANSPORTELEMENT,IFCTUBEBUNDLE,IFCUNITARYCONTROLELEMENT,IFCUNITARYEQUIPMENT,IFCVALVE,IFCVIBRATIONISOLATOR,IFCVIRTUALELEMENT,IFCVOIDINGFEATURE,IFCWALL,IFCWASTETERMINAL,IFCWINDOW
```

<details><summary>✂️  IDS エンティティ・ファセットとして IFC4 内の IfcElement サブエンティティ</summary>

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

**コンマで区切られたIfcElement のサブエンティティIFC2X3**：
```
IFCELEMENT,IFCBUILDINGELEMENT,IFCBUILDINGELEMENTPROXY,IFCCOVERING,IFCBEAM,IFCCOLUMN,IFCCURTAINWALL,IFCDOOR,IFCMEMBER,IFCRAILING,IFCRAMP,IFCRAMPFLIGHT,IFCWALL,IFCSLAB,IFCSTAIRFLIGHT,IFCWINDOW,IFCSTAIR,IFCROOF,IFCPILE,IFCFOOTING,IFCBUILDINGELEMENTCOMPONENT,IFCPLATE,IFCFURNISHINGELEMENT,IFCDISTRIBUTIONELEMENT,IFCDISTRIBUTIONFLOWELEMENT,IFCFLOWFITTING,IFCFLOWSEGMENT,IFCFLOWCONTROLLER,IFCFLOWTERMINAL,IFCFLOWMOVINGDEVICE,IFCENERGYCONVERSIONDEVICE,IFCFLOWSTORAGEDEVICE,IFCFLOWTREATMENTDEVICE,IFCDISTRIBUTIONCHAMBERELEMENT,IFCDISTRIBUTIONCONTROLELEMENT,IFCTRANSPORTELEMENT,IFCEQUIPMENTELEMENT,IFCFEATUREELEMENT,IFCFEATUREELEMENTADDITION,IFCPROJECTIONELEMENT,IFCFEATUREELEMENTSUBTRACTION,IFCOPENINGELEMENT,IFCELEMENTASSEMBLY,IFCVIRTUALELEMENT
```

<details><summary>✂️  IDS エンティティ・ファセットとして IFC2X3 の IfcElement サブエンティティ。</summary>

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
