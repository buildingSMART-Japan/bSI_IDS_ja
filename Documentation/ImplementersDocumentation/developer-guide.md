# 開発者ガイド

IDSファイルは、XSDで定義されたスキーマを持つ、単なるXMLファイルです。 IDSがどのような構造になっているかを知るために、既存のIDSファイルを開き、その内容を検査することができます。

IDS は、XSD ベースの検証チェックに合格すれば有効であるとみなされます。 公開 IDS テンプレートの buildingSMART ディレクトリで利用可能なすべてのサンプル IDS ファイルは、有効であることが保証されています。

1. [最新のIDS XSDスキーマをダウンロードする](https://github.com/buildingSMART/IDS/blob/master/Development/ids.xsd)
2. IDSのサンプルファイルは`Documentation/ImplementersDocumentation/TestCases`リーフレット

XSDの検証を実行できる、自由に利用できるオンラインツールやプログラミングライブラリは数多くあります。
However, a valid IDS file requires more than bare XML schema compliance; buildingSMART provides an [IDS auditing tool](https://github.com/buildingSMART/IDS-Audit-tool/) to help ensure that the IDS files that you produce or receive are fully valid. The same tool is also available at [Xbim IDS auditing service](https://www.xbim.it/ids), which is executed locally in your web browser and does not upload your IDS files to any server.

## オーサリングIDS

IDSファイルの読み取りとオーサリングのみを行うソフトウェアを作成する場合、次のようになります。**マスト**は以下の基準を満たしている：

- すべての IDS ソフトウェアは、有効な IDS ファイルのみを読み書きしなければならない。 不正な IDS ファイルを読み込むためにリカバリが必要な場合は、その問題および自動リカバリ イベントをユーザーに通知する必要がある。
- IDSまたは関連するIFCモデルを補強するために補助システム（追加ロードメタデータなど）を使用する場合は、それがIDSの外部であることをユーザーに明確に示すべきである。
- IDSをロードし、IDSを保存する場合、IDSのすべての情報を保持しなければならない。 データが変更されない限り、構文のわずかな変更は許される。
- の中のxmlエンティティの順序を指定します。`xs:sequence`このxml機能の使用は、ファイル間のコンテンツの比較を簡単にすることを目的としている。

加えて、ユーザーには以下の機能も提供することを強く推奨する：

- IFCクラスを**エンティティ・ファセット**自動補完を推奨します。
- ユーザーが定義済みの型を**エンティティ・ファセット**しかし、ユーザーが定義済みのカスタム・タイプを記述できるようにする必要があります。 オートコンプリートを推奨します。
- ユーザーがすでに**エンティティ・ファセット**を作成している。**属性ファセット**インターフェースは、指定されたIFCクラスに基づいて許容値を制限する必要があります。 また、インターフェースは、指定された属性名に基づいて正しいデータ型を使用するようにユーザーをガイドする必要があります。
- ユーザーがすでに**エンティティ・ファセット**を作成している。**物件ファセット**しかし、ユーザがカスタムプロパティセットの名前を書くこともできるようにする必要があります。 標準化された（たとえば`Pset_`または`Qto_`)プロパティセットが指名された場合、あなたのインターフェイスは、使用可能なプロパティ名を制限し、使用すべき適切なデータ型を推奨すべきである。
- 文字列が**物件ファセット**IfcLabelはデフォルトのデータ型であることが望ましい。
- のカスタムプロパティに整数が指定されている場合**物件ファセット**デフォルトのデータ型はIfcIntegerであることが望ましい。
- のカスタムプロパティにfloatが指定されている場合。**物件ファセット**デフォルトのデータ型はIfcRealであることが望ましい。
- ユーザーが単位付きの値を指定する場合、変換ツールを提供し、ユーザーが希望する単位で IDS を記述できるようにする必要があります。
- また、スペルミスを防ぐために、一般的に知られているシステムの標準化された分類名と、分類リファレンスをあらかじめロードしておくこともできます。 これを使用することもできます。[分類システムのためのIFCディレクトリ](https://github.com/Moult/ifcclassification).
- ユーザーが**素材ファセット**あなたのインターフェースは、IFCが推奨する材料カテゴリー（「コンクリート」、「スチール」、「アルミニウム」、「ブロック」、「レンガ」、「石」、「木材」、「ガラス」、「石膏」、「プラスチック」、「土」のいずれか）を推奨する必要があります。
- 値を指定する場合、XML文字列（simpleValueと制限列挙の場合）は[正規表現](DataTypes.md#xml-base-types)で発表された。[DataType ドキュメント](DataTypes.md).

## IFCに対するIDSのチェック

IDSチェックを行うソフトウェア**マスト**で利用可能なIFC/IDSペアのテスト・スイートに準拠する。`Documentation/ImplementersDocumentation/TestCases`フォルダ ([テストケースの文書化](TestCases/scripts.md)).

加えて、ユーザーには以下の機能も提供することを強く推奨する：

- IDS の監査結果は BCF-XML 形式で保存されるか、BCF-API を介して OpenCDE に接続されることが意図されています。しかし、BCF でのこれらの結果のフォーマットと全体的な構造は、現在指定されていません。
- ソフトウェアがIDS仕様で指定されたIFCバージョンを解析できない場合は、ユーザーにその制限を知らせるべきである。
- 要件がオプションであるが、代わりに必須であれば失敗する場合、チェッカーツールはエラーを記録してはならないが、補助的な警告や推奨を提供することができる。

### 精密

浮動小数点値は数値と等価とみなされる。`x`の間にある場合（排他的）。`x * (1. - 1.e-6) - 1.e-6`そして`x * (1. + 1.e-6) + 1.e-6`.

これは、精度を小さな単位から大きな単位まで拡大できるようにするための妥協であり、単純化である。

### 制限事項

XSD には**合計桁数**そして**端数の桁数**これらは有用性が限られるため、IDSではサポートされない。

### オプション

仕様は次のように設定できる。**必須**,**オプション**あるいは**禁止**そのマッチングによって`applicability`モデル上
This is represented using XSD's `minOccurs` and `maxOccurs` functionality. They are represented by the following states:

| オプション | minOccurs | maxOccurs |
| ----------- | --------- | --------- |
| 必須 | 1 | 無制限 |
| オプション | 0 | 無制限 |
| 禁止 | 0 | 0 |

Other configurations of `minOccurs` and `maxOccurs` are currently not allowed.

## 利用可能な開発者ライブラリ

開発を始めるために、以下のものがあります。[IDSライブラリのディレクトリ](https://technical.buildingsmart.org/resources/software-implementations/)あなたのアプリケーションで使用することができます。

ご遠慮なく[ライブラリーを投稿する](https://technical.buildingsmart.org/resources/software-implementations/)(ログインが必要です）。

## もっと読む

- [ソフトウェアベンダーディレクトリに実装を追加する](https://technical.buildingsmart.org/resources/software-implementations/)
- [改善提案をする](https://github.com/buildingSMART/IDS/issues)
