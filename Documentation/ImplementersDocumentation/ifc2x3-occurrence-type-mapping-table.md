# IFC2X3 エンティティマッピング
以下の表は、IFC2X3 モデル・サブセットの識別をチェックするためのすべての特別なケースのリストである。

最初の列は、IDSエンティティ・ファセットで使用される名前を示す。  
2列目と3列目は、IFC2X3 エンティティとタイプのペアにマッチするプロパティを定義する。

| IDS<nobr>ファ</nobr>セットの名前 | <nobr>発生</nobr>エンティティ   | タイプ・<nobr>エンティティ</nobr> |
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
たとえば、IDS適用可能ファセットをエンティティ `IfcFilter`を持つIDS適用可能性ファセットを定義すると `IfcFlowTreatmentDevice`タイプ `IfcFilterType`.

同様に、エンティティ名 `IfcFilter`を持つ要件の定義は、エンティティタイプが `IfcFlowTreatmentDevice`と異なる場合、またはその型が `IfcFilterType`.

## 備考
これらの合意の歴史は[116号で](https://github.com/buildingSMART/IDS/issues/116)辿ることができる。
