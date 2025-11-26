# リポジトリポリシー
## 枝
主な作業ブランチは`development` で、開発中の最新の標準提案の状態が表示される。バージョンブランチは、`ver` で始まるブランチ、例えば`ver/1.1.x` にあります。標準の公式バージョンは、例えば`1.0.0` のようにタグでマークされており、[GitHubのrealesesでも](https://github.com/buildingSMART/IDS/releases)見ることができる。 

<img src="Graphics/branch-policy.svg" alt="branch-policy" width="600"/>

## 貢献
誰でも IDS リポジトリに貢献することができます。アイデアや問題があるが解決方法がわからない場合は、[Issue ボードに](https://github.com/buildingSMART/IDS/issues)書き込んでください。変更を加えて貢献したい場合は、最も関連性の高いブランチ (おそらく 'development' ですが、バグ修正のためのバージョンブランチもあります) に基づいて専用のブランチを作成してください。

変更の性質に応じて、`feature/` 、`bugfix/` または`docs/` という接頭辞を付け、その後に発行番号（存在する場合）と説明的な名前を付ける： `feature/<issue-number>-<descriptive-name>`


## バージョン名
IDS標準のバージョンについては、[セマンティックバージョン](https://semver.org/)命名に従う。`MAJOR.MINOR.PATCH` （例1.2.3）：
- 互換性のない変更のためのメジャーバージョン。
- 下位互換性のある機能追加のためのマイナーバージョン。
- 後方互換性のある修正のためのPATCHバージョン - 別個の認証手続きは必要ありません。
