# 情報配信仕様書
<img src="Graphics/IDS-logo-with-letters.png" alt="IDS Logo" width="300"/>

**情報提供仕様（IDS**）は、IFCモデルから単純な情報要件を指定し、チェックするためのbuildingSMART標準です。モデル・チェックのための自由で軽量、標準化されたアプローチとして設計されています。詳細は[公式ウェブサイトを](https://www.buildingsmart.org/standards/bsi-standards/information-delivery-specification-ids/)ご覧ください。

## はじめに
IDSは、情報**仕様の**リストを含む`.ids` で終わるファイル形式である。例えば、1つの**仕様**書に*「すべての壁には耐火等級プロパティが必要である*」と記載されている場合があります。IDSファイルを受け取ったモデル作成者は、**各仕様に**必要な情報がすべて提供されていることを確認するために、IDSファイルを使用することができます。モデルの受信者は、IDSファイルを使用して、IFCモデルがすべての**仕様を満たして**いるかどうかを確認できます。また、**仕様**準拠チェックの結果を一覧にしたレポートを作成することもできます。

![IDS Diagram](Graphics/ids-diagram.png)

IDSファイル作成ツールとモデルチェックツールは、多くの[ソフトウェアベンダーから](https://technical.buildingsmart.org/ids-software-implementations/)提供されています。どのソフトウェアから作成されたIFCモデルでも、IDSファイルと照合することができます。

## IDSの構造
各IDSファイルは[メタデータで](ids-metadata.md)記述することができ、1つ以上の[仕様を](specifications.md)含むことができる。仕様は、適用可能性（applicability） - どの要素がこの仕様の対象となるかを記述する部分と、要件（requirements） - 適用可能な要素が持つべきもの、または持つべきでないものを列挙する部分の2つで構成される。適用可能性も要件も、プロパティ、エンティティ、クラシフィケーション、マテリアル、パートオブなどのファセットで構築されます。

## 始め方
 1. IDSチェックをサポートするソフトウェアを選択する（[IDSをサポートするツールのリストを](https://technical.buildingsmart.org/ids-software-implementations/)参照）。

 1. [IDSファイルのサンプルを](../Examples/IDS_wooden-windows.ids)ダウンロードする。

 1. [IFCモデルのサンプルを](../Examples/IDS_wooden-windows_IFC.ifc)ダウンロードして、IDSと照合してください。

 1. IDSとIFCの両方をソフトウェアにロードし、チェック・プロセスを開始する。

 1. すべての不適合の報告書を入手すべきである。

以上です！その他、サンプルIDSファイルは、[Examplesに](../Examples)あります。ヘルプが必要な場合は、[buildingSMARTフォーラムに](https://forums.buildingsmart.org/)お気軽にお問い合わせください。

## IDS についてもっと知る
 1. [ **スペックの**仕組み](specifications.md)

 1. [優れた**仕様の**メタデータを指定するためのガイドライン](ids-metadata.md)

 1. [ **複雑な制限を**指定する方法を学ぶ](restrictions.md)

 1. [ **エンティティ・ファセットの**使い方](entity-facet.md)

 1. [ **アトリビュート・ファセットの**使い方を学ぶ](attribute-facet.md)

 1. [ **クラシフィケーション・ファセットの**使い方を学ぶ](classification-facet.md)

 1. [ **プロパティ・ファセットの**使用方法を学ぶ](property-facet.md)

 1. [ **マテリアルファセットの**使い方を学ぶ](material-facet.md)

 1. [ **パートオブファセットの**使い方](partof-facet.md)

 1. [ソフトウェア開発者ですか？開発者ガイドをお読みください！](../ImplementersDocumentation/developer-guide.md)
