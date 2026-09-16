---
"agents": minor
---

`createBrowserSession` accepts `guardrails` — Browser Run [hostname guardrails](https://developers.cloudflare.com/browser-run/features/guardrails/) (`allowedDomains`, `allowedDomainSets`) sent in the session-acquire body and fixed for the session's lifetime, including Live View connections. `connectBrowserSession` accepts an options object (`{ timeoutMs, onClose, onActivity }`) in place of the bare timeout number — `onClose` runs once when the session reaches a terminal state (explicit close, peer closure, or socket error), and `onActivity` fires on every CDP command sent, as an activity signal for idle tracking; the numeric form still works but is now deprecated and will be removed. The `BrowserSessionGuardrails` and `ConnectBrowserSessionOptions` types are exported from `agents/browser`.

`ConnectBrowserOptions` is now an engine-discriminated union: `browser: "kitesurf"` removes the Chromium-only options (`keepAliveMs`, `includeTargets`, `recording`) at the type level, and `browser: "chromium"` is accepted explicitly on the default arm (the `ConnectChromiumBrowserOptions` and `ConnectKitesurfBrowserOptions` arms are exported). `CdpSession` is now constructed with a `CdpSessionOptions` object (`{ timeoutMs, onClose, sessionId, onActivity }`) instead of positional arguments — relevant only if you construct one directly around your own WebSocket.
