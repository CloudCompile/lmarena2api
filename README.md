<p align="right">
<strong>Chinese</strong>
</p>
<div align="center">

# lmarena2api

_If you find this interesting, don't forget to give it a ⭐_

<a href="https://t.me/+LGKwlC_xa-E5ZDk9">
<img src="https://img.shields.io/badge/Telegram-AI Wave Community-0088cc?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram Community" />
</a>

<sup><i>AI Wave Community</i></sup> · <sup><i>(Public API and AI bots available in the group)</i></sup>


</div>

> ⚠️**Because `lmarena` uses Cloudflare's interactive challenge verification, it is strongly recommended to deploy the project in a [`win`/`mac` environment](#mac-local-deployment-recommended). After startup, you can use intranet penetration for public network access.**

## Features

- [x] Supports conversational interface (streaming/non-streaming) (`/chat/completions`), see [Supported Models](#supported-models) for details
- [x] Supports text-to-image generation compatible with conversational interface (`/chat/completions`) and image generation interface (`/images/generations`)
- [x] Supports custom request header verification value (Authorization)
- [x] Supports cookie pool (random), see [How to obtain cookies](#cookie-acquisition-methods) for details
- [x] Supports automatic cookie switching and retrying on request failure (requires cookie pool configuration)
- [x] Configurable proxy requests (environment variable `PROXY_URL`)

### API Documentation:

[Omitted]

### Example:

[Omitted]

## How to Use

[Omitted]

## How to Integrate NextChat

[Omitted]

## How to Integrate one-api

[Omitted]

## Deployment

### Mac Local Deployment [Recommended]

Download the `lmarena2api` file corresponding to your environment from the [Releases page](https://github.com/deanxv/lmarena2api/releases) and place it in your desired directory. Terminal execution:

```shell
nohup env CF_CLEARANCE=****** DEBUG=true LA_COOKIE=****** API_SECRET=123456  ./lmarena2api-macos > logfile.log 2>&1 &
```

### Deployment using Docker-Compose (All In One)

```shell
docker-compose pull && docker-compose up -d
```

#### docker-compose.yml

```docker
version: '3.4'

services:
lmarena2api:
image: deanxv/lmarena2api:latest
container_name: lmarena2api
restart: always
ports:
- "10088:10088"
volumes:
- ./data:/app/lmarena2api/data
environment:
- LA_COOKIE=******  # cookie (separate multiple values ​​with commas)
- CF_CLEARANCE=******
- API_SECRET=123456  # [Optional] API key - modify this value for request header verification (separate multiple values ​​with commas)
- TZ=Asia/Shanghai
```

### Deployment using Docker

```docker
docker run --name lmarena2api -d --restart always \
-p 10088:10088 \
-v $(pwd)/data:/app/lmarena2api/data \
-e LA_COOKIE=***** \
-e CF_CLEARANCE=***** \
-e API_SECRET="123456" \
-e TZ=Asia/Shanghai \
deanxv/lmarena2api
```

Replace `API_SECRET`, `LA_COOKIE`, and `CF_CLEARANCE` with your own values.

If the above image cannot be pulled, you can try using the GitHub Docker image by replacing `deanxv/lmarena2api` with
`ghcr.io/deanxv/lmarena2api`. ### Deployment to Third-Party Platforms

<details>
<summary><strong>Deploy to Zeabur</strong></summary>
<div>

[![Deployed on Zeabur](https://zeabur.com/deployed-on-zeabur-dark.svg)](https://zeabur.com?referralCode=deanxv&utm_source=deanxv)

> Zeabur's servers are located abroad, automatically resolving network issues, and the free tier is sufficient for personal use.

1. First, **fork** a copy of the code.
2. Go to [Zeabur](https://zeabur.com?referralCode=deanxv), log in using GitHub, and enter the console.
3. In Service -> Add Service, select Git (authorization is required for the first use), and select your forked repository.
4. Deployment will start automatically; cancel it first.
5. Add environment variables:

`LA_COOKIE=******`  cookie (separate multiple cookies with commas)

`CF_CLEARANCE=******`

`API_SECRET=123456` [Optional] API key - modify this value for request header verification (separate multiple keys with commas) (same usage as openai-API-KEY)

Save.

6. Select Redeploy.

</div>
</details> </div>


</details>

<details>
<summary><strong>Deploy to Render</strong></summary>
<div>

> Render provides a free tier; you can further increase your quota after adding a payment method.

Render can directly deploy Docker images without forking the repository: [Render](https://dashboard.render.com)

</div>
</details>

## Configuration

### Environment Variables

1. `PORT=10088` [Optional] Port, defaults to 10088
2. `DEBUG=true` [Optional] DEBUG mode, prints more information [true: enable, false: disable]
3. `API_SECRET=123456` [Optional] API key - modify this value for the Authorization header (same as API-KEY) (separate multiple values ​​with commas)
4. `LA_COOKIE=******` cookie (separate multiple values ​​with commas)
5. `CF_CLEARANCE=******` Cloudflare clearance value, used to bypass Cloudflare verification
6. `REQUEST_RATE_LIMIT=60` [Optional] Request rate limit per minute per IP address, default: 60 requests/min
7. `PROXY_URL=http://127.0.0.1:10801` [Optional] Proxy
8. `ROUTE_PREFIX=hf` [Optional] Route prefix, defaults to empty. Example API endpoint after adding this variable: `/hf/v1/chat/completions`

### How to obtain cookies

1. Open [lmarena](https://beta.lmarena.ai/).
2. Open **F12** developer tools.
3. Conduct a conversation.
4. As shown in the image below, the `cf_clearance` value in the `cookie` header of the `create-evaluation` interface on the right (highlighted in blue) is the required `CF_CLEARANCE` environment variable value, and the `arena-auth-prod-v1` value (highlighted in red) is the required `LA_COOKIE` environment variable value. ![img.png](docs/img.png)
## Advanced Configuration

(Omitted)

## Supported Models

### Conversational Models

| Model Name                                    |
|-----------------------------------------|
| chatgpt-4o-latest-20250326              |
| gpt-4.1-2025-04-14                      |
| gpt-4.1-mini-2025-04-14                 |
| claude-3-5-haiku-20241022               |
| claude-3-5-sonnet-20241022              |
| claude-3-7-sonnet-20250219              |
| claude-3-7-sonnet-20250219-thinking-32k |
| claude-opus-4-20250514                  |
| claude-sonnet-4-20250514                |
| gemini-2.0-flash-001                    |
| gemini-2.5-flash-preview-04-17          |
| gemini-2.5-pro-preview-05-06            |
| gemma-3-27b-it                          |
| llama-3.3-70b-instruct                  |
| llama-4-maverick-03-26-experimental     |
| llama-4-maverick-17b-128e-instruct      |
| amazon.nova-pro-v1:0                    |
| command-a-03-2025                       |
| deepseek-v3-0324                        |
| grok-3-mini-beta                        |
| grok-3-preview-02-24                    |
| mistral-medium-2505                     |
| o3-2025-04-16                           |
| o3-mini                                 |
| o4-mini-2025-04-16                      |
| qwen-max-2025-01-25                     | qwen3-30b-a3b
qwen3-235b-a22b
qwq-32b

### Image Generation Models

| Model Name|
|-------------------------------------------|
| dall-e-3                                  |
| gpt-image-1                               |
| gemini-2.0-flash-preview-image-generation |
| imagen-3.0-generate-002                   |
| flux-1.1-pro                              |
| ideogram-v2                               |
| photon                                    |
| recraft-v3                                |


## Troubleshooting

[Omitted]

## Others

[Omitted]
