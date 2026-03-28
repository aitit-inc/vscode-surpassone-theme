# CLAUDE.md

## Project Overview

SurpassOne Theme — VS Code / Cursor 用のフラット・モノクロームカラーテーマ。
コーラル1色 + グレーの濃淡だけでシンタックスハイライトを表現する。

## Theme Design Principles

- **ワンカラー**: シンタックスで使う「色」はコーラルのみ。それ以外はグレーの濃淡で階層を作る
- **フラット**: ボーダーや影を極力排除し、背景色の差だけで領域を区別する
- **視認性**: 色数を減らす代わりに、トーンの段階で読みやすさを担保する

### Syntax Tonal Hierarchy

| 層 | Dark | Light | 対象 |
|---|---|---|---|
| コーラル (bold) | `#E8755E` | `#C05248` | キーワード, タグ, this, デコレータ |
| 明グレー | `#C3C4C9` | `#444444` | 変数, 関数, プロパティ |
| 中グレー | `#A8A9AE` | `#5E5E5E` | 文字列, 型, 数値, 定数, 属性 |
| 淡グレー (italic) | `#64656A` | `#A7A19E` | コメント |
| 句読点 | `#86878C` | `#847E7B` | 演算子, 括弧 |

### Font Style Rules

- bold → キーワードのみ
- italic → コメントのみ
- underline → 使わない

## File Structure

```
themes/
  surpassone-dark-color-theme.json   # ダークテーマ定義
  surpassone-light-color-theme.json  # ライトテーマ定義
package.json                         # 拡張マニフェスト (version, publisher 等)
.github/workflows/publish.yml        # 自動公開ワークフロー
```

テーマファイルは JSON のみ。ビルドステップなし。

## Development

### ローカルプレビュー (Cursor)

開発時はシンボリックリンクを使って即時プレビューする:

```bash
# リンク作成 (初回のみ)
ln -s /Users/leo/src/vscode-surpassone-theme ~/.cursor/extensions/surpassone-theme

# リンク削除 (マーケットプレイス版に戻すとき)
rm ~/.cursor/extensions/surpassone-theme
```

リンクがある間はテーマ JSON を保存するだけで変更が即反映される。
Cursor 再起動後に `Cmd+Shift+P` → `Color Theme` → SurpassOne を選択。

**注意**: マーケットプレイスからインストールした拡張と競合する場合は、マーケットプレイス版を一時的に無効化する。

### テーマの色を調整するとき

`Developer: Inspect Editor Tokens and Scopes` コマンドで、任意のトークンの TextMate スコープを確認できる。

## Release

タグを push すると GitHub Actions が自動で VS Code Marketplace, Open VSX, GitHub Releases に公開する。

```bash
# 1. package.json の version を更新
# 2. コミット & push
git add package.json
git commit -m "v0.X.0"
git push

# 3. タグを打って push → 自動公開
git tag v0.X.0
git push --tags
```

### 公開先

| 配信先 | 対象 |
|---|---|
| VS Code Marketplace | VS Code ユーザー |
| Open VSX | Cursor, VSCodium 等 |
| GitHub Releases | .vsix 直接ダウンロード |

### Secrets (GitHub Repository Settings)

- `VSCE_PAT` — VS Code Marketplace の Personal Access Token
- `OVSX_PAT` — Open VSX のアクセストークン

## Organization

- 会社名: SurpassOne
- GitHub org: `aitit-inc`
- Marketplace publisher ID: `surpassone`
