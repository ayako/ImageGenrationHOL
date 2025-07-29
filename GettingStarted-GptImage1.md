
# Azure OpenAI Service の GPT-Image-1 を使った画像生成手順

## 0. Azure OpenAI Service GPT-Image-1 の利用申請
- GPT-Image-1 を利用するには、予め利用申請が必要です。

## 1. Azure OpenAI Service & GPT-Image-1 の利用準備
- Azure AI Foundry (ポータル) にサインインし、新規プロジェクトを作成します。
- リソースグループ、リージョンを選択し、リソースを作成します。
- 作成したプロジェクトを開き、「モデルのデプロイ」から「gpt-image-1」モデルを選択し、デプロイ名を入力してデプロイします。
- 作成した gpt-image-1 を選択、「エンドポイント」と「キー」を取得します。これらはAPIリクエスト時に必要です。

## 2. GPT-Image-1 の呼び出し

### REST API での呼び出し例

```http
POST https://<your-resource-name>.openai.azure.com/openai/deployments/<deployment-name>/images/generations:submit?api-version=2024-02-15-preview
api-key: <your-api-key>
Content-Type: application/json

{
  "prompt": "富士山と桜の美しい風景を描いてください。",
  "n": 1,
  "size": "1024x1024"
}
```

### Python での呼び出し例

```python
import requests

endpoint = "https://<your-resource-name>.openai.azure.com/openai/deployments/<deployment-name>/images/generations:submit?api-version=2024-02-15-preview"
api_key = "<your-api-key>"

headers = {
    "api-key": api_key,
    "Content-Type": "application/json"
}

data = {
    "prompt": "富士山と桜の美しい風景を描いてください。",
    "n": 1,
    "size": "1024x1024"
}

response = requests.post(endpoint, headers=headers, json=data)
print(response.json())
```

### JavaScript (Node.js) での呼び出し例

```javascript
const fetch = require('node-fetch');

const endpoint = 'https://<your-resource-name>.openai.azure.com/openai/deployments/<deployment-name>/images/generations:submit?api-version=2024-02-15-preview';
const apiKey = '<your-api-key>';

const data = {
  prompt: '富士山と桜の美しい風景を描いてください。',
  n: 1,
  size: '1024x1024'
};

fetch(endpoint, {
  method: 'POST',
  headers: {
    'api-key': apiKey,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
})
  .then(res => res.json())
  .then(json => console.log(json))
  .catch(err => console.error(err));
```
