# openai-playground

This repository is designed for hands-on experimentation with OpenAI API using cURL. Here, you'll find simple examples and test cases for different models and endpoints.

## How to Get Started:

1. **Sign Up**: If you don't have an OpenAI account, create one [here](https://platform.openai.com/signup).
2. **API Key**: Get your API key from your [OpenAI dashboard](https://platform.openai.com/account/api-keys).
3. **Export the API Key as an environment variable**, DO NOT COMMIT/SHOW IT ANYWHERE
   ```bash
   export OPENAI_API_KEY="your_api_key_here"
   ```
4. **cURL Commands**: The examples in this repository are written in cURL. Modify them based on your API key and test them directly from your terminal.

## Example of Calling OpenAI API with cURL:

```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4",
    "messages": [{"role": "user", "content": "Hi, may you tell me the list of most valuable Einstein discoveries?"}],
    "temperature": 0.7,
    "max_tokens": 2048
  }'
```
**where**:
* ```model``` - name of the model you want to use
* ```messages``` - history of the dialog in the format of Chat API (system, user, assistant)
* ```temperature``` - level of the creativity (0-2.0)
* ```max_tokens``` - max amount of token in the model's output
* ```top_p``` - nucleus sampling (0-1.0, default 1.0)


## Playgrounds
* [gtp-4-playground-1: history teacher](/gpt-4-playground-1-history-teacher.md)
* [whisper-1-playground-1-audio-note-to-text](/whisper-1-playground-1-audio-note-to-text.md)