# Voice Reply

Send a voice message instead of text. Uses text-to-speech to synthesize your response and deliver it as a Telegram voice note.

## When to Use

- User says "say this", "tell me out loud", "reply with voice", "send voice message", "voice note", or "read this to me"
- You want to deliver a greeting, short update, or personal touch as audio
- User explicitly asks for audio/spoken response

## How

Call `mcp__nanoclaw__send_voice` with the text you want spoken.

```
mcp__nanoclaw__send_voice(text: "Hey Shintaro, just finished that research. Check your messages!")
```

## Guidelines

- Keep text under 500 characters — voice notes should be brief and conversational
- Write naturally as if speaking — contractions, casual tone, no markdown or formatting
- Don't include URLs, code, bullet points, or structured text — those belong in regular messages
- For longer content, send a text message AND a short voice summary
- The voice is English (US, male). Write text that sounds natural when spoken aloud
- You can still send a text message before or after the voice note for context
