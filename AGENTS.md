# プロジェクト方針

- SvelteKit の SPA を ASP.NET Core から配信する構成を維持する。
- API のアクセスパスの先頭は `/api/` とする。
- 実装とドキュメントを一致させ、構成変更時は README.md も更新する。

## 作業前に読む文書

- ルール追加が妥当と考えるケースでは、ユーザが承諾した場合にルールを追加する。
- `.agents/rules/**` と各サブシステムの `AGENTS.md` に定義されたルールは、既存コードの実装・配置より優先する。既存コードがルールと矛盾する場合は、今回の変更対象はルールに沿う形に修正すること。対象外の矛盾は報告する。共通ルールとサブシステムの `AGENTS.md` が矛盾した場合、より対象範囲が狭いルールを優先する。例外が必要な場合はユーザに確認した上で修正すること。
- 全ての開発作業で `.agents/rules/common/README.md` を読み、該当する共通ルール（今後追加予定）に従うこと。
- frontend 配下を変更する前に、frontend/AGENTS.md が存在する場合は読む。
- backend 配下を変更する前に、backend/AGENTS.md が存在する場合は読む。

## 共通コーディング規約

- 識別子は英語、説明コメントは日本語で記載する。
- 既存の命名とファイル構成に合わせる。
- コメントには処理の説明より、判断の理由を記載する。
- backend/wwwroot のビルド生成物は直接編集せず、frontend のソースを変更して再生成する。

## 変更後の確認

以下のコマンドはリポジトリ直下から実行する。

- フロントエンド変更時: npm --prefix frontend run check
- バックエンド変更時: dotnet build backend
- フロントエンドの動作・テスト変更時: npm --prefix frontend run test
- バックエンドの動作・テスト変更時（`backend.Tests` 配置後から有効）: dotnet test backend.Tests
- 配備構成の変更時: dotnet publish backend -c Release
- 完了報告には確認結果と、実行できなかった確認を記載する。

| 操作 | コマンド |
| -- | -- |
| 開発サーバ起動 | `mise run dev` |
