# IDSのユニット
数値メジャー値は、SI単位を使用してIDSファイルで表されます。

IFC モデルが検証される場合、その値は比較の前にデフォルト単位に変換される必要がある。

次の表に、変換が必要なメジャーと、変換プロセスをサポートするメタデータを示します。  
IFC Defined typesの完全なリストは、IFC ドキュメントにある。

次元指数単位のオーダーは`(m, kg, s, A, K, mol, cd)` である。

| Ifc <nobr>定義された</nobr>型名 | 物理量の<nobr>説明</nobr>      | <nobr>単位</nobr> | 単位<nobr>記号</nobr> | <nobr>デフォルト</nobr>表示 | <nobr>次元</nobr>指数        | 単位<nobr>列挙</nobr>        | <nobr>IfcSIUnitName</nobr>列挙 |
| --------------------------------------------- | --------------------------------------- | ------------ | ----------- | --------------- | ----------------------- | ---------------------------------------------------------- | -------------------------------------------------- |
| IFCABSORBEDDOSEMEASURE | 吸収放射能量　 | 灰色　　　　　 | Gy　　　　　 | J / kg　 | (2, 0, -2, 0, 0, 0, 0)　　　　　　 | IfcUnitEnum.ABSORBEDDOSEUNIT | IfcSIUnitName.GRAY |
| IFCACCELERATIONMEASURE | 加速 |  |  | m / s2 | (1, 0, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.ACCELERATIONUNIT |  |
| IFCAMOUNTOFSUBSTANCEMEASURE | 物質量 | モル | mol | mol | (0, 0, 0, 0, 0, 1, 0) | IfcUnitEnum.AMOUNTOFSUBSTANCEUNIT | IfcSIUnitName.MOLE |
| IFCANGULARVELOCITYMEASURE | 角速度 |  |  | rad / s | (0, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.ANGULARVELOCITYUNIT |  |
| IFCAREADENSITYMEASURE | 面積密度 |  |  | kg / m2 | (-2, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.AREADENSITYUNIT |  |
| IFCAREAMEASURE | エリア | 平方メートル |  | m2 | (2, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.AREAUNIT | IfcSIUnitName.SQUARE_METRE |
| IFCCURVATUREMEASURE | 曲率 |  |  | rad / m | (-1, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.CURVATUREUNIT |  |
| IFCDOSEEQUIVALENTMEASURE | 投与量に相当する | シーベルト | Sv | J / kg | (2, 0, -2, 0, 0, 0, 0) | IfcUnitEnum.DOSEEQUIVALENTUNIT | IfcSIUnitName.SIEVERT |
| IFCDYNAMICVISCOSITYMEASURE | 動的粘度 |  |  | Pa s | (-1, 1, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.DYNAMICVISCOSITYUNIT |  |
| IFCELECTRICCAPACITANCEMEASURE | 電気容量 | ファラド | F | F | (-2, 1, 4, 1, 0, 0, 0) | IfcUnitEnum.ELECTRICCAPACITANCEUNIT | IfcSIUnitName.FARAD |
| IFCELECTRICCHARGEMEASURE | 電荷 | クーロン | C | C | (0, 0, 1, 1, 0, 0, 0) | IfcUnitEnum.ELECTRICCHARGEUNIT | IfcSIUnitName.COULOMB |
| IFCELECTRICCONDUCTANCEMEASURE | 電気コンダクタンス | ジーメンス | S | S | (-2, -1, 3, 2, 0, 0, 0) | IfcUnitEnum.ELECTRICCONDUCTANCEUNIT | IfcSIUnitName.SIEMENS |
| IFCELECTRICCURRENTMEASURE | 電流 | アンペア | A | A | (0, 0, 0, 1, 0, 0, 0) | IfcUnitEnum.ELECTRICCURRENTUNIT | IfcSIUnitName.AMPERE |
| IFCELECTRICRESISTANCEMEASURE | 電気抵抗 | オーム | Ω | Ω | (2, 1, -3, -2, 0, 0, 0) | IfcUnitEnum.ELECTRICRESISTANCEUNIT | IfcSIUnitName.OHM |
| IFCELECTRICVOLTAGEMEASURE | 電圧 | ボルト | V | V | (2, 1, -3, -1, 0, 0, 0) | IfcUnitEnum.ELECTRICVOLTAGEUNIT | IfcSIUnitName.VOLT |
| IFCENERGYMEASURE | エネルギー | ジュール | J | J | (2, 1, -2, 0, 0, 0, 0) | IfcUnitEnum.ENERGYUNIT | IfcSIUnitName.JOULE |
| IFCFORCEMEASURE | フォース | ニュートン | N | N | (1, 1, -2, 0, 0, 0, 0) | IfcUnitEnum.FORCEUNIT | IfcSIUnitName.NEWTON |
| IFCFREQUENCYMEASURE | 頻度 | ヘルツ | ヘルツ | ヘルツ | (0, 0, -1, 0, 0, 0, 0) | IfcUnitEnum.FREQUENCYUNIT | IfcSIUnitName.HERTZ |
| IFCHEATFLUXDENSITYMEASURE | 熱流束密度 |  |  | W / m2 | (0, 1, -3, 0, 0, 0, 0) | IfcDerivedUnitEnum.HEATFLUXDENSITYUNIT |  |
| IFCHEATINGVALUEMEASURE | 暖房 |  |  | J / K | (2, 1, -2, 0, -1, 0, 0) | IfcDerivedUnitEnum.HEATINGVALUEUNIT |  |
| IFCILLUMINANCEMEASURE | 照度 | ルクス | lx | lx | (-2, 0, 0, 0, 0, 0, 1) | IfcUnitEnum.ILLUMINANCEUNIT | IfcSIUnitName.LUX |
| IFCINDUCTANCEMEASURE | インダクタンス | ヘンリー | H | Wb / A | (2, 1, -2, -2, 0, 0, 0) | IfcUnitEnum.INDUCTANCEUNIT | IfcSIUnitName.HENRY |
| IFCINTEGERCOUNTRATEMEASURE | カウント率 |  |  | 1 / s | (0, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.INTEGERCOUNTRATEUNIT |  |
| IFCIONCONCENTRATIONMEASURE | イオン濃度測定 |  |  | mol / m3 | (-3, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.IONCONCENTRATIONUNIT |  |
| IFCISOTHERMALMOISTURECAPACITYMEASURE | 磯熱水分率 |  |  | m3 / kg | (3, -1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.ISOTHERMALMOISTURECAPACITYUNIT |  |
| IFCKINEMATICVISCOSITYMEASURE | 動粘度 |  |  | m2 / s | (2, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.KINEMATICVISCOSITYUNIT |  |
| IFCLENGTHMEASURE | 長さ | メーター | m | m | (1, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.LENGTHUNIT | IfcSIUnitName.METRE |
| IFCLINEARFORCEMEASURE | 直線力 |  |  | N / m | (0, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARFORCEUNIT |  |
| IFCLINEARMOMENTMEASURE | 線形モーメント |  |  | N m / m | (1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARMOMENTUNIT |  |
| IFCLINEARSTIFFNESSMEASURE | 線形剛性 |  |  | N / m | (0, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARSTIFFNESSUNIT |  |
| IFCLINEARVELOCITYMEASURE | スピード |  |  | m / s | (1, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARVELOCITYUNIT |  |
| IFCLUMINOUSFLUXMEASURE | 光束 | 内腔 | lm | lm | (0, 0, 0, 0, 0, 0, 1) | IfcUnitEnum.LUMINOUSFLUXUNIT | IfcSIUnitName.LUMEN |
| IFCLUMINOUSINTENSITYDISTRIBUTIONMEASURE | 光度分布 |  |  | cd / lm | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.LUMINOUSINTENSITYDISTRIBUTIONUNIT |  |
| IFCLUMINOUSINTENSITYMEASURE | 光度 | カンデラ | cd | cd | (0, 0, 0, 0, 0, 0, 1) | IfcUnitEnum.LUMINOUSINTENSITYUNIT | IfcSIUnitName.CANDELA |
| IFCMAGNETICFLUXDENSITYMEASURE | 磁束密度 | テスラ | T | Wb / m2 | (0, 1, -2, -1, 0, 0, 0) | IfcUnitEnum.MAGNETICFLUXDENSITYUNIT | IfcSIUnitName.TESLA |
| IFCMAGNETICFLUXMEASURE | 磁束 | ウェーバー | Wb | Wb | (2, 1, -2, -1, 0, 0, 0) | IfcDerivedUnitEnum.MAGNETICFLUXUNIT | IfcSIUnitName.WEBER |
| IFCMASSDENSITYMEASURE | 質量密度 |  |  | kg / m3 | (-3, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.MASSDENSITYUNIT |  |
| IFCMASSFLOWRATEMEASURE | 質量流量 |  |  | kg / s | (0, 1, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.MASSFLOWRATEUNIT |  |
| IFCMASSMEASURE | 質量 | キログラム | kg | kg | (0, 1, 0, 0, 0, 0, 0) | IfcUnitEnum.MASSUNIT | IfcSIUnitName.GRAM |
| IFCMASSPERLENGTHMEASURE | 長さあたりの質量 |  |  | kg / m | (-1, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.MASSPERLENGTHUNIT |  |
| IFCMODULUSOFELASTICITYMEASURE | 弾性係数 |  |  | N / m2 | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.MODULUSOFELASTICITYUNIT |  |
| IFCMODULUSOFLINEARSUBGRADEREACTIONMEASURE | 線形地盤反力係数 |  |  | N / m2 | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.MODULUSOFLINEARSUBGRADEREACTIONUNIT |  |
| IFCMODULUSOFROTATIONALSUBGRADEREACTIONMEASURE | 回転地盤反力係数 |  |  | N m / m rad | (1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.MODULUSOFROTATIONALSUBGRADEREACTIONUNIT |  |
| IFCMODULUSOFSUBGRADEREACTIONMEASURE | 地盤反力係数 |  |  | N / m3 | (-2, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.MODULUSOFSUBGRADEREACTIONUNIT |  |
| IFCMOISTUREDIFFUSIVITYMEASURE | 水分拡散率 |  |  | m3 / s | (3, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.MOISTUREDIFFUSIVITYUNIT |  |
| IFCMOLECULARWEIGHTMEASURE | 分子量 |  |  | kg / mol | (0, 1, 0, 0, 0, -1, 0) | IfcDerivedUnitEnum.MOLECULARWEIGHTUNIT |  |
| IFCMOMENTOFINERTIAMEASURE | 慣性モーメント |  |  | m4 | (4, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.MOMENTOFINERTIAUNIT |  |
| IFCNONNEGATIVELENGTHMEASURE | 非負の長さ | メーター | m | m | (1, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.LENGTHUNIT | IfcSIUnitName.METRE |
| IFCPHMEASURE | pH |  | pH | pH | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.PHUNIT |  |
| IFCPLANARFORCEMEASURE | 平面力 | パスカル | Pa | Pa | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.PLANARFORCEUNIT | IfcSIUnitName.PASCAL |
| IFCPLANEANGLEMEASURE | アングル | ラジアン | rad | rad | (0, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.PLANEANGLEUNIT | IfcSIUnitName.RADIAN |
| IFCPOSITIVELENGTHMEASURE | 正の長さ | メーター | m | m | (1, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.LENGTHUNIT | IfcSIUnitName.METRE |
| IFCPOSITIVEPLANEANGLEMEASURE | 正の平面角 | ラジアン | rad | rad | (0, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.PLANEANGLEUNIT | IfcSIUnitName.RADIAN |
| IFCPOWERMEASURE | パワー | ワット | W | W | (2, 1, -3, 0, 0, 0, 0) | IfcUnitEnum.POWERUNIT | IfcSIUnitName.WATT |
| IFCPRESSUREMEASURE | 圧力 | パスカル | Pa | Pa | (-1, 1, -2, 0, 0, 0, 0) | IfcUnitEnum.PRESSUREUNIT | IfcSIUnitName.PASCAL |
| IFCRADIOACTIVITYMEASURE | ラジオ活動 | ベクレル | Bq | Bq | (0, 0, -1, 0, 0, 0, 0) | IfcUnitEnum.RADIOACTIVITYUNIT | IfcSIUnitName.BECQUEREL |
| IFCROTATIONALFREQUENCYMEASURE | 回転数 | ヘルツ | ヘルツ | ヘルツ | (0, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.ROTATIONALFREQUENCYUNIT | IfcSIUnitName.HERTZ |
| IFCROTATIONALMASSMEASURE | 回転質量 |  |  | kg m2 | (2, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.ROTATIONALMASSUNIT |  |
| IFCROTATIONALSTIFFNESSMEASURE | 回転剛性 |  |  | N m / rad | (2, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.ROTATIONALSTIFFNESSUNIT |  |
| IFCSECTIONALAREAINTEGRALMEASURE | 区間積分 |  |  | m5 | (5, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.SECTIONALAREAINTEGRALUNIT |  |
| IFCSECTIONMODULUSMEASURE | 断面係数 |  |  | m3 | (3, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.SECTIONMODULUSUNIT |  |
| IFCSHEARMODULUSMEASURE | せん断弾性率 |  |  | N / m2 | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.SHEARMODULUSUNIT |  |
| IFCSOLIDANGLEMEASURE | ソリッドアングル | ステラジアン | sr | sr | (0, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.SOLIDANGLEUNIT | IfcSIUnitName.STERADIAN |
| IFCSOUNDPOWERLEVELMEASURE | 音響パワーレベル（対数基準 1e-12 W） | デシベルSWL | db | db | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPOWERLEVELUNIT |  |
| IFCSOUNDPOWERMEASURE | 音響パワー | ワット | W | W | (2, 1, -3, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPOWERUNIT |  |
| IFCSOUNDPRESSURELEVELMEASURE | 音圧レベル（対数基準 2e-5 Pa） | デシベルSPL | db | db | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPRESSURELEVELUNIT |  |
| IFCSOUNDPRESSUREMEASURE | 音圧 | パスカル | Pa | Pa | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPRESSUREUNIT |  |
| IFCSPECIFICHEATCAPACITYMEASURE | 比熱容量 |  |  | J / kg K | (2, 0, -2, 0, -1, 0, 0) | IfcDerivedUnitEnum.SPECIFICHEATCAPACITYUNIT |  |
| IFCTEMPERATUREGRADIENTMEASURE | 温度勾配 |  |  | K / m | (-1, 0, 0, 0, 1, 0, 0) | IfcDerivedUnitEnum.TEMPERATUREGRADIENTUNIT |  |
| IFCTEMPERATURERATEOFCHANGEMEASURE | 温度変化率 |  |  | K / s | (0, 0, -1, 0, 1, 0, 0) | IfcDerivedUnitEnum.TEMPERATURERATEOFCHANGEUNIT |  |
| IFCTHERMALADMITTANCEMEASURE | 熱アドミタンス |  |  | W / m2 K | (0, 1, -3, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALADMITTANCEUNIT |  |
| IFCTHERMALCONDUCTIVITYMEASURE | 熱伝導率 |  |  | W / m K | (1, 1, -3, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALCONDUCTANCEUNIT |  |
| IFCTHERMALEXPANSIONCOEFFICIENTMEASURE | 熱膨張係数 |  |  | 1 / K | (0, 0, 0, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALEXPANSIONCOEFFICIENTUNIT |  |
| IFCTHERMALRESISTANCEMEASURE | 熱抵抗 |  |  | m2 K / W | (0, -1, 3, 0, 1, 0, 0) | IfcDerivedUnitEnum.THERMALRESISTANCEUNIT |  |
| IFCTHERMALTRANSMITTANCEMEASURE | 熱貫流率 |  |  | W / m2 K | (0, 1, -3, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALTRANSMITTANCEUNIT |  |
| IFCTHERMODYNAMICTEMPERATUREMEASURE | 温度 | ケルビン | °K | °K | (0, 0, 0, 0, 1, 0, 0) | IfcUnitEnum.THERMODYNAMICTEMPERATUREUNIT | IfcSIUnitName.KELVIN IfcSIUnitName 。DEGREE_CELSIUS |
| IFCTIMEMEASURE | 時間 | セカンド | s | s | (0, 0, 1, 0, 0, 0, 0) | IfcUnitEnum.TIMEUNIT | IfcSIUnitName.SECOND |
| IFCTORQUEMEASURE | トルク |  |  | N m | (2, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.TORQUEUNIT |  |
| IFCVAPORPERMEABILITYMEASURE | 蒸気透過性 |  |  | kg / s m Pa | (0, 0, 1, 0, 0, 0, 0) | IfcDerivedUnitEnum.VAPORPERMEABILITYUNIT |  |
| IFCVOLUMEMEASURE | ボリューム | 立方メートル |  | m3 | (3, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.VOLUMEUNIT | IfcSIUnitName.CUBIC_METRE |
| IFCVOLUMETRICFLOWRATEMEASURE | 容積流量 |  |  | m3 / s | (3, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.VOLUMETRICFLOWRATEUNIT |  |
| IFCWARPINGCONSTANTMEASURE | ワープ定数 |  |  | m6 | (6, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.WARPINGCONSTANTUNIT |  |
| IFCWARPINGMOMENTMEASURE | ワープする瞬間 |  |  | N m2 | (3, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.WARPINGMOMENTUNIT |  |

## 寸法単位
各次元指数は、デフォルトのSI単位を参照する。

| <nobr>次元</nobr>指数リストにおける位置 | <nobr>物理</nobr>量      | SI<nobr>単位</nobr> |
| ------------------------------------------ | ----------------- | ------------------------- |
| 1　　　　　　 | 長さ　　　　　 | メートル　　　 |
| 2 | 質量 | キログラム |
| 3 | 時間 | セカンド |
| 4 | アンペア | 電流 |
| 5 | ケルビン | 熱力学温度 |
| 6 | モル | 物質量 |
| 7 | カンデラ | 光度 |

## 例
ソフトウェアでは通常、値はローカル単位で表示される。次の表は、ユーザーに対して物事がどのように表現され、IDSではどのように表現されるかの例をいくつか示したものである。

| ユーザーの<nobr>視点</nobr>     | IDS<nobr>値</nobr> | <nobr>物理</nobr>量      |
| ---------------- | ---------- | ----------------- |
| 10 mm　　 | 0.01　　　 | 長さ　　　　　 |
| 1 | 0.0254 | 長さ |
| 1 kW | 1000 | パワー |
| 1ポンド | 0.45359237 | 質量 |
| 20 C | 293.15 | 温度 |
