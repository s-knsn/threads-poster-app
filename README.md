# threads-poster-app — 投稿承認用モバイルPWA

[threads-poster](https://github.com/s-knsn/threads-poster)(private)の投稿キューをスマホから
承認・再スケジュールするためのWebアプリ。GitHub Pagesでホストする。

## このrepoが公開でも安全な理由

- ここにあるのは**汎用のアプリコードだけ**。投稿文・認証キー・アカウント情報は一切含まれない
- キューのデータは「スマホ ⇄ GitHub API」間の直接通信(HTTPS)のみで、このサイトを経由しない
- 認証キー(Fine-grained PAT)は**スマホのブラウザ内(localStorage)にのみ**保存される

## できること(v1)

- 下書き(draft)の承認: 時刻プリセット(7/12/18/21時) or カスタム日時 → 承認確認 → 予約
- 失敗(failed)・期限切れ(expired)の確認と再スケジュール
- 予約(approved)の取り消し、投稿済み(posted)の直近確認
- PC側(Claude Code)との同時編集に安全: 保存直前に最新を再取得し、対象の投稿だけを変更

## スマホでの初期設定(初回のみ・約5分)

1. **PATを発行**(スマホまたはPCで):
   GitHub → Settings → Developer settings → Fine-grained tokens → Generate new token
   - Repository access: **Only select repositories → threads-poster**
   - Permissions: **Contents = Read and write**
   - 有効期限: 最長を選択(切れたら再発行して⚙から入れ直す)
2. スマホでアプリURLを開く → 初期設定画面にPATを貼って保存
3. **ホーム画面に追加**:
   - iPhone: Safariの共有ボタン → 「ホーム画面に追加」
   - Android: Chromeのメニュー → 「アプリをインストール」

## セキュリティ

- PATはこのrepo(threads-poster)のContents読み書きしかできない最小権限
- スマホ紛失時: GitHub → Settings → Fine-grained tokens → 該当トークンを **Revoke** すれば即無効化
