---
title: Cerebras
tags:
    - cerebras
    - api
    - llm
    - serving
    - inference
---


Cerebras API: https://cloud.cerebras.ai/platform/org_v3ee433cnx3fm3jrnm8djpf3/playground?onboarding=true


API Key: <hidden>

```python

import os
from cerebras.cloud.sdk import Cerebras

client = Cerebras(
    # This is the default and can be omitted
    api_key=os.environ.get("CEREBRAS_API_KEY")
)

stream = client.chat.completions.create(
    messages=[
        {
            "role": "system",
            "content": ""
        }
    ],
    model="llama-4-scout-17b-16e-instruct",
    stream=True,
    max_completion_tokens=2048,
    temperature=0.2,
    top_p=1
)

for chunk in stream:
  print(chunk.choices[0].delta.content or "", end="")

```


```curl

curl --location 'https://api.cerebras.ai/v1/chat/completions' \
--header 'Content-Type: application/json' \
--header "Authorization: Bearer ${CEREBRAS_API_KEY}" \
--data '{
  "model": "llama-4-scout-17b-16e-instruct",
  "stream": true,
  "max_tokens": 2048,
  "temperature": 0.2,
  "top_p": 1,
  "messages": [
    {
      "role": "system",
      "content": ""
    }
  ]
}'

```

```js
import Cerebras from '@cerebras/cerebras_cloud_sdk';

const cerebras = new Cerebras({
  apiKey: process.env['CEREBRAS_API_KEY']
  // This is the default and can be omitted
});

async function main() {
  const stream = await cerebras.chat.completions.create({
    messages: [
        {
            "role": "system",
            "content": ""
        }
    ],
    model: 'llama-4-scout-17b-16e-instruct',
    stream: true,
    max_completion_tokens: 2048,
    temperature: 0.2,
    top_p: 1
  });

  for await (const chunk of stream) {
    process.stdout.write(chunk.choices[0]?.delta?.content || '');
  }
}

main();

```