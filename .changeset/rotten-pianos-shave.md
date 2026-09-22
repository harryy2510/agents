---
"@cloudflare/think": minor
---

Stop discarding the messages a messenger burst skipped.

The Chat SDK runtime Think creates uses the `burst` concurrency strategy, whose contract is to run the handler once for the newest message of a run and report the earlier ones in `MessageContext.skipped`. Think's `onDirectMessage`, `onNewMention`, and `onSubscribedMessage` handlers ignored that context argument, so someone typing three quick lines had the first two thrown away and the model answered the last fragment alone. Any attachment sent on a skipped line went with them.

`ChatSdkMessengerEventInput` now carries a `skipped` array of the folded messages, oldest first, and `defaultChatSdkEvent` prepends their text to the answered message and their attachments to its attachment list before self-mention resolution runs over the result. A custom `toEvent` receives the same input and can fold them differently, or ignore them to keep the previous behaviour.
