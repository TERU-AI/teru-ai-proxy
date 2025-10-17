# 🧩 TERU AI Proxy Server - Setup Guide (for Render)

このプロキシは、GitHub Pages などの静的サイトから OpenAI API を安全に呼び出すための中継サーバーです。

---

## 🚀 手順（初心者向け）

### ① GitHub にアップロード
1. `teru-ai-proxy.zip` を解凍します。
2. `server.js` と `package.json`、`README_SETUP.md` の3つのファイルを **新しいGitHubリポジトリ（例: teru-ai-proxy）** にアップロードします。

### ② Render で新規Webサービスを作成
1. https://render.com にログインまたは無料登録します。
2. 「New +」 → 「Web Service」 を選択。
3. 「Connect your GitHub」 → 上記リポジトリ（`teru-ai-proxy`）を選択。
4. 設定は以下の通り：
   - **Environment:** Node
   - **Build Command:** （空欄のままでOK）
   - **Start Command:** `node server.js`
5. 「Create Web Service」をクリックしてデプロイ。

### ③ 環境変数を設定
1. Render の「Dashboard」→ サービス名（例: `teru-ai-proxy`）をクリック。
2. 「Environment」タブを開く。
3. **Add Environment Variable** をクリックして以下を入力：
   - `OPENAI_API_KEY` = あなたのOpenAIのAPIキー（sk-から始まるもの）
4. 「Save Changes」をクリック。

### ④ 公開URLを確認
- デプロイ完了後、Renderの画面に  
  例：`https://teru-ai-proxy.onrender.com` が表示されます。  
  このURLがあなたの **APIプロキシURL** です。

### ⑤ GitHub Pages側（AIブログツール）と接続
`script.js` 内のAPIエンドポイントを次のように変更します：

```js
// 変更前
fetch("https://api.openai.com/v1/chat/completions", ...)

// 変更後
fetch("https://teru-ai-proxy.onrender.com/v1/chat/completions", ...)
```

同様に画像生成APIも：

```js
fetch("https://teru-ai-proxy.onrender.com/v1/images/generations", ...)
```

---

✅ これで、GitHub Pages上のAIブログツールがCORSエラーなしで動作します！
