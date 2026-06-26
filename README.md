# 📚 読書管理アプリ

スマホで使える、サーバー不要の読書管理アプリ（PWA）。
バーコード（ISBN）スキャン・タイトル/著者検索で本を登録し、「読みたい / 読書中 / 読了」で管理できます。サービス終了した読書管理SNSの代わりに、自分用の本棚として使えます。

## できること

- 📷 **バーコードスキャン** … 本の裏のISBNバーコードをスマホのカメラで読み取って登録
- 🔍 **検索登録** … タイトル・著者名・ISBNで検索して登録（日本語の本もOK）
- 📖 **ステータス管理** … 読みたい / 読書中 / 読了
- ⭐ **評価＆メモ** … 星5段階評価と感想メモ
- 💾 **バックアップ** … JSON形式で書き出し / 読み込み（機種変更時の引き継ぎに）
- 📲 **ホーム画面に追加** … アプリのように起動・オフラインでも閲覧可能

データはお使いの端末のブラウザ内（localStorage）に保存され、外部には送信されません。

## 使っているデータソース（無料・APIキー不要）

- [openBD](https://openbd.jp/) … 日本の書籍の書誌（ISBN検索の主データ）
- [Google Books API](https://developers.google.com/books) … タイトル・著者検索の主データ
- [国立国会図書館サーチ](https://ndlsearch.ndl.go.jp/) … Google Booksが使えない時のタイトル・著者検索の予備
- [Open Library Covers](https://openlibrary.org/dev/docs/api/covers) … 書影が無いときの予備
- [html5-qrcode](https://github.com/mebjas/html5-qrcode) … バーコード読み取り

### 検索が「ほとんどヒットしない」場合について
タイトル・著者検索は Google Books を主に使っています。Google Books はキー無しだと **同じIPからのアクセスが多いと一時的に制限（429）** されることがあり、特にモバイル回線（多数の利用者で同じIPを共有する）では出やすくなります。本アプリは Google が使えない時に**自動で国立国会図書館サーチに切り替える**ようにしてあるので、その場合でも日本語書籍はヒットします（ただし並び順は Google ほど賢くありません）。Wi-Fi 環境だと Google 側が安定しやすいです。

## GitHub Pages で公開する手順（誰でも使える状態にする）

1. GitHubで新しいリポジトリを作成（例：`book-tracker`、Publicを選択）
2. このフォルダの中身（`index.html` などすべて）をアップロード
   - 簡単な方法：リポジトリ画面の「Add file」→「Upload files」でドラッグ＆ドロップ
3. リポジトリの **Settings → Pages** を開く
4. 「Build and deployment」の Source を **Deploy from a branch** にし、Branch を **main / (root)** に設定して Save
5. 数十秒後、`https://<ユーザー名>.github.io/book-tracker/` でアクセス可能になります
6. そのURLをスマホで開き、ブラウザメニューから「ホーム画面に追加」

> ⚠️ カメラ（バーコードスキャン）は **https環境でのみ動作**します。GitHub Pagesは自動でhttpsになるので問題ありません。ローカルで開く場合（file://）はスキャンが使えませんが、検索は使えます。

## ローカルでの動作確認

カメラ機能まで試すには簡易サーバーが必要です（例）：

```bash
# Python が入っていれば
python -m http.server 8000
# → http://localhost:8000 を開く（localhostはカメラ許可されます）
```

## ファイル構成

| ファイル | 役割 |
|---|---|
| `index.html` | アプリ本体（UI・ロジックすべて） |
| `manifest.webmanifest` | PWA設定（ホーム追加・アプリ名） |
| `sw.js` | Service Worker（オフライン対応） |
| `icon.svg` | アプリアイコン |

## ライセンス

MIT
