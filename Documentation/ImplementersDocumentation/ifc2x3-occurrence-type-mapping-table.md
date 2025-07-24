# IFC2X3エニタリーマッピング

以下の表は、IFC2X3モデルのチェックに関するすべての特別なケースの一覧です。モデルのサブセットの識別は、タイプオブジェクトによってさらに制限されます。

最初の列は、IDSエンティティ・ファセットで使用される名前を示す。
The second and third columns define the properties of matching IFC2X3 entity and type pair.

| IDSファセットの名前 | 発生エンティティ | タイプ・エンティティ |
| ---------------------------- | ----------------------------- | -------------------------------- |
| Ifc家具 | IfcFurnishingElement | 家具タイプ |
| IfcSystemFurnitureElement | IfcFurnishingElement | IfcSystem家具要素タイプ |
| IfcActuator | IfcDistributionControl要素 | IfcActuatorType |
| IfcAlarm | IfcDistributionControl要素 | IfcAlarmType |
| IfcController | IfcDistributionControl要素 | IfcControllerType |
| IfcFlowInstrument | IfcDistributionControl要素 | IfcFlowInstrumentType |
| Ifcセンサー | IfcDistributionControl要素 | IfcSensorType |
| IfcAirToAirHeatRecovery | Ifcエネルギー変換装置 | IfcAirToAirHeatRecoveryタイプ |
| Ifcボイラー | Ifcエネルギー変換装置 | IfcBoilerType |
| イフチラー | Ifcエネルギー変換装置 | IfcChillerType |
| イフコイル | Ifcエネルギー変換装置 | コイルタイプ |
| イフコンデンサー | Ifcエネルギー変換装置 | IfcCondenserType |
| イフクールドビーム | Ifcエネルギー変換装置 | IfcCooledBeamType |
| 冷却塔 | Ifcエネルギー変換装置 | IfcCoolingTowerType |
| Ifc発電機 | Ifcエネルギー変換装置 | Ifc発電機タイプ |
| Ifc電気モーター | Ifcエネルギー変換装置 | Ifc電気モータータイプ |
| Ifc蒸発冷却器 | Ifcエネルギー変換装置 | Ifc蒸発冷却器タイプ |
| Ifcエバポレーター | Ifcエネルギー変換装置 | IfcEvaporatorType |
| Ifc熱交換器 | Ifcエネルギー変換装置 | IfcHeatExchangerType |
| IfcHumidify | Ifcエネルギー変換装置 | IfcHumidifierType |
| IfcMotorConnection | Ifcエネルギー変換装置 | IfcMotorConnectionType |
| IfcTransformer | Ifcエネルギー変換装置 | IfcTransformerType |
| IfcTubeバンドル | Ifcエネルギー変換装置 | IfcTubeBundleType |
| Ifcユニタリー機器 | Ifcエネルギー変換装置 | Ifcユニタリー機器タイプ |
| IfcAirTerminalBox | IfcFlowController | IfcAirTerminalBoxType |
| イフクダンパー | IfcFlowController | IfcDamperタイプ |
| Ifc電気時間制御 | IfcFlowController | Ifc電気時間制御タイプ |
| IfcFlowMeter | IfcFlowController | IfcFlowMeterType |
| IfcProtectiveDevice | IfcFlowController | IfcProtectiveDeviceType |
| IfcSwitchingDevice | IfcFlowController | IfcSwitchingDeviceType |
| Ifcバルブ | IfcFlowController | IfcValveType |
| ケーブルキャリアフィッティング | IfcFlowFitting | IfcCableCarrierFittingType（ケーブル・キャリア・フィッティング・タイプ |
| ダクト・フィッティング | IfcFlowFitting | ダクト・フィッティング・タイプ |
| Ifcジャンクションボックス | IfcFlowFitting | IfcJunctionBoxType |
| Ifcパイプフィッティング | IfcFlowFitting | IfcPipeFittingType |
| コンプレッサー | IfcFlowMovingDevice。 | IfcCompressorType |
| Ifcファン | IfcFlowMovingDevice。 | IfcFanType |
| Ifcポンプ | IfcFlowMovingDevice。 | IfcPumpType |
| IfcCableCarrierセグメント | IfcFlowSegment | IfcCableCarrierSegmentType（ケーブル・キャリア・セグメント・タイプ |
| IfcCableSegment | IfcFlowSegment | IfcCableSegmentType |
| IfcDuctセグメント | IfcFlowSegment | IfcDuctSegmentType |
| IfcPipeSegment | IfcFlowSegment | IfcPipeSegmentType |
| Ifc電気流体貯蔵装置 | IfcFlowStorageDevice | IfcElectricFlowStorageDeviceType。 |
| Ifcタンク | IfcFlowStorageDevice | Ifcタンクタイプ |
| IfcAirTerminal | IfcFlowTerminal | IfcAirTerminalType |
| IfcElectricアプライアンス | IfcFlowTerminal | IfcElectricApplianceType |
| Ifc火災抑制ターミナル | IfcFlowTerminal | IfcFireSuppressionターミナルタイプ |
| イフクランプ | IfcFlowTerminal | ランプタイプ |
| IfcLightFixture | IfcFlowTerminal | IfcLightFixtureType |
| Ifcアウトレット | IfcFlowTerminal | Ifcアウトレットタイプ |
| Ifcサニタリーターミナル | IfcFlowTerminal | IfcSanitaryTerminalType（サニタリーターミナルタイプ |
| Ifcスペースヒーター | IfcFlowTerminal | IfcSpaceHeaterType |
| Ifcスタックターミナル | IfcFlowTerminal | IfcStackTerminalType |
| IfcWasteターミナル | IfcFlowTerminal | IfcWasteTerminalType |
| ダクトサイレンサー | IfcFlowトリートメントデバイス | ダクトサイレンサータイプ |
| ifcFilter | IfcFlowトリートメントデバイス | IfcFilterType |
| IfcVibrationIsolator | IfcElementComponent | IfcVibrationIsolatorタイプ |

## Examples

例えば、IDS適用可能性ファセットの定義は、エンティティ`IfcFilter`その結果、すべての`IfcFlowTreatmentDevice`タイプに関連する`IfcFilterType`.

同様に、エンティティ名`IfcFilter`エンティティタイプが`IfcFlowTreatmentDevice`またはその型が`IfcFilterType`.

## 備考

この協定の歴史は、以下の記事で辿ることができる。[#116](https://github.com/buildingSMART/IDS/issues/116).
