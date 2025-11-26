# 情報配信仕様書
<img src="Graphics/IDS-logo-with-letters.png" alt="IDS Logo" width="300"/>

**情報提供仕様（IDS**）は、IFC モデルから単純な情報要求を指定し、チェックするためのbuildingSMART標準である。モデル・チェックのための、自由で軽量、標準化されたアプローチとして設計されている。詳しくは[公式ウェブサイトを](https://www.buildingsmart.org/standards/bsi-standards/information-delivery-specification-ids/)ご覧ください。

## はじめに
IDSは、情報**仕様の**リストを含む`.ids` で終わるファイル形式である。例えば、1つの**仕様**書には、"*すべての壁に耐火等級プロパティが必要で*"あると記載されている場合があります。IDSファイルを受け取ったモデル作成者は、**各仕様に**必要な情報がすべて提供されていることを確認するために、IDSファイルを使用することができます。モデルの受信者は、IDSファイルを使用して、IFC モデルがすべての**仕様を満たして**いるかどうかを確認することができます。また、**仕様**準拠チェックの結果を一覧表示するレポートを作成することもできます。

![IDS Diagram](Graphics/ids-diagram.png)

IDSファイル作成ツールとモデルチェックツールは、多くの[ソフトウェアベンダーから](https://technical.buildingsmart.org/ids-software-implementations/)提供されています。どのソフトウェアから作成されたIFC モデルでも、IDS ファイルと照合することができます。

## IDSの構造
各IDSファイルは[メタデータで](ids-metadata.md)記述することができ、1つ以上の[仕様を](specifications.md)含むことができる。仕様は、適用可能性（applicability） - この仕様の対象となる要素を記述する部分と、要件（requirements） - 適用可能な要素が持つべきもの、または持つべきでないものを列挙する部分の2つで構成される。適用可能性も要件も、プロパティ、エンティティ、クラシフィケーション、マテリアル、パートオブなどのファセットで構築されます。

## 始め方
 1. IDSチェックをサポートするソフトウェアを選択する（[IDSをサポートするツールのリストを](https://technical.buildingsmart.org/ids-software-implementations/)参照）。

 1. [IDSファイルのサンプルを](../Examples/IDS_wooden-windows.ids)ダウンロードする。

 1. IDSと照合するための[IFCサンプルモデルを](../Examples/IDS_wooden-windows_IFC.ifc)ダウンロードしてください。

 1. IDSとIFC の両方をソフトウェアにロードし、チェック・プロセスを開始する。

 1. すべての不適合の報告書を入手すべきである。

以上です！その他、サンプルIDSファイルは、[Examplesに](../Examples)あります。ヘルプが必要な場合は、[buildingSMARTフォーラムに](https://forums.buildingsmart.org/)お気軽にお問い合わせください。

## IDS についてもっと知る
 1. [ **仕様の**仕組み](specifications.md)

 1. [優れた**仕様の**メタデータを指定するためのガイドライン](ids-metadata.md)

 1. [ **複雑な制限を**指定する方法を学ぶ](restrictions.md)

 1. [ **エンティティ・ファセットの**使い方](entity-facet.md)

 1. [ **アトリビュート・ファセットの**使い方を学ぶ](attribute-facet.md)

 1. [ **クラシフィケーション・ファセットの**使い方を学ぶ](classification-facet.md)

 1. [ **プロパティ・ファセットの**使用方法を学ぶ](property-facet.md)

 1. [ **マテリアルファセットの**使い方を学ぶ](material-facet.md)

 1. [ **パートオブファセットの**使い方](partof-facet.md)

 1. [ソフトウェア開発者ですか？開発者ガイドをお読みください！](../ImplementersDocumentation/developer-guide.md)
