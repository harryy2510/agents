---
"@cloudflare/think": patch
---

`telegramMessenger` now accepts `nativeStreaming` and forwards it to the Telegram adapter. From `@chat-adapter/telegram` 4.38.0, native draft streaming in private chats is opt-in, and because `telegramMessenger` builds the adapter itself there was no way to turn it back on: private-chat replies always streamed by posting a placeholder and editing it. The default follows the adapter (post-and-edit), and groups keep post-and-edit because Telegram has no drafts there.

`telegramMessenger` also passes `allowUnverifiedWebhooks` when no `secretToken` is given, so `verifyWebhook: false` or a custom verifier no longer makes adapter 4.38+ throw at construction.
