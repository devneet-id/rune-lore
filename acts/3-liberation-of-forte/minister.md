# Minister

> Ask a familiar on behalf of the runite.

<!-- status: draft -->

A **familiar** is a spirit that answers. Minister carries your question to it and brings the answer back into the flow. Minister is still being shaped — its Phantasm mark is `DEVELOPMENT` today, which is not a real mark; it will move to one of the three [marks](../../glossary.md#marks-and-signs) (VOID, BETA, EXIST).

Minister reads its familiar through Keeper, so **Keeper must be engraved**.

## The familiar
A JSON file next to the runite's memory: `.echoes/<runite>/familiar.json`
```json
{"url": "https://your-familiar.example/ask", "token": "your-token", "model": "gemini"}
```
- `url` — where the question is sent. Required.
- `token` — sent as `Authorization: Bearer <token>`.
- `model` — sent with the question (default `gemini`).

Minister does **not** talk to an AI provider directly. It sends one POST with a JSON body:
```json
{"model": "gemini", "text": "What is a rune?\nTASK: ANSWER AS LESS AND TO THE POINT"}
```
and reads the answer from the reply:
```json
{"data": {"response": "..."}}
```
So the familiar is a small service of yours (or your team's) that speaks this shape. Keep `familiar.json` out of git and out of artefacts — it holds a token.

## In code
```php
Chanter::cast('ask --question', function() {
  $answer = Minister::ask(Chanter::spell('question') ?: 'What is a rune?');
  if ($answer !== false) Whisper::echo($answer . '{{nl}}');
}, 'Ask the familiar.');
```
Without a familiar:
```
$ php cast ask
[!] No spirit in your familiar to ask (engrave Keeper and fill familiar.json).
```
With a familiar that answers:
```
$ php cast ask --question="What is a rune?"
A rune is one power with one purpose. (gemini)
```
- `Minister::ask($text)` — a string or an array of lines. Returns the answer, or `false`.
- `Minister::say()` — every answer of this run, one per line.

→ Reference: [runes/minister.md](../../runes/minister.md)
