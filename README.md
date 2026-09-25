# 🔨 @itsliaaa/starforge

[![Logo](https://files.catbox.moe/wbv9fk.png)](https://www.npmjs.com/package/@itsliaaa/starforge)

<p align="center">
   A toolkit for building WhatsApp bots with Baileys and Zapo.
   <br><br>
   <a href="https://www.npmjs.com/package/@itsliaaa/starforge">
      <img src="https://img.shields.io/npm/v/@itsliaaa/starforge?style=for-the-badge&logo=npm"/>
   </a>
   <a href="https://www.npmjs.com/package/@itsliaaa/starforge">
      <img src="https://img.shields.io/npm/dm/@itsliaaa/starforge?style=for-the-badge&logo=npm"/>
   </a>
   <a href="https://github.com/itsliaaa/starforge">
      <img src="https://img.shields.io/github/stars/itsliaaa/starforge?style=for-the-badge&logo=github"/>
   </a>
   <a href="LICENSE">
      <img src="https://img.shields.io/badge/license-Apache--2.0-blue?style=for-the-badge"/>
   </a>
   <a href="https://nodejs.org">
      <img src="https://img.shields.io/badge/node-%3E%3D20-339933?logo=node.js&labelColor=green&logoColor=white&style=for-the-badge"/>
   </a>
   <a href="https://bun.sh">
      <img src="https://img.shields.io/badge/bun-%3E%3D1.3-fbf0df?logo=bun&labelColor=14151a&logoColor=white&style=for-the-badge"/>
   </a>
   <a href="#">
      <img src="https://img.shields.io/badge/ESM-only?logo=javascript&labelColor=yellow&logoColor=black&style=for-the-badge"/>
   </a>
</p>

☕ For donation: [Saweria](https://saweria.co/itsliaaa)

### ⚠️ Notice

This project is simply a toolkit for building WhatsApp bots using Baileys and Zapo, and will be used for [@itsliaaa/starseed](https://github.com/itsliaaa/starseed#readme).

### 📥 Installation

```bash
npm install @itsliaaa/starforge qr magic-bytes.js sharp
```

- `qr` is used by the `encodeQR()` function.
- `magic-bytes.js` is used by the `detectFileType()` function.
- `sharp` is used for image processing tasks such as generating thumbnails, creating favicons, `createMediaProcessor()`, and more. Alternatively, you can install `@napi-rs/image` or `jimp`.

### 🧩 Example

Here's a simple example using Zapo.

```javascript
import { WaClient } from 'zapo-js'
import { createMediaProcessor, createSerializer, encodeQR, extendSocket } from '@itsliaaa/starforge'

let serialize
const processor = createMediaProcessor()

const client = new WaClient({
   sessionId: 'main',
   media: { processor }
})

// Extend the client immediately after creating it
extendSocket(client)

client.on('auth_qr', async ({ qr }) => {
   const { ascii } = awair encodeQR(qr)
   console.log('📷 Scan this QR', ascii)
})

client.on('connection', ({ status }) => {
   if (status !== 'open') return

   // Create the serializer after the connection is established
   serialize = createSerializer(client)
})

client.on('message', async (m) => {
   // The serializer adds several properties to "m"
   await serialize(m)

   if (m.text === 'ping') {
      m.reply('🏓 Pong')
   }
})

await client.connect()
```

> 📕 Note: `serialize` can also be used with other `message_*` events, such as `message_addon`.

The following example shows the serialized message payload.

```javascript
{
  rawNode: {
    tag: 'message',
    attrs: {
      from: '120111111111111111@g.us',
      type: 'text',
      id: 'AC62067AG6D12C8741E9E0C2CE21F367',
      participant: '43411111111111@lid',
      sts: '1890322359495077',
      notify: '‮‮',
      addressing_mode: 'lid',
      expiration: '604800',
      participant_pn: '6281111111111@s.whatsapp.net',
      t: '1790322359'
    },
    content: [ [Object], [Object] ]
  },
  key: {
    remoteJid: '120111111111111111@g.us',
    id: 'AC62067AG6D12C8741E9E0C2CE21F367',
    fromMe: false,
    isGroup: true,
    isBroadcast: false,
    isNewsletter: false,
    participantAlt: '6281111111111@s.whatsapp.net',
    senderDevice: 0,
    participant: '43411111111111@lid'
  },
  stanzaType: 'text',
  offline: false,
  timestampSeconds: 1890322359,
  expirationSeconds: 604800,
  pushName: '‮‮',
  message: e {
    extendedTextMessage: e {
      endCardTiles: [],
      text: 'A',
      previewType: 0,
      contextInfo: [e],
      inviteLinkGroupTypeV2: 0
    },
    messageContextInfo: e {
      threadId: [],
      messageSecret: [Uint8Array],
      limitSharingV2: [e]
    }
  },
  id: 'AC62067AG6D12C8741E9E0C2CE21F367',
  chat: '120111111111111111@g.us',
  sender: '6281111111111@s.whatsapp.net',
  senderLid: '43411111111111@lid',
  device: 'android',
  fromMe: false,
  isGroup: true,
  isPrivate: false,
  isBroadcast: false,
  isNewsletter: false,
  type: 'extendedTextMessage',
  msg: e {
    endCardTiles: [],
    text: 'A',
    previewType: 0,
    contextInfo: e {
      mentionedJid: [],
      groupMentions: [],
      statusAttributions: [],
      stanzaId: 'ACC4C76F644FF8ECD0193D87E2380367',
      participant: '43411111111111@lid',
      quotedMessage: [e],
      expiration: 604800,
      disappearingMode: [e],
      quotedType: 0
    },
    inviteLinkGroupTypeV2: 0
  },
  quoted: {
    text: 'A',
    id: 'ACC4C76F644FF8ECD0193D87E2380367',
    chat: '120111111111111111@g.us',
    sender: '6281111111111@s.whatsapp.net',
    senderLid: '43411111111111@lid',
    device: 'android',
    fromMe: false,
    isGroup: true,
    isPrivate: false,
    isBroadcast: false,
    isNewsletter: false,
    type: 'conversation',
    fakeObj: { key: [Object], message: [e] },
    reply: [Function: replyMessage],
    react: [Function: reactMessage]
  },
  expiration: 604800,
  mentionedJid: [],
  text: 'A',
  reply: [Function: replyMessage],
  react: [Function: reactMessage]
}
```