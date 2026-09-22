---
"@cloudflare/think": minor
---

Let a Think agent choose how its messenger runtime handles overlapping messages.

The `Chat` instance the messenger runtime builds was created with a hardcoded `{ debounceMs: 600, strategy: "burst" }`, so every deployment paid a 600ms pause before anyone got an answer and no subclass could opt into `queue`, `concurrent`, `debounce`, or `drop`, or tune the burst window.

`Think.messengerConcurrency` now supplies that value and accepts anything the Chat SDK's `concurrency` option does. It defaults to the exported `DEFAULT_MESSENGER_CONCURRENCY`, which is the same debounced burst as before, so existing agents are unaffected. `MessengerThinkHost` carries the property as optional and the runtime falls back to the same default, leaving other implementations of that interface valid.

Note that this is separate from `messageConcurrency`, which governs submits on the agent's own chat surface rather than inbound messenger traffic.
