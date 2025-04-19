# openai-playground

This repository is designed for hands-on experimentation with OpenAI API using cURL. Here, you'll find simple examples and test cases for different models and endpoints like GPT-3.5, GPT-4, and DALL·E.

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
curl https://api.openai.com/v1/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "text-davinci-003",
    "prompt": "Translate the following English text to French: 'Hello, how are you?'",
    "max_tokens": 60
  }'
