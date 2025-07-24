# 情報配信仕様書

<img src="Graphics/IDS-logo-with-letters.png" alt="IDS Logo" width="300"/>

**情報デリバリー仕様書（IDS）**は、IFCモデルから単純な情報要件を指定し、チェックするためのbuildingSMART標準です。 これは、モデル・チェックのための自由で軽量、標準化されたアプローチとして設計されています。 詳細を読む[公式サイト](https://www.buildingsmart.org/standards/bsi-standards/information-delivery-specification-ids/).

## はじめに

IDSは`.ids`情報のリストを含む**仕様**例えば**仕様**と言うかもしれない。_すべての壁には耐火等級が必要_「IDSファイルを受け取ったモデル作成者は、各モデルに必要な情報がすべて提供されていることを確認するために、IDSファイルを使用することができる。**仕様**モデルの受信者は、IDSファイルを使用して、IFCモデルが以下のすべての条件を満たしているかどうかを確認することができます。**仕様**の結果を一覧にしたレポートも作成できる。**仕様**コンプライアンス・チェック

![IDSダイアグラム](Graphics/ids-diagram.png)

IDSファイル作成ツールやモデルチェックツールは、多くの企業が提供している。[ソフトウェア・ベンダー](https://technical.buildingsmart.org/ids-software-implementations/)どのソフトウェアから作成されたIFCモデルでも、IDSファイルと照合することができます。

## IDSの構造

各IDSファイルは[メタデータ](ids-metadata.md)を含み、1つ以上を含むことができる。[仕様書](specifications.md)仕様は、適用可能性（この仕様の対象となる要素を記述する部分）と、要件（適用可能な要素が持つべきもの、あるいは持つべきでないものを列挙する部分）の2つの部分から構成される。 適用可能性と要件はどちらも、property、entity、classification、material、partOfなどのファセットで構築される。

## 始め方

 1. IDSチェックをサポートするソフトウェアを選択する。[IDS対応ツール一覧](https://technical.buildingsmart.org/ids-software-implementations/)).
 2. ダウンロード[サンプルIDSファイル](../Examples/IDS_wooden-windows.ids).
 3. ダウンロード[サンプルIFCモデル](../Examples/IDS_wooden-windows_IFC.ifc)IDSと照合する。
 4. IDSとIFCの両方をソフトウェアにロードし、チェック・プロセスを開始する。
 5. すべての不適合の報告書を入手すべきである。

以上です！IDSファイルのサンプルは[例](../Examples)ヘルプが必要な場合は、お気軽にお問い合わせください。[buildingSMARTフォーラム](https://forums.buildingsmart.org/).

## IDSについてもっと知る

 1. [どのように**仕様**仕事？](specifications.md)
 1. [良好な仕様に関するガイドライン**仕様**メタデータ](ids-metadata.md)
 1. [指定方法**複合施設の制限**](restrictions.md)
 1. [の使い方を学ぶ。**エンティティ・ファセット**](entity-facet.md)
 1. [の使い方を学ぶ。**属性ファセット**](attribute-facet.md)
 1. [の使い方を学ぶ。**分類ファセット**](classification-facet.md)
 1. [の使い方を学ぶ。**物件ファセット**](property-facet.md)
 1. [の使い方を学ぶ。**素材ファセット**](material-facet.md)
 1. [の使い方を学ぶ。**PartOfファセット**](partof-facet.md)
 1. [ソフトウェア開発者の方は、開発者ガイドをお読みください！](../ImplementersDocumentation/developer-guide.md)
