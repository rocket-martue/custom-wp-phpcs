# WordPress Plugin Coding Standard

このプロジェクトでは、WordPress Coding Standards（WPCS）に基づいたカスタムルールにより、コード品質とスタイルの統一を図っています。
WordPressの基本ルールに沿いつつ、現場でありがちなストレスを最小限にする内容になっています。
静的解析ツール [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) により、チーム全体でのスタイルチェックを自動化しています。

---

## 📌 使用するルールセット

`phpcs.xml` にて、WordPressの標準ルールに一部カスタマイズを加えた独自ルールセットを定義しています。

### ベースルール
- `WordPress`（= `WordPress-Core` + `WordPress-Extra` + `WordPress-Docs`）

---

## ⚙️ カスタムルール（除外内容）

| 対象ルール | 内容 | 理由 |
|------------|------|------|
| `Generic.Files.LineEndings.InvalidEOLChar` | 改行コード（\r\n, \n）を許容 | OS（Mac/Windows）間の開発環境差異に対応 |
| `Squiz.PHP.CommentedOutCode.Found` | コメントアウトされたコードを許容 | デバッグ用コードの一時保持を想定（最終的には削除推奨） |
| `Squiz.Commenting.InlineComment.InvalidEndChar` | コメントの末尾ピリオドを不要とする | 実用性を重視し、自然な記述を許容 |
| `Generic.Arrays.DisallowShortArraySyntax.Found` | `[]` の短縮配列構文を許可 | PHP 5.4以降の標準記法として許容 |
| `Generic.ControlStructures.InlineControlStructure.NotAllowed` | 一行 `if` 文を許容 | 簡潔なコードを許可し柔軟性を確保 |

#### コメントアウト中の除外（必要に応じて有効化）

- `WordPress.Files.FileName`  
- `WordPress.PHP.DisallowShortTernary.Found`  
- `Squiz.Commenting`, `Generic.Commenting`

---

## 🚫 除外ディレクトリ

以下のディレクトリは自動チェック対象外です：

- `node_modules/`
- `vendor/`

---

## 🧰 セットアップ手順

### 1. WPCSのインストール

```bash
composer require --dev wp-coding-standards/wpcs
```

### 2. PHPCS に WPCS を登録

```bash
vendor/bin/phpcs --config-set installed_paths vendor/wp-coding-standards/wpcs
```

### 3. 適用ルールの確認（任意）

```bash
vendor/bin/phpcs -i
```

---

## ✅ チェックと自動整形の実行

### コードスタイルチェック：

```bash
vendor/bin/phpcs
```

### 自動整形（可能な範囲）：

```bash
vendor/bin/phpcbf
```

---

## 💬 運用ルールと相談窓口

- 新たなルール追加や既存ルールの除外提案などは、プロジェクト管理者までお知らせください。
- チーム内で合意形成のうえ `phpcs.xml` を更新します。

---

## 🔗 参考リンク

- [PHP_CodeSniffer GitHub](https://github.com/squizlabs/PHP_CodeSniffer)
- [WordPress Coding Standards](https://github.com/WordPress/WordPress-Coding-Standards)
