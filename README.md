# free-one-api

Turn reverse engineered LLM lib to standard OpenAI GPT API.  
By using free-one-api, you can easily convert reverse engineered LLM libs (e.g. [acheong08/ChatGPT](https://github.com/acheong08/ChatGPT) ) to standard OpenAI GPT API.  
So other application supports OpenAI GPT API can use reverse engineered LLM libs directly.

## Features

- Automatically load balance.
- Web UI.
- Stream mode supported.

### Supported LLM libs

- [acheong08/ChatGPT](https://github.com/acheong08/ChatGPT)

## Setup

### Docker (Recommended)

```bash
docker run -d -p 3000:3000 --name free-one-api rockchin/free-one-api -v ./data:/app/data
```

then you can open the admin page at `http://localhost:3000/`.

### Manual

```bash
git clone https://github.com/RockChinQ/free-one-api.git
cd free-one-api

cd web && npm install && npm run build && cd ..

pip install -r requirements.txt
python main.py
```

then you can open the admin page at `http://localhost:3000/`.

## Usage

Create channel on the admin page, create a new key.  
Set the url (e.g. http://localhost:3000/v1 ) as OpenAI endpoint, and set the generated key as OpenAI api key.  
Then you can use the OpenAI API to access the reverse engineered LLM lib.

```curl
# curl example
curl http://localhost:3000/v1/chat/completions \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ],
    "stream": true
  }'
```
