=========================
TERU AI Proxy Server セットアップ手順
=========================

◆ 準備：
1. Render.com（無料）でアカウントを作成
   → https://render.com

2. GitHub にログインし、新しいリポジトリを作成（例：teru-ai-proxy）
3. このZIPを解凍して、3つのファイルをGitHubリポジトリにアップロード
   - server.js
   - package.json
   - README.txt

◆ Renderデプロイ：
1. Renderのダッシュボード → 「New」→「Web Service」
2. GitHubと連携して、リポジトリ「teru-ai-proxy」を選択
3. 設定：
   - Name: teru-ai-proxy
   - Environment: Node
   - Build Command: （空欄のまま）
   - Start Command: node server.js
4. Environment Variables に以下を追加：
   - OPENAI_API_KEY = （OpenAIのAPIキー）
5. Deployボタンをクリック

◆ デプロイ後：
- URL（例：https://teru-ai-proxy.onrender.com）をコピー
- GitHub PagesのAIツール側で次のように設定：
  script.js 内の
  const API_BASE = "https://teru-ai-proxy.onrender.com/api/chat";

これでCORSエラーは解消され、GitHub Pagesから安全にOpenAI APIを呼び出せます。
