# dev-env-consult

Ubuntu（WSL）・VSCode・PowerShell・CMD・Docker のコマンド相談スキルです。
IT研修講師兼フルスタックエンジニアとして、公式ドキュメントを根拠に答えます。
**コマンドは提案するだけで、実行は「実行」と許可したときだけ**行います。

---

## できること

| 機能 | 内容 |
|---|---|
| コマンド相談 | やりたいことから、環境に合ったコマンドを出す |
| 環境別の書き分け | bash／PowerShell／CMD の違い（改行 `\` `` ` `` `^`、`$(pwd)` `${PWD}` `%cd%` など）を並べて示す |
| トラブル診断 | 7ステップの診断フローで、原因を1つずつ絞り込む |
| エラーの読み解き | STATUS・終了コード（0／1／125／126／127／137／143）とよくあるエラーの対処 |
| 公式サイトで確認 | バージョンで変わる話は公式ドキュメントを調べ、出典リンクを付ける |
| 研修向けの説明 | 合言葉・セットで覚える動詞・「こう表示されればOK」の確認方法を添える |

## 安全ルール（実行は許可制）

実行する前に、毎回次の形で提示して返事を待ちます。

```
▶ 実行予定のコマンド（環境：Ubuntu bash）
docker system df

危険度：🟢 見るだけ（何も変更しない）
何が起きる：イメージ・コンテナ・ボリュームの使用容量を表示する
元に戻す方法：不要
→ 実行してよければ「実行」と返信してください
```

| 危険度 | 意味 | 例 |
|---|---|---|
| 🟢 見るだけ | 何も変更しない | `docker ps` `docker logs` `docker inspect` `Get-ChildItem` |
| 🟡 変更する | 戻せる変更 | `docker run` `docker stop` `docker build` `compose up` `apt install` |
| 🔴 消える | 戻せない | `docker rm` `prune` 系 `compose down -v` `sudo rm -rf` `wsl --unregister` |

- 読むだけのコマンドも、許可なしには実行しません。
- 許可は提示したコマンドにだけ有効です。次のコマンドは改めて確認します。
- 🔴 は、先に中身を確認するコマンドと、バックアップの方法も示します。

## インストール

### Claude Code（Ubuntu／WSL）

```bash
unzip dev-env-consult.zip
mkdir -p ~/.claude/skills
mv dev-env-consult ~/.claude/skills/
ls ~/.claude/skills/dev-env-consult   # SKILL.md と README.md があればOK
```

### Claude Code（PowerShell）

```powershell
Expand-Archive .\dev-env-consult.zip -DestinationPath .
New-Item -ItemType Directory -Force "$HOME\.claude\skills" | Out-Null
Move-Item .\dev-env-consult "$HOME\.claude\skills\"
Get-ChildItem "$HOME\.claude\skills\dev-env-consult"
```

### プロジェクト単位で使う場合

プロジェクト直下の `./.claude/skills/dev-env-consult/` に置きます。チームで共有できます。

## 使い方

明示して呼ぶ場合：

```
/dev-env-consult コンテナがすぐ Exited になる
```

普通に相談しても発動します（description のキーワードで判定）。

```
PowerShellで今のフォルダをDockerにマウントしたい
docker: permission denied が出た
VSCodeのターミナルでdockerが見つからない
使っていないイメージを消して容量を空けたい
```

## 回答の型

1. 結論（1〜2行）
2. 環境ごとのコマンド
3. 危険度と、何が起きるか
4. 正常なら何が表示されるか
5. 次の一手・合言葉
6. 出典（公式ドキュメント）
7. 実行してよいかの確認

## 参照する公式ドキュメント

| 対象 | URL |
|---|---|
| Docker CLI | https://docs.docker.com/reference/cli/docker/ |
| Docker Compose | https://docs.docker.com/compose/ |
| WSL | https://learn.microsoft.com/windows/wsl/ |
| PowerShell | https://learn.microsoft.com/powershell/ |
| Windows コマンド（CMD） | https://learn.microsoft.com/windows-server/administration/windows-commands/windows-commands |
| Ubuntu | https://ubuntu.com/server/docs ／ https://manpages.ubuntu.com/ |
| VSCode | https://code.visualstudio.com/docs |

## ファイル構成

```
dev-env-consult/
├── SKILL.md    # スキル本体（Claude が読む指示）
└── README.md   # この説明書（人が読む）
```

## カスタマイズ

| やりたいこと | 編集する場所（SKILL.md） |
|---|---|
| 危険度の判定を変える | 「最重要ルール：実行は許可制」の 4. |
| 参照サイトを足す | 「根拠：公式サイトを参照する」 |
| エラーと対処を足す | 「よくあるエラー」の表 |
| 発動しやすくする | 先頭の `description:` にキーワードを足す |

編集後は Claude Code を開き直すと反映されます。

## 元にした資料

- `docker-cheatsheet_20261025.xlsx`（必須TOP30、診断フロー、STATUSの読み方、トラブル対処表、3シェル対比 ほか）

## 注意

- コマンドのオプションや既定値は、バージョンによって変わります。最終確認は公式ドキュメントと `--help`・`man`・`Get-Help` で行ってください。
- 社外秘の情報（パスワード、`.env` の中身など）は、相談文に貼らないでください。

---

作成：2026-10-26
