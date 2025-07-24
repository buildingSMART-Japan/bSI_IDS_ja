# テストケースに貢献する

このフォルダー内のテストケースは、スクリプト言語からプログラムで生成することができ、保守者の労力を最小限に抑えるように設計されている。

可能であれば、テスト・スイートへの貢献はプル・リクエストとして行うべきである。

各試験は2つのパートで構成される：

1. 関連する[ドキュメントファイル](scripts.md).
1. 最小化されたIFCファイルで、結果のIDSと照合して検証する必要がある。

## スクリプト・ドキュメント

ドキュメンテーション・スクリプトのスニペットは以下のようなものだ：

```` text
### Test case title

An optional (but welcome) description of the rationale of the test.

``` ids attribute/<pass/fail/invalid>-<Test file name>.ids
Test case title
IFC4
Entity: ''IFCPRESENTATIONLAYERWITHSTYLE''
Requirements:
Attribute: ''LayerOn''
```
````

で始まる各コードブロックは` ids `シーケンスの後にローカルファイル名が続くと、IDSに変換される。

の中のスクリプトの構文は[トリプルバックティック](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks#fenced-code-blocks)は以下の通りである：

### タイトル

最初の行は、常にIDSのタイトルと含まれる仕様名として解釈される。

### スキーマ

次の行が`IFC2X3`,`IFC4`そして`IFC4X3_ADD2`トークンをどのような順序で並べたとしても、それは仕様のスキーマを定義する。
This line is optional, when the schema is omitted, the default schemas of the IDS are `IFC2X3 IFC4`. Note that the capitalization of this line matters.

### 適用カーディナリティ

次の行がトークスの一つである場合`Optional`,`Required`あるいは`Prohibited`IDSの適用範囲を定義する。
This line is optional, when omitted, the default cardinality is set to `Required`. Note that the capitalization of this line matters.

### 適用ファセット

それに続く各行は、適用可能なファセットとして解釈される。`Requirements:`トークンに遭遇した場合

### 要件ファセット

一旦`Requirements:`トークンが見つかった場合、それに続く各行は要件ファセットとして解釈される。

## オートメーション

既存のIDSをスクリプト言語に自動変換することも可能である。

そのためには、IDSファイルを`testcases`フォルダーにあるビルド・ターゲットのいずれかを起動し、コンピューター上でスクリプトを実行する。

スクリプトの実行には、Windows、MacOS、Linuxで利用可能な.NET 6.0 SDKがコンピュータにインストールされている必要があります。

お使いのシステムに応じて、適切なコマンドを`RepositoryAutomation`フォルダーにある：

1. 窓のパワーシェルについて：`./build.ps1 CreateTestCases`
1. ウィンドウズのコマンドプロンプトで`build CreateTestCases`
1. マックのターミナルで：`./build.sh CreateTestCases`
1. linuxのターミナルで：`./build.sh CreateTestCases`

出力結果には、以下のようなセクションが含まれているはずだ：

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

について`Extra IDS report generated:`テキストはHTMLレポートを示す：

1. 変換されたスクリプトIDSの構文
2. 元のIDSとスクリプトが生成したIDSの違い

必要に応じてスクリプトを調整し、上記のアドバイスに従って文書に追加する。
