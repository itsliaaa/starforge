# Changelog

## 0.0.0-alpha.8 - 2026-09-08

- docs: add more `sendAdText()` example.
- feat: add `spoiler` boolean option *(currently not all WhatsApp versions render it)*.
- feat: add patterns to automatically enable `spoiler` based on the several message body.
- feat: support `file-type` as an alternative file type detector.
- fix: prevent `compactEntity[]` in `sendRich()` from failing to display profile pictures.
- fix: prevent `resolveContextInfo()` errors.
- refactor: improved the logical flow of `levenshtein()`.

## 0.0.0-alpha.7 - 2026-09-06

- fix: prevent `sendMedia()` from throwing errors frequently.

## 0.0.0-alpha.6 - 2026-09-06

- docs: add more `sendRich()` example.
- fix: handle `htmlPayload` correctly in `sendRich()`.
- feat: add `labels[]` and `mapItems[]` in `sendRich()`.
- feat: add configurable media processor environment variables.
- fix: use temporary files for media inputs in several FFmpeg processes.
- refactor: restructure the logical flow of `createSqliteDatabase()`.

## 0.0.0-alpha.5 - 2026-09-04

- docs: add `isAi` option example.
- docs: add more `sendLegacyButton()` option example.
- fix: optimize media processor compression.
- fix: `updateMemberLabel()` constructor invocation ([#1](https://github.com/itsliaaa/starforge/issues/1)).
- feat: support `motionThumbnail` *(Photo Live)* in `sendMedia()` and `sendAlbum()`.

## 0.0.0-alpha.4 - 2026-09-03

- feat: add `sendCarousel()`.
- feat: support `audioFooter` *(currently iOS only & not all WhatsApp versions render it)* in `sendInteractive()` and `sendCarousel()`.
- feat: support `compactEntity[]` in `sendRich()` content.
- fix: prevent serializer fallback value from being `undefined`.

## 0.0.0-alpha.3 - 2026-09-02

- refactor: adjusted `createSqliteDatabase()` logical flow.
- fix: prevent `sendMedia()` from throwing when parameters are `null` or `undefined`.
- feat: add `sendCopy()` for directly copying message content with forward metadata.

## 0.0.0-alpha.2 - 2026-09-02

- feat: add `readTimeout` to make messages disappear after being opened.
- feat: add extra options to `sendText()` for sending status, including group status.
- feat: add `createSemaphore()` functions and `Semaphore` classes.
- chore: improve `resolveUserJid()` to resolve user JIDs more accurately.
- fix: prevent `send*()` functions from throwing when parameters are `null` or `undefined`.

## 0.0.0-alpha.1 - 2026-09-01

- feat: add `send*()` helpers wrapping Zapo's `message.send()`.
- feat: add `rejectCall()`, `updateMemberLabel()`, and `setChatEphemeral()`.
- chore: simplify `createSerializer()` usage.
- chore: fix internal functions in `createMediaProcessor()`.

## 0.0.0-alpha.0 - 2026-09-25

- Initial public release.