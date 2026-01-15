# テストケースに貢献する
このフォルダー内のテストケースは、スクリプト言語からプログラムで生成することができ、保守者の労力を最小限に抑えるように設計されている。

可能であれば、テスト・スイートへの貢献はプル・リクエストとして行うべきである。

各試験は2つの部分から構成される：

1. 関連する[ドキュメント・](scripts.md)ファイルのエントリ。

1. 最小化されたIFCファイルで、結果のIDSと照合して検証する必要がある。

## ドキュメンテーション・スクリプト
ドキュメンテーション・スクリプトのスニペットは以下のようなものだ：

```` text
### テストケースのタイトル
An optional (but welcome) description of the rationale of the test.

``` ids attribute/<pass/fail/invalid>-<Test file name>.ids
Test case title
IFC4
Entity: ''IFCPRESENTATIONLAYERWITHSTYLE''
Requirements:
Attribute: ''LayerOn''
```
````

` ids `シーケンスで始まり、ローカルファイル名が続く各コードブロックは、IDSに変換される。

[三重のバックティック](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks#fenced-code-blocks)内のスクリプトの構文は以下の通り：

### タイトル
最初の行は、常にIDSのタイトルと含まれる仕様名として解釈される。

### スキーマ
次の行が `IFC2X3``IFC4`、および `IFC4X3_ADD2`トークンの並びであれば、どのような順番であっても、仕様のスキーマを定義していることになります。  
この行は省略可能で、スキーマを省略した場合、IDS のデフォルト・スキーマは次のようになります。 `IFC2X3 IFC4`です。この行の大文字小文字は重要であることに注意してください。

### 適用カーディナリティ
以下の行が、`Optional`、`Required`、`Prohibited`いずれかのトークスである場合、IDSの適用可能なカーディナリティを定義する。  
この行は省略可能で、省略された場合、デフォルトのカーディナリティは`Required`設定される。この行の大文字小文字は重要であることに注意。

### 適用ファセット
後続の各行は、`Requirements:`トークンに遭遇するまで、適用可能なファセットとして解釈される。

### 要件ファセット
`Requirements:`トークンが見つかると、それに続く各行は要件ファセットとして解釈されます。

## オートメーション
既存のIDSをスクリプト言語に自動変換することも可能である。

そのためには、`testcases`フォルダのサブディレクトリにIDSファイルを記述し、ビルドターゲットのいずれかを起動してコンピュータ上でスクリプトを実行します。

スクリプトの実行には、Windows、MacOS、Linuxで利用可能な.NET 6.0 SDKがコンピュータにインストールされている必要があります。

システムによっては、リポジトリの`RepositoryAutomation`フォルダで適切なコマンドを起動します：

1. 窓のパワーシェルについて：`./build.ps1 CreateTestCases`

1. ウィンドウズのコマンドプロンプトで`build CreateTestCases`

1. マックのターミナルで：`./build.sh CreateTestCases`

1. linuxのターミナルで：`./build.sh CreateTestCases`

結果の出力には、以下のようなセクションが含まれているはずだ：

``` text
╬════════════════════
║ CreateTestCases
╬═══════════

17:33:55 [INF] > "C:\Program Files\dotnet\dotnet.exe" run --configuration Release --project C:\Data\Dev\BuildingSmart\IDS\SchemaProject\SchemaProject.csproj
17:33:57 [DBG] Hello IDS!
17:33:57 [DBG] Process started in: C:\Data\Dev\BuildingSmart\IDS
17:33:57 [DBG] Testcase generation started in: C:\Data\Dev\BuildingSmart\IDS\Documentation\testcases
17:33:57 [DBG] Extra IDS report generated: C:\Data\Dev\BuildingSmart\IDS\Documentation\testcases\library\sample1.html
17:33:57 [DBG] Extra IDS report generated: C:\Data\Dev\BuildingSmart\IDS\Documentation\testcases\library\sample2.html
17:33:57 [DBG] Extra IFC: - C:\Data\Dev\BuildingSmart\IDS\Documentation\testcases\entity\fail-a_predefined_type_must_always_specify_a_meaningful_type__not_userdefined_itself.ifc
17:33:57 [DBG] Extra IFC: - C:\Data\Dev\BuildingSmart\IDS\Documentation\testcases\library\sample1.ifc
17:33:57 [DBG] Extra IFC: - C:\Data\Dev\BuildingSmart\IDS\Documentation\testcases\library\sample2.ifc
17:33:57 [DBG] All scripting IFC files found
17:33:57 [DBG]
17:33:57 [DBG] Done
```

`Extra IDS report generated:`テキストは、以下の内容を含むHTMLレポートを示す：

1. 変換されたスクリプトIDSの構文

1. 元のIDSとスクリプトが生成したIDSの違い

この情報は、良いPRを作成するのに役立つはずです。必要に応じてスクリプトを調整し、上記のアドバイスに従ってドキュメントに追加してください。
