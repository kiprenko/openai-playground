# GPT-4 Playground 1: History teacher

## Conversation
### Input 1
The model is whisper-1, let's convert an audio note that I took today into a text. The note is in Ukranian.
```bash
curl https://api.openai.com/v1/audio/transcriptions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: multipart/form-data" \
  -F file=@audio-note-in-ukranian.m4a \
  -F model=whisper-1
```

### Output 1
Pretty good result. Though it has some issues, mostly due to my pronunciation.
```JSON
{"text":"Крім тої ідеї, яка в мене є щодо створення агенту, який буде експертом з нерухомості в країні Басків. Безусловно, цей агент не потрібен мені для пошуку житла. Мені здається, це гарна ідея, так як це більш-менш цікава і складна галузь. І потестувати, погадатися, подивитися, як різні матеріали відповідають. Також можна зробити якогось ботап для агента, який буде працювати не з текстом, а з, наприклад, картинками. Тому що, якщо подивитися OpenAPI Platform, тут у них в описі є те, що вони можуть приймати текст, фотографії для комп'ютерного бачення. І там різні інші штуки. І от можна, наприклад, зробити якийсь API, не знаю, на Бумі, Джаві або на Пайтені, де ти завантажуєш якийсь файлик і він, наприклад, тобі щось про нього каже. Можна було б спробувати щось зробити на кшталт дизайнів інтер'єрів. Ти його завантажуєш і каже, дивись, от тобі такий інтер'єр. От така квартира, наприклад, кімната. І скажи мені, як я її можу прокастити, що мені треба зробити, щоб вона стала сучасною, то, наприклад, в стилі сучасної фермерської родини."}
```

### Input 2
Everything is the same as previously, but let's add a prompt to try to make the result cleaner.
```bash
curl https://api.openai.com/v1/audio/transcriptions \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: multipart/form-data" \
  -F file=@audio-note-in-ukranian.m4a \
  -F model=whisper-1 \
  -F prompt="This is an audio note I took today. It contains some thoughts I had related to an application I could make to hone my skills in work with OpenAI platform."
```

### Output 2
A bit different result. More conversational now, but made some new errors (e. g. instead of "на Бумі, Джаві або на Пайтені", now it is "на бомбі джаві або на пайтені")
```JSON
{"text":"Крім тої ідеї, яка в мене є щодо створення агенту, який буде експертом з нерухомості в країні Басків. Безусловно, цей агент не потрібен мені для пошуку житла. Просто, мені здається, гарна ідея, так як це більш-менш цікава і складна галузь. І потестувати, погадатися, подивитися, як різні матеріали відповідають. Також можна зробити якогось bot-up для агента, який буде працювати не з текстом, а з, наприклад, картинками. Тому що, якщо подивитися OpenAPI platform, тут у них в описі є те, що вони можуть приймати текст, фотографії для комп'ютерного бачення. І там різні інші штуки. І от можна, наприклад, зробити якийсь API, не знаю, на бомбі джаві або на пайтені, де ти завантажуєш якийсь файлик і він, наприклад, тобі щось про нього каже. Можна було б спробувати щось зробити на кшталт дизайнів інтер'єрів. Ти його завантажуєш і каже, дивись, тобі такий інтер'єр. От така квартира, наприклад, кімната. І скажи мені, як я її можу прокастити, що мені треба зробити, щоб вона стала сучасною, то, наприклад, в стилі сучасної фермерської родини."}
```

### Input 3
Let's send the last transcription to ChatGPT in order to get it structured. 
```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-4",
    "messages": [
      {"role": "system", "content": "You help summarize voice message transcriptions. Compress or paraphrase the users text to make it shorter and clearer. Obviously they may have some errors, try to get rid of them."},
      {"role": "user", "content": "Крім тої ідеї, яка в мене є щодо створення агенту, який буде експертом з нерухомості в країні Басків. Безусловно, цей агент не потрібен мені для пошуку житла. Просто, мені здається, гарна ідея, так як це більш-менш цікава і складна галузь. І потестувати, погадатися, подивитися, як різні матеріали відповідають. Також можна зробити якогось bot-up для агента, який буде працювати не з текстом, а з, наприклад, картинками. Тому що, якщо подивитися OpenAPI platform, тут у них в описі є те, що вони можуть приймати текст, фотографії для компютерного бачення. І там різні інші штуки. І от можна, наприклад, зробити якийсь API, не знаю, на бомбі джаві або на пайтені, де ти завантажуєш якийсь файлик і він, наприклад, тобі щось про нього каже. Можна було б спробувати щось зробити на кшталт дизайнів інтерєрів. Ти його завантажуєш і каже, дивись, тобі такий інтерєр. От така квартира, наприклад, кімната. І скажи мені, як я її можу прокастити, що мені треба зробити, щоб вона стала сучасною, то, наприклад, в стилі сучасної фермерської родини."}
    ],
    "temperature": 0.7,
    "max_tokens": 512
  }'
```

### Output 3
Cool result, I like it.
```JSON
{
  "id": "chatcmpl-BOB3hyCLvGCGSfTEin04Iz1eXOZqD",
  "object": "chat.completion",
  "created": 1745102081,
  "model": "gpt-4-0613",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "I have an idea to create an AI agent expert in Basque country real estate. It's not for personal house hunting, but to explore this complex industry. We could also create a bot that works with images, not just text. Using OpenAPI platform, which supports text and photos for computer vision, we could make an API that processes image files. For instance, it could analyze interior designs - you upload a room's photo and it suggests how to modernize it, maybe in a contemporary farmhouse style.",
        "refusal": null,
        "annotations": []
      },
      "logprobs": null,
      "finish_reason": "stop"
    }
  ],
  "usage": {
    "prompt_tokens": 636,
    "completion_tokens": 103,
    "total_tokens": 739,
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