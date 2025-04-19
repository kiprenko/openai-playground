# GPT-4 Playground 1: History teacher

## Conversation
### Input 1
Let's make a simple call to DALL-E 3 and see how he paints myself during this time.
```bash
curl https://api.openai.com/v1/images/generations \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "dall-e-3",
    "prompt": "A young man sitting at his desk on Easter Sunday, surrounded by colorful Easter decorations and traditional Ukrainian pysanky (painted eggs), deeply focused on his computer screen, experimenting with artificial intelligence models on the OpenAI platform. Outside the window it’s sunny and festive, but he stays inside, learning with curiosity and excitement. Cozy room, soft natural light, digital art style.",
    "n": 1,
    "size": "1024x1024"
  }'

```

### Output 1
Really close to the reality. But too many eggs around :D
![dall-e-3-generated-image](/dall-e-3-playground-1-output.png)

### Input 2
What 
```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4",
    "messages": [
      {"role": "system", "content": "You are an assistant that can process and analyze both text and images."},
      {"role": "user", "content": "Please describe what is shown in the image."},
      {"role": "user", "content": "<THERE WAS AN ORIGINAL URL DALL-E 3 SENT ME>"}
    ]
  }'
```

### Output 2
It didn't work :(
```JSON
{
  "id": "chatcmpl-BOBJhxUw3gDRxtJJOjyp24AZObG8X",
  "object": "chat.completion",
  "created": 1745103073,
  "model": "gpt-4-0613",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "I'm sorry, but as a text-based AI, I'm unable to process an image or URL directly. Please describe the image to me, and I'd be happy to assist further based on the information provided.",
        "refusal": null,
        "annotations": []
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 323,
    "completion_tokens": 44,
    "total_tokens": 367,
    "prompt_tokens_details": {
      "cached_tokens": 0,
      "audio_tokens": 0
    },
    "completion_tokens_details": {
      "reasoning_tokens": 0,
      "audio_tokens": 0,
      "accepted_prediction_tokens": 0,
      "rejected_prediction_tokens": 0
    }
  },
  "service_tier": "default",
  "system_fingerprint": null
}
```