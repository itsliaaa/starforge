# Changelog

## 0.2.2 - 2026-11-28

- perf: optimize sticker image and video conversion.
- perf: improve WebP encoding efficiency.

## 0.2.1 - 2026-11-25

- chore: increase sticker compression level.
- revert: increase animated sticker framerate from 15 to 24.

## 0.2.0 - 2026-11-25

- feat: add sticker reaction for `sendReact()`.
- feat: add audio sticker for `sendSticker()`.
- chore: increase animated sticker framerate from 15 to 24.
- chore: increase audio quality when sending mp3 and ptt.

## 0.1.0 - 2026-11-20

- fix: prevent `undefined` when resolving context info.
- fix: add ephemeral resolver when sending `FutureProofMessage` for `send*()` functions.
- feat: add `decodeHTMLEntities()`, `escapeHTML()`, and `isGroupStatus()` functions.
- refactor: improved the logical flow of `createCache()`.

## 0.0.0-alpha.14 - 2026-11-16

- feat: implement a qr encoder, reducing reliance on external dependencies.
- fix: prevent product list cannot be sent using `sendLegacyList()`.

## 0.0.0-alpha.13 - 2026-11-05

- feat: implement a custom file signature detector based on the [List of File Signatures](https://en.wikipedia.org/wiki/List_of_file_signatures), reducing reliance on external dependencies.

## 0.0.0-alpha.12 - 2026-10-29

- fix: prevent serialization errors caused by empty `quotedMessage` values.
- fix: resolve MIME type detection failures in `Request.gemini()` when processing files.
- fix: improve `sendAlbum()` compatibility with zapo-js v1.11.0+.

## 0.0.0-alpha.11 - 2026-10-28

- chore: increase default value of timeout to 60 seconds.
- chore: use `SIGTERM` instead of `SIGKILL` to terminate FFmpeg and FFprobe processes on timeout.
- chore: rename `.type` to `.msgType` in the message serializer.
- feat: add `.downloadFile()` for serialized message.
- feat: add `messageIdPrefix` and `simulatePresence` options to `extendSocket()` configuration.
- chore: add product list message example to [README.md](README.md).

## 0.0.0-alpha.10 - 2026-10-15

- fix: prevent circular references from `quoted.fakeObj` in the serializer.
- feat: support sending statuses through all functions returned by `extendSocket()`.
- feat: add `hasBotIndicator()` to detect incoming messages.

## 0.0.0-alpha.9 - 2026-10-09

- fix: support `0` and `1` values for `premium` and `isAiSticker` metadata in `sendSticker()` and `sendStickerPack()`.
- feat: support metadata rewriting for WhatsApp Lottie stickers in `sendSticker()` and `sendStickerPack()`.
- feat: support custom thumbnails for `review_and_pay` buttons in `sendInteractive()`.

## 0.0.0-alpha.8 - 2026-10-08

- docs: add more `sendAdText()` example.
- feat: add `spoiler` boolean option *(currently not all WhatsApp versions render it)*.
- feat: add patterns to automatically enable `spoiler` based on the several message body.
- feat: support `file-type` as an alternative file type detector.
- fix: prevent `compactEntity[]` in `sendRich()` from failing to display profile pictures.
- fix: prevent `resolveContextInfo()` errors.
- refactor: improved the logical flow of `levenshtein()`.

## 0.0.0-alpha.7 - 2026-10-06

- fix: prevent `sendMedia()` from throwing errors frequently.

## 0.0.0-alpha.6 - 2026-10-06

- docs: add more `sendRich()` example.
- fix: handle `htmlPayload` correctly in `sendRich()`.
- feat: add `labels[]` and `mapItems[]` in `sendRich()`.
- feat: add configurable media processor environment variables.
- fix: use temporary files for media inputs in several FFmpeg processes.
- refactor: restructure the logical flow of `createSqliteDatabase()`.

## 0.0.0-alpha.5 - 2026-10-04

- docs: add `isAi` option example.
- docs: add more `sendLegacyButton()` option example.
- fix: optimize media processor compression.
- fix: `updateMemberLabel()` constructor invocation ([#1](https://github.com/itsliaaa/starforge/issues/1)).
- feat: support `motionThumbnail` *(Photo Live)* in `sendMedia()` and `sendAlbum()`.

## 0.0.0-alpha.4 - 2026-10-03

- feat: add `sendCarousel()`.
- feat: support `audioFooter` *(currently iOS only & not all WhatsApp versions render it)* in `sendInteractive()` and `sendCarousel()`.
- feat: support `compactEntity[]` in `sendRich()` content.
- fix: prevent serializer fallback value from being `undefined`.

## 0.0.0-alpha.3 - 2026-10-02

- refactor: adjusted `createSqliteDatabase()` logical flow.
- fix: prevent `sendMedia()` from throwing when parameters are `null` or `undefined`.
- feat: add `sendCopy()` for directly copying message content with forward metadata.

## 0.0.0-alpha.2 - 2026-10-02

- feat: add `readTimeout` to make messages disappear after being opened.
- feat: add extra options to `sendText()` for sending status, including group status.
- feat: add `createSemaphore()` functions and `Semaphore` classes.
- chore: improve `resolveUserJid()` to resolve user JIDs more accurately.
- fix: prevent `send*()` functions from throwing when parameters are `null` or `undefined`.

## 0.0.0-alpha.1 - 2026-10-01

- feat: add `send*()` helpers wrapping Zapo's `message.send()`.
- feat: add `rejectCall()`, `updateMemberLabel()`, and `setChatEphemeral()`.
- chore: simplify `createSerializer()` usage.
- chore: fix internal functions in `createMediaProcessor()`.

## 0.0.0-alpha.0 - 2026-09-25

- Initial public release.