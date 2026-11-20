# MATHESIS

数学コンテンツ共有サイトの初期実装です。静的ホスティング + Firebaseを想定しています。

## できること
- Googleログイン
- 公開投稿一覧、検索、分野フィルター
- 投稿の作成、下書き保存、公開、編集、削除
- 文章、LaTeX数式、問題、解答・解説、簡易図形、関数グラフのブロック編集
- ログインユーザーによる質問、投稿者による回答
- Firestore Security Rulesによる投稿者権限の保護

## Firebaseセットアップ
1. https://console.firebase.google.com/ でプロジェクトを作成
2. Authentication > Sign-in method で Google を有効化
3. Authentication > Settings > Authorized domains に公開先ドメインを追加
4. Firestore Databaseを作成
5. プロジェクト設定 > マイアプリ > Webアプリを登録し、Firebase configを取得
6. `index.html` 内の `firebaseConfig` の `YOUR_...` を実際の値に置換
7. Firestore > Rules に `firestore.rules` の内容を貼り付けて公開
8. `index.html` をFirebase Hosting、GitHub Pages等に配置

## ローカル確認
ES modulesを使うため、`index.html` を直接 file:// で開かず、ローカルHTTPサーバーで開いてください。
例: `python -m http.server 8000` を実行し、http://localhost:8000 を開く。

## 現在の実装上の注意
- Firebase設定前はUIのプレビューのみで、ログイン・投稿保存は動きません。
- 図形エディタはクリックで点を置き、点を結ぶ簡易ポリライン方式です。作図ツール（円・角度・垂線等）は次段階で拡張できます。
- 関数グラフはブラウザ内の簡易式評価です。信頼できない式をサーバーで実行する仕組みではありません。
- 数式入力はMathLive、表示はKaTeXを使用します。MathLiveの入力値はLaTeXとして保存されます。
- グラフ描画式は初期プロトタイプです。任意コードを実行しない安全な数式パーサーへの置き換えを推奨します。
- 質問と回答はFirestoreのサブコレクションに保存されます。
- 本番運用前にFirebaseの利用上限、バックアップ、通報・スパム対策、利用規約・プライバシーポリシーを整備してください。

## 構成
- `index.html`: フロントエンド
- `firestore.rules`: 投稿・質問のアクセス制御
