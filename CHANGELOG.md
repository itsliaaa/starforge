# Changelog

## 0.0.0-alpha.4

- feat: add `sendCarousel()`.
- feat: support `audioFooter` *(currently iOS only & not all WhatsApp versions render it)* in `sendInteractive()` and `sendCarousel()`.
- feat: support `compactEntity[]` in `sendRich()` content.
- fix: prevent serializer fallback value from being `undefined`.

## 0.0.0-alpha.3

- refactor: adjusted `createSqliteDatabase()` logical flow.
- fix: prevent `sendMedia()` from throwing when parameters are `null` or `undefined`.
- feat: add `sendCopy()` for directly copying message content with forward metadata.

## 0.0.0-alpha.2

- feat: add `readTimeout` to make messages disappear after being opened.
- feat: add extra options to `sendText()` for sending status, including group status.
- feat: add `createSemaphore()` functions and `Semaphore` classes.
- chore: improve `resolveUserJid()` to resolve user JIDs more accurately.
- fix: prevent `send*()` functions from throwing when parameters are `null` or `undefined`.

## 0.0.0-alpha.1

- feat: add `send*()` helpers wrapping Zapo's `message.send()`.
- feat: add `rejectCall()`, `updateMemberLabel()`, and `setChatEphemeral()`.
- chore: simplify `createSerializer()` usage.
- chore: fix internal functions in `createMediaProcessor()`.

## 0.0.0-alpha.0

- Initial public release.