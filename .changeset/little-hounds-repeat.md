---
"@cloudflare/think": patch
---

Return attachment data unchanged when a chat adapter resolves `fetchData` to an `ArrayBuffer` instead of a `Buffer`.

`toMessengerAttachment` assumed `fetchData` always resolves to a `Buffer` and reached for `data.buffer`, `data.byteOffset`, and `data.byteLength` to copy out the view's bytes. `chat` widened `Attachment.fetchData` to `() => Promise<Buffer | ArrayBuffer>` within the `^4.31.0` range Think already declares, so on a release in that range the conversion no longer typechecks and an adapter that hands back a plain `ArrayBuffer` throws inside the attachment's `fetch()` closure rather than delivering the bytes. An `ArrayBuffer` is now returned as-is, and the existing view-copy path is unchanged.
