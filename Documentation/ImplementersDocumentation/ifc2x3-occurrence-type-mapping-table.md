# IFC2X3エニシティ・マッピング
次の表は、IFC2X3モデルのサブセットの識別をチェックするためのすべての特別なケースをリストしたものです。

最初の列は、IDSエンティティ・ファセットで使用される名前を示す。  
2列目と3列目は、一致するIFC2X3エンティティとタイプのペアのプロパティを定義します。

| IDSファセットの名前 | 発生主体 | タイプ・エンティティ |
| ---------------------------- | ----------------------------- | -------------------------------- |
| IfcFurniture | IfcFurnishingElement | IfcFurnitureType |
| IfcSystemFurnitureElement | IfcFurnishingElement | IfcSystemFurnitureElementType |
| IfcActuator | IfcDistributionControlElement | IfcActuatorType |
| IfcAlarm | IfcDistributionControlElement | IfcAlarmType |
| IfcController | IfcDistributionControlElement | IfcControllerType |
| IfcFlowInstrument | IfcDistributionControlElement | IfcFlowInstrumentType |
| IfcSensor | IfcDistributionControlElement | IfcSensorType |
| IfcAirToAirHeatRecovery | IfcEnergyConversionDevice | IfcAirToAirHeatRecoveryType |
| IfcBoiler | IfcEnergyConversionDevice | IfcBoilerType |
| IfcChiller | IfcEnergyConversionDevice | IfcChillerType |
| IfcCoil | IfcEnergyConversionDevice | IfcCoilType |
| IfcCondenser | IfcEnergyConversionDevice | IfcCondenserType |
| IfcCooledBeam | IfcEnergyConversionDevice | IfcCooledBeamType |
| IfcCoolingTower | IfcEnergyConversionDevice | IfcCoolingTowerType |
| IfcElectricGenerator | IfcEnergyConversionDevice | IfcElectricGeneratorType |
| IfcElectricMotor | IfcEnergyConversionDevice | IfcElectricMotorType |
| IfcEvaporativeCooler | IfcEnergyConversionDevice | IfcEvaporativeCoolerType |
| IfcEvaporator | IfcEnergyConversionDevice | IfcEvaporatorType |
| IfcHeatExchanger | IfcEnergyConversionDevice | IfcHeatExchangerType |
| IfcHumidifier | IfcEnergyConversionDevice | IfcHumidifierType |
| IfcMotorConnection | IfcEnergyConversionDevice | IfcMotorConnectionType |
| IfcTransformer | IfcEnergyConversionDevice | IfcTransformerType |
| IfcTubeBundle | IfcEnergyConversionDevice | IfcTubeBundleType |
| IfcUnitaryEquipment | IfcEnergyConversionDevice | IfcUnitaryEquipmentType |
| IfcAirTerminalBox | IfcFlowController | IfcAirTerminalBoxType |
| IfcDamper | IfcFlowController | IfcDamperType |
| IfcElectricTimeControl | IfcFlowController | IfcElectricTimeControlType |
| IfcFlowMeter | IfcFlowController | IfcFlowMeterType |
| IfcProtectiveDevice | IfcFlowController | IfcProtectiveDeviceType |
| IfcSwitchingDevice | IfcFlowController | IfcSwitchingDeviceType |
| IfcValve | IfcFlowController | IfcValveType |
| IfcCableCarrierFitting | IfcFlowFitting | IfcCableCarrierFittingType |
| IfcDuctFitting | IfcFlowFitting | IfcDuctFittingType |
| IfcJunctionBox | IfcFlowFitting | IfcJunctionBoxType |
| IfcPipeFitting | IfcFlowFitting | IfcPipeFittingType |
| IfcCompressor | IfcFlowMovingDevice | IfcCompressorType |
| IfcFan | IfcFlowMovingDevice | IfcFanType |
| IfcPump | IfcFlowMovingDevice | IfcPumpType |
| IfcCableCarrierSegment | IfcFlowSegment | IfcCableCarrierSegmentType |
| IfcCableSegment | IfcFlowSegment | IfcCableSegmentType |
| IfcDuctSegment | IfcFlowSegment | IfcDuctSegmentType |
| IfcPipeSegment | IfcFlowSegment | IfcPipeSegmentType |
| IfcElectricFlowStorageDevice | IfcFlowStorageDevice | IfcElectricFlowStorageDeviceType |
| IfcTank | IfcFlowStorageDevice | IfcTankType |
| IfcAirTerminal | IfcFlowTerminal | IfcAirTerminalType |
| IfcElectricAppliance | IfcFlowTerminal | IfcElectricApplianceType |
| IfcFireSuppressionTerminal | IfcFlowTerminal | IfcFireSuppressionTerminalType |
| IfcLamp | IfcFlowTerminal | IfcLampType |
| IfcLightFixture | IfcFlowTerminal | IfcLightFixtureType |
| IfcOutlet | IfcFlowTerminal | IfcOutletType |
| IfcSanitaryTerminal | IfcFlowTerminal | IfcSanitaryTerminalType |
| IfcSpaceHeater | IfcFlowTerminal | IfcSpaceHeaterType |
| IfcStackTerminal | IfcFlowTerminal | IfcStackTerminalType |
| IfcWasteTerminal | IfcFlowTerminal | IfcWasteTerminalType |
| IfcDuctSilencer | IfcFlowTreatmentDevice | IfcDuctSilencerType |
| IfcFilter | IfcFlowTreatmentDevice | IfcFilterType |
| IfcVibrationIsolator | IfcElementComponent | IfcVibrationIsolatorType |

## 例
例えば、エンティティ `IfcFilter`持つIDS適用可能ファセットを定義すると、`IfcFilterType`に関連付けられたすべての `IfcFlowTreatmentDevice`の特定を結果として識別します。 

同様に、エンティティ名 `IfcFilter`持つ要件の定義は、エンティティ・タイプが `IfcFlowTreatmentDevice`と異なるか、またはその型が `IfcFilterType`.

## 備考
これらの合意の歴史は[116号で](https://github.com/buildingSMART/IDS/issues/116)辿ることができる。
