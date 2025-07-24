# IDSのユニット

数値メジャー値は、SI単位を使用してIDSファイルで表されます。

IFCモデルが検証される場合、その値は比較の前にデフォルト単位に変換される必要がある。

次の表に、変換が必要なメジャーと、変換プロセスをサポートするメタデータを示します。
A full list of IFC Defined types can be found in the IFC documentation.

次元指数単位の順序は次のとおりである。`(m, kg, s, A, K, mol, cd)`.

| Ifc定義型名 | 物理量の説明 | 単位 | 単位記号 | デフォルト表示 | 次元指数 | 単位列挙 | IfcSIUnitName 列挙型 |
| --------------------------------------------- | --------------------------------------- | ------------ | ----------- | --------------- | ----------------------- | ---------------------------------------------------------- | -------------------------------------------------- |
| 吸収量測定 | 吸収放射能量 | 灰色 | Gy | J/kg | (2, 0, -2, 0, 0, 0, 0) | IfcUnitEnum.ABSORBEDDOSEUNIT | IfcSIUnitName.GRAY |
| ifcaccelerationmeasure | 加速 |  |  | m / s2 | (1, 0, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.ACCELERATIONUNIT。 |  |
| 物質量測定値 | 物質量 | モル | モル | モル | (0, 0, 0, 0, 0, 1, 0) | IfcUnitEnum.AMOUNTOFSUBSTANCEUNIT。 | ifcSIUnitName.MOLE |
| 角速度測定 | 角速度 |  |  | rad / s | (0, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.ANGULARVELOCITYUNIT。 |  |
| 強度測定 | 面積密度 |  |  | kg / m2 | (-2, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.AREADENSITYUNIT。 |  |
| IFCAREAMEASURE | エリア | 平方メートル |  | m2 | (2, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.AREAUNIT | ifcSIUnitName.SQUARE_METRE |
| 曲率測定 | カーブス |  |  | rad / m | (-1, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.CURVATUREUNIT。 |  |
| 等価測定 | 投与量に相当する | シーベルト | Sv | J/kg | (2, 0, -2, 0, 0, 0, 0) | IfcUnitEnum.DOSEEQUIVALENTUNIT | ifcSIUnitName.SIEVERT |
| 動粘度測定法 | 動的粘度 |  |  | パ | (-1, 1, -1, 0, 0, 0, 0) | ifcDerivedUnitEnum.DYNAMICVISCOSITYUNIT |  |
| キャパシタンス測定 | 電気容量 | ファラド | F | F | (-2, 1, 4, 1, 0, 0, 0) | IfcUnitEnum.ELECTRICCAPACITANCEUNIT | IfcSIUnitName.FARAD |
| 放電測定 | 電荷 | クーロン | C | C | (0, 0, 1, 1, 0, 0, 0) | IfcUnitEnum.ELECTRICCHARGEUNIT | IfcSIUnitName.COULOMB |
| 導電率測定 | 電気コンダクタンス | ジーメンス | S | S | (-2, -1, 3, 2, 0, 0, 0) | IfcUnitEnum.ELECTRICCONDUCTANCEUNIT。 | IfcSIUnitName.SIEMENS |
| 電流測定 | 電流 | アンペア | A | A | (0, 0, 0, 1, 0, 0, 0) | IfcUnitEnum.ELECTRICCURRENTUNIT | IfcSIUnitName.AMPERE |
| 電気抵抗測定 | 電気抵抗 | オーム | Ω | Ω | (2, 1, -3, -2, 0, 0, 0) | IfcUnitEnum.ELECTRICRESISTANCEUNIT | IfcSIUnitName.OHM |
| 電圧測定 | 電圧 | ボルト | V | V | (2, 1, -3, -1, 0, 0, 0) | IfcUnitEnum.ELECTRICVOLTAGEUNIT | IfcSIUnitName.VOLT |
| エネルギー測定 | エネルギー | ジュール | J | J | (2, 1, -2, 0, 0, 0, 0) | IfcUnitEnum.ENERGYUNIT | IfcSIUnitName.ジュール |
| イフフォースメジャー | フォース | ニュートン | N | N | (1, 1, -2, 0, 0, 0, 0) | IfcUnitEnum.FORCEUNIT | IfcSIUnitName.ニュートン |
| 周波数測定 | 頻度 | ヘルツ | ヘルツ | ヘルツ | (0, 0, -1, 0, 0, 0, 0) | IfcUnitEnum.FREQUENCYUNIT | IfcSIUnitName.HERTZ |
| 熱流束密度測定 | 熱流束密度 |  |  | W / m2 | (0, 1, -3, 0, 0, 0, 0) | IfcDerivedUnitEnum.HEATFLUXDENSITYUNIT。 |  |
| もしものときの計量 | 暖房 |  |  | J / K | (2, 1, -2, 0, -1, 0, 0) | IfcDerivedUnitEnum.HEATINGVALUEUNIT。 |  |
| 輝度測定 | 照度 | ルクス | lx | lx | (-2, 0, 0, 0, 0, 0, 1) | IfcUnitEnum.ILLUMINANCEUNIT | IfcSIUnitName.LUX |
| インダクタンス測定 | インダクタンス | ヘンリー | H | Wb / A | (2, 1, -2, -2, 0, 0, 0) | IfcUnitEnum.INDUCTANCEUNIT | IfcSIUnitName.ヘンリー |
| イフコンテジェカウントレートメジャー | カウント率 |  |  | 1 / s | (0, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.INTEGERCOUNTRATEUNIT。 |  |
| 濃度測定 | イオン濃度測定 |  |  | mol / m3 | (-3, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.IONCONCENTRATIONUNIT。 |  |
| 等温水分容量測定法 | 磯熱水分率 |  |  | m3 / kg | (3, -1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.ISOTHERMALMOISTURECAPACITYUNIT。 |  |
| イフキネマチック粘度計 | 動粘度 |  |  | m2 / s | (2, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.KINEMATICVISCOSITYUNIT。 |  |
| イフクロングスメジャー | 長さ | メーター | m | m | (1, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.LENGTHUNIT | IfcSIUnitName.METRE |
| イフクリニアフォースメジャー | 直線力 |  |  | N / m | (0, 1, -2, 0, 0, 0, 0) | ifcDerivedUnitEnum.LINEARFORCEUNIT |  |
| イフクリニアルモーメント測定 | 線形モーメント |  |  | N m/m | (1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARMOMENTUNIT。 |  |
| もし線形剛性測定 | 線形剛性 |  |  | N / m | (0, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARSTIFFNESSUNIT。 |  |
| もし直線速度測定 | スピード |  |  | m / s | (1, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.LINEARVELOCITYUNIT。 |  |
| 光束測定器 | 光束 | 内腔 | lm | lm | (0, 0, 0, 0, 0, 0, 1) | IfcUnitEnum.LUMINOUSFLUXUNIT。 | IfcSIUnitName.LUMEN |
| 輝度分布測定法 | 光度分布 |  |  | cd / lm | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.LUMINOUSINTENSITYDISTRIBUTIONUNIT。 |  |
| 輝度測定 | 光度 | カンデラ | cd | cd | (0, 0, 0, 0, 0, 0, 1) | IfcUnitEnum.LUMINOUSINTENSITYUNIT。 | IfcSIUnitName.CANDELA |
| 磁束密度測定 | 磁束密度 | テスラ | T | Wb/m2 | (0, 1, -2, -1, 0, 0, 0) | IfcUnitEnum.MAGNETICFLUXDENSITYUNIT。 | IfcSIUnitName.テスラ |
| 磁束測定 | 磁束 | ウェーバー | ウェッブ | ウェッブ | (2, 1, -2, -1, 0, 0, 0) | IfcDerivedUnitEnum.MAGNETICFLUXUNIT。 | IfcSIユニット名.WEBER |
| 質量密度測定 | 質量密度 |  |  | kg / m3 | (-3, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.MASSDENSITYUNIT。 |  |
| 流量測定 | 質量流量 |  |  | kg / s | (0, 1, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.MASSFLOWRATEUNIT。 |  |
| IFCMASSMEASURE | 質量 | キログラム | kg | kg | (0, 1, 0, 0, 0, 0, 0) | IfcUnitEnum.MASSUNIT | IfcSIUnitName.GRAM。 |
| 長さ測定 | 長さあたりの質量 |  |  | kg / m | (-1, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.MASSPERLENGTHUNIT。 |  |
| 弾性係数測定 | 弾性係数 |  |  | N / m2 | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.MODULUSOFELASTICITYUNIT。 |  |
| 線膨張係数の劣化反応測定法 | 線形地盤反力係数 |  |  | N / m2 | (-1, 1, -2, 0, 0, 0, 0) | ifcDerivedUnitEnum.MODULUSOFLINEARSUBGRADEREACTIONUNIT |  |
| 回転係数がグレードの反応測定値である場合 | 回転地盤反力係数 |  |  | N m / m rad | (1, 1, -2, 0, 0, 0, 0) | ifcDerivedUnitEnum.MODULUSOFROTATIONALSUBGRADEREACTIONUNIT。 |  |
| サブグレードの反応係数測定値 | 地盤反力係数 |  |  | N / m3 | (-2, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.MODULUSOFSUBGRADEREACTIONUNIT |  |
| ifcmoisturediffusivitymeasure（イフカモイスト・ディフュージビティ・メジャー | 水分拡散率 |  |  | m3 / s | (3, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.MOISTUREDIFFUSIVITYUNIT。 |  |
| 分子量測定 | 分子量 |  |  | kg / mol | (0, 1, 0, 0, 0, -1, 0) | IfcDerivedUnitEnum.MOLECULARWEIGHTUNIT。 |  |
| もし、そのようなことがあれば | 慣性モーメント |  |  | m4 | (4, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.MOMENTOFINERTIAUNIT。 |  |
| 負の長さ対策 | 非負の長さ | メーター | m | m | (1, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.LENGTHUNIT | IfcSIUnitName.METRE |
| IFCPHMEASURE | pH |  | pH | pH | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.PHUNIT。 |  |
| ifc平面力測定 | 平面力 | パスカル | パ | パ | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.PLANARFORCEUNIT。 | ifcSIUnitName.PASCAL |
| ifcplaneanglemeasure | アングル | ラジアン | ラド | ラド | (0, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.PLANEANGLEUNIT | IfcSIUnitName.RADIAN |
| ifcpositivelengthメジャー | 正の長さ | メーター | m | m | (1, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.LENGTHUNIT | IfcSIUnitName.METRE |
| IFC正平面角測定法 | 正の平面角 | ラジアン | ラド | ラド | (0, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.PLANEANGLEUNIT | IfcSIUnitName.RADIAN |
| IFCパワーメジャー | パワー | ワット | W | W | (2, 1, -3, 0, 0, 0, 0) | IfcUnitEnum.POWERUNIT | IfcSIUnitName.WATT |
| 圧力測定 | 圧力 | パスカル | パ | パ | (-1, 1, -2, 0, 0, 0, 0) | IfcUnitEnum.PRESSUREUNIT | ifcSIUnitName.PASCAL |
| 放射能測定 | ラジオ活動 | ベクレル | Bq | Bq | (0, 0, -1, 0, 0, 0, 0) | IfcUnitEnum.RADIOACTIVITYUNIT | ifcSIUnitName.BECQUEREL |
| 回転周波数測定 | 回転数 | ヘルツ | ヘルツ | ヘルツ | (0, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.ROTATIONALFREQUENCYUNIT。 | IfcSIUnitName.HERTZ |
| 回転質量測定 | 回転質量 |  |  | kg m2 | (2, 1, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.ROTATIONALMASSUNIT。 |  |
| 回転剛性測定 | 回転剛性 |  |  | N m / rad | (2, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.ROTATIONALSTIFFNESSUNIT。 |  |
| イフカセクショナルアインテグラルメジャー | 区間積分 |  |  | m5 | (5, 0, 0, 0, 0, 0, 0) | ifcDerivedUnitEnum.SECTIONALAREAINTEGRALUNIT |  |
| IFCセクションモジュラス測定 | 断面係数 |  |  | m3 | (3, 0, 0, 0, 0, 0, 0) | ifcDerivedUnitEnum.SECTIONMODULUSUNIT |  |
| 弾性係数測定 | せん断弾性率 |  |  | N / m2 | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.SHEARMODULUSUNIT。 |  |
| イフチ固体角測定 | ソリッドアングル | ステラジアン | むせん | むせん | (0, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.SOLIDANGLEUNIT | IfcSIUnitName.STERADIAN |
| 音圧レベル測定 | 音響パワーレベル（対数基準 1e-12 W） | デシベルSWL | デブ | デブ | (0, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPOWERLEVELUNIT |  |
| 音響パワー測定 | 音響パワー | ワット | W | W | (2, 1, -3, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPOWERUNIT |  |
| 音圧レベル測定 | 音圧レベル（対数基準 2e-5 Pa） | デシベルSPL | デブ | デブ | (0, 0, 0, 0, 0, 0, 0) | ifcDerivedUnitEnum.SOUNDPRESSURELEVELUNIT |  |
| 音圧測定 | 音圧 | パスカル | パ | パ | (-1, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.SOUNDPRESSUREUNIT |  |
| IFC別熱容量測定法 | 比熱容量 |  |  | J/kg K | (2, 0, -2, 0, -1, 0, 0) | IfcDerivedUnitEnum.SPECIFICHEATCAPACITYUNIT。 |  |
| 温度勾配測定 | 温度勾配 |  |  | K / m | (-1, 0, 0, 0, 1, 0, 0) | IfcDerivedUnitEnum.TEMPERATUREGRADIENTUNIT。 |  |
| 直流温度変化率測定器 | 温度変化率 |  |  | K / s | (0, 0, -1, 0, 1, 0, 0) | IfcDerivedUnitEnum.TEMPERATURERATEOFCHANGEUNIT。 |  |
| 熱貫流率測定法 | 熱アドミタンス |  |  | W / m2 K | (0, 1, -3, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALADMITTANCEUNIT。 |  |
| 熱伝導率測定 | 熱伝導率 |  |  | W / m K | (1, 1, -3, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALCONDUCTANCEUNIT。 |  |
| 熱膨張係数測定法 | 熱膨張係数 |  |  | 1 / K | (0, 0, 0, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALEXPANSIONCOEFFICIENTUNIT。 |  |
| 熱抵抗測定 | 熱抵抗 |  |  | m2 K / W | (0, -1, 3, 0, 1, 0, 0) | IfcDerivedUnitEnum.THERMALRESISTANCEUNIT。 |  |
| 熱貫流率測定 | 熱貫流率 |  |  | W / m2 K | (0, 1, -3, 0, -1, 0, 0) | IfcDerivedUnitEnum.THERMALTRANSMITTANCEUNIT。 |  |
| ifct熱力学温度測定 | 温度 | ケルビン | °K | °K | (0, 0, 0, 0, 1, 0, 0) | IfcUnitEnum.THERMODYNAMICTEMPERATUREUNIT。 | IfcSIUnitName.KELVIN, IfcSIUnitName.DEGREE_CELSIUS |
| IFCTIMEASURE | 時間 | セカンド | s | s | (0, 0, 1, 0, 0, 0, 0) | IfcUnitEnum.TIMEUNIT | IfcSIUnitName.SECOND |
| イクタクメジャー | トルク |  |  | N m | (2, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.TORQUEUNIT |  |
| 蒸気透過率測定 | 蒸気透過性 |  |  | kg/s m Pa | (0, 0, 1, 0, 0, 0, 0) | IfcDerivedUnitEnum.VAPORPERMEABILITYUNIT。 |  |
| 容積測定 | ボリューム | 立方メートル |  | m3 | (3, 0, 0, 0, 0, 0, 0) | IfcUnitEnum.VOLUMEUNIT | IfcSIUnitName.CUBIC_METRE |
| 容積流量計 | 容積流量 |  |  | m3 / s | (3, 0, -1, 0, 0, 0, 0) | IfcDerivedUnitEnum.VOLUMETRICFLOWRATEUNIT。 |  |
| 反り腰対策 | ワープ定数 |  |  | m6 | (6, 0, 0, 0, 0, 0, 0) | IfcDerivedUnitEnum.WARPINGCONSTANTUNIT。 |  |
| イフコンピューティングモーメント対策 | ワープする瞬間 |  |  | N m2 | (3, 1, -2, 0, 0, 0, 0) | IfcDerivedUnitEnum.WARPINGMOMENTUNIT。 |  |

## Dimensional units

各次元指数は、デフォルトのSI単位を参照する。

| 次元指数リストにおける位置 | 物理量 | SI単位 |
| ------------------------------------------ | ----------------- | ------------------------- |
| 1 | 長さ | メートル |
| 2 | 質量 | キログラム |
| 3 | 時間 | セカンド |
| 4 | アンペア | 電流 |
| 5 | ケルビン | 熱力学温度 |
| 6 | モル | 物質量 |
| 7 | カンデラ | 光度 |

## Examples

ソフトウェアでは通常、値はローカル単位で表示される。 次の表は、ユーザーに対して物事がどのように表現され、IDSではどのように表現されるかの例をいくつか示したものである。

| ユーザーの視点 | IDS値 | 物理量 |
| ---------------- | ---------- | ----------------- |
| 10 mm | 0.01 | 長さ |
| 1" | 0.0254 | 長さ |
| 1 kW | 1000 | パワー |
| 1ポンド | 0.45359237 | 質量 |
| 20 C | 293. | 温度 |

