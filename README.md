# ja-subject-predicate-check

Claude Code向けの日本語「主述の骨格検査と直接修正」スキルです。

文を区切り、主語・必須格・述語の骨格を抽出したうえで主述の対応を検査します。明示的に実行したときだけ動作し、対象ファイルを**直接編集**します。意味を確定できない箇所は勝手に書き換えず報告します。

## 使い方

Claude Codeにて、対象は次のいずれかで指定できます。

```text
/ja-subject-predicate-check docs/design.md                 # ファイルを直接編集
/ja-subject-predicate-check docs/a.md docs/b.md            # 複数ファイル
/ja-subject-predicate-check                                # 引数なし = 直前のアシスタント出力
/ja-subject-predicate-check 直前の出力
/ja-subject-predicate-check 2 つ前の回答の「設定手順」の節だけ
/ja-subject-predicate-check 私が貼った文章
/ja-subject-predicate-check 会議の目的は資料を共有する。  # 文章そのもの
/ja-subject-predicate-check 直前の出力 保存先: C:\work\note.md
```

ファイル以外を対象にしたときは修正済み全文を出力します。「保存先: パス」を付けると、修正前を `<名前>.before<拡張子>`、修正後を `<名前><拡張子>` に書き出すので、`git diff --no-index` などで前後比較できます。

## インストール

Claude Codeの個人用スキルフォルダへ、このリポジトリの`SKILL.md`を配置してください。

- Windows: `%USERPROFILE%\.claude\skills\ja-subject-predicate-check\SKILL.md`
- macOS / Linux: `~/.claude/skills/ja-subject-predicate-check/SKILL.md`

または、次のようにリポジトリをクローンできます。

```bash
git clone https://github.com/kumisun/ja-subject-predicate-check.git ~/.claude/skills/ja-subject-predicate-check
```

プロジェクトのみに適用する場合は、`<project>/.claude/skills/ja-subject-predicate-check/SKILL.md`へ配置します。

## 仕様と注意

- `disable-model-invocation: true`により、Claudeによる自発的な起動を禁止しています。
- 文章の意味や技術的事実を推測して変更しないよう指示しています。ただし、AIによる修正の正確性は保証されません。編集前にGitでコミットするなどして差分を確認できる状態で使用してください。
- ライセンスはMITです（`LICENSE`を参照）。

参考：[Claude Code公式Skillsドキュメント](https://code.claude.com/docs/en/skills)
