# 🔨 @itsliaaa/starforge

[![Logo](https://files.catbox.moe/wbv9fk.png)](https://www.npmjs.com/package/@itsliaaa/starforge)

<p align="center">
   A toolkit for building WhatsApp bots with Zapo.
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

### 📋 Table of Content
  - [⚠️ Notice](#%EF%B8%8F-notice)
  - [📥 Installation](#-installation)
  - [🧩 Example](#-example)
  - [📄 Serialized Message](#-serialized-message)
  - [✉️ Sending Message](#%EF%B8%8F-sending-message)
    - [💭 Text](#-text)
    - [😄 Reaction](#-reaction)
    - [📰 Link Preview](#-link-preview)
    - [🖼️ Media](#%EF%B8%8F-media)
    - [🗒️ Sticker](#%EF%B8%8F-sticker)
    - [👤 Contact](#-contact)
    - [📦 Sticker Pack](#-sticker-pack)
    - [🖼️ Album](#%EF%B8%8F-album)
    - [📊 Poll](#-poll)
    - [📋 Poll Result](#-poll-result)
    - [🗄️ Interactive](#%EF%B8%8F-interactive)
    - [🔘 Legacy Button](#-legacy-button)
    - [📋 Legacy List](#-legacy-list)
    - [✨ Rich](#-rich)
    - [🧰 Additional Options](#-additional-options)
  - [👤 Chats](#-chats)
    - [rejectCall](#rejectcallcallid-string-callcreatorjid-string)
    - [resolveUserJid](#resolveuserjidjid-string)
    - [updateMemberLabel](#updatememberlabeljid-string-label-string)
    - [setChatEphemeral](#setchatephemeraljid-string-durationsecs-number)
  - [❤️ Credits](#%EF%B8%8F-credits)
  - [📄 License](#-license)

### ⚠️ Notice

This project is simply a toolkit for building WhatsApp bots using Zapo, and will be used for [@itsliaaa/starseed](https://github.com/itsliaaa/starseed#readme).

### 📥 Installation

```bash
npm install @itsliaaa/starforge magic-bytes.js qr sharp zapo-js
```

- `qr` is used by the `encodeQR()` function.
- `magic-bytes.js` is used by the `detectFileType()` function.
- `sharp` is used for image processing tasks such as generating thumbnails, creating favicons, `createMediaProcessor()`, and more. Alternatively, you can install `@napi-rs/image` or `jimp`.

### 🧩 Example

Here's a simple example using Zapo.

```javascript
import { WaClient, createStore } from 'zapo-js'
import { createMediaProcessor, createSerializer, encodeQR, extendSocket } from '@itsliaaa/starforge'

const store = createStore()
const processor = createMediaProcessor()

const client = new WaClient({
  store,
  sessionId: 'main',
  media: { processor }
})

// Extend the client immediately after creating it
extendSocket(client)

// Create the serializer
const serialize = createSerializer(client)

client.on('auth_qr', async ({ qr }) => {
  const { ascii } = await encodeQR(qr)
  console.log('📷 Scan this QR', ascii)
})

client.on('connection', ({ status }) => {
  if (status !== 'open') return
  console.log('✅ Connected to WhatsApp')
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

### 📃 Serialized Message

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
      text: '@itsliaaa/starforge',
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
  isMedia: false,
  type: 'extendedTextMessage',
  msg: e {
    endCardTiles: [],
    text: '@itsliaaa/starforge',
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
    text: '@itsliaaa/starforge',
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
    isMedia: false,
    type: 'conversation',
    fakeObj: { key: [Object], message: [e] },
    reply: [AsyncFunction: replyMessage],
    react: [AsyncFunction: reactMessage],
    getProfilePicture: [AsyncFunction: getProfilePicture]
  },
  expiration: 604800,
  mentionedJid: [],
  text: '@itsliaaa/starforge',
  reply: [AsyncFunction: replyMessage],
  react: [AsyncFunction: reactMessage],
  getProfilePicture: [AsyncFunction: getProfilePicture]
}
```

### ✉️ Sending Message

> 📕 Note: You must call `extendSocket(client)` before using any of the following functions.

#### 💭 Text

`sendText(jid: string, rawText: string, quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendText(jid, 'Hello 👋🏻', m)

// Send as a group status with a custom font color, background color, and font style
client.sendText(jid, 'Hello 👋🏻', m, {
   // RGB: 230, 230, 250
   fontColor: '#E6E6FA',

   // RGB: 75, 0, 130
   backgroundColor: '#4B0082',

   // MORNINGBREEZE_REGULAR
   fontType: 7
}, {
   groupStatus: true
})
```

#### 😄 Reaction

`sendReact(jid: string, rawEmoji: string, target?: object, options?: object)`

```javascript
client.sendReact(jid, '🫪', m.key)

// You can also react to a group status
client.sendReact(jid, '🫪', m.key, { groupStatus: true })
```

#### 📰 Link Preview

`sendAdText(jid: string, rawText: string, quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendAdText(jid, 'Link Preview 🌱', m, {
  title: 'Interesting Article!',
  description: 'See more...',
  thumbnail: /* Buffer | string | Readable */,
  favicon: /* Buffer | string | Readable */,
  largeThumbnail: true,
  width: 1920,
  height: 1080
})
```

#### 🖼️ Media

`sendMedia(jid: string, source: Buffer | string | Readable, rawText: string, quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendMedia(jid, 'https://files.catbox.moe/jtofzb.jpeg', '🍂', m)

// Force the media type
client.sendMedia(jid, 'https://files.catbox.moe/jtofzb.jpeg', '🍂', m, {
  document: true,
  audio: false,
  ptt: false,
  ptv: false,
  gifPlayback: false,
  fileName: 'Nature.jpeg',
  mimetype: 'image/jpeg'
})

// Send as a group status with Close Friends
// Works with images, videos, and audio
client.sendMedia(jid, 'https://files.catbox.moe/jtofzb.jpeg', '🍂', m, null, {
  groupStatus: true,
  closeFriends: {
    name: 'To My Friends!',
    emoji: '🍅'
  }
})
```

#### 🗒️ Sticker

`sendSticker(jid: string, source: Buffer | string | Readable, quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendSticker(jid, 'https://files.catbox.moe/jtofzb.jpeg', m)

// Add an exclusive metadata
client.sendSticker(jid, 'https://files.catbox.moe/jtofzb.jpeg', m, {
  isAiSticker: true,
  premium: 0,
  name: '@itsliaaa/starforge',
  publisher: 'Stellar'
})
```

#### 👤 Contact

`sendContact(jid: string, contacts?: object[], quote?: object, options?: object)`

```javascript
client.sendContact(jid, [{
  name: 'James J. Jonah',
  org: 'Daily Bugle',
  email: 'james.jonah@example.com',
  website: 'https://example.com',
  location: 'New York, USA',
  other: '',
  number: '+1 555 123 4567'
}], m)

// You can also send multiple contacts at once
client.sendContact(jid, [{
  name: 'James J. Jonah',
  org: 'Daily Bugle',
  email: 'james.jonah@example.com',
  website: 'https://example.com',
  location: 'New York, USA',
  other: '',
  number: '155512345678'
}, {
  name: 'Peter Parker',
  org: 'Freelance Photographer',
  email: 'peter.parker@example.com',
  website: '',
  location: 'New York, USA',
  other: '',
  number: '155598765432'
}], m)
```

#### 📦 Sticker Pack

`sendStickerPack(jid: string, sources?: (Buffer | string | Readable)[], quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendStickerPack(jid, [
  'https://files.catbox.moe/jtofzb.jpeg',
  'https://files.catbox.moe/jtofzb.jpeg'
], m, {
  name: 'My Sticker Pack 📦',
  publisher: 'Stellar',
  description: 'Limited Sticker!'
})
```

#### 🖼️ Album

`sendAlbum(jid: string, sources?: object[], quote?: object, options?: object)`

```javascript
client.sendAlbum(jid, [{
  media: /* Buffer | string | Readable */,
  caption: '🌱 Album Message'
}, {
  media: /* Buffer | string | Readable */,
  caption: '🌱 Album Message'
}], m)
```

#### 📊 Poll

`sendPoll(jid: string, rawText: string, selections: string[] | object[], quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendPoll(jid, '📊 Choose your favorite language', [
  'JavaScript',
  'Python',
  'Rust'
], m, {
  announcementGroup: false,
  multiSelect: false,
  hideVoter: true,
  endTime: Date.now() + 86_400_000,
  canAddOption: false
})
```

#### 📋 Poll Result

`sendPollResult(jid: string, rawText: string, selections: string[] | object[], quote?: object, options?: object)`

```javascript
client.sendPollResult(jid, '📋 Poll Results', [{
  name: 'JavaScript',
  count: 20
}, {
  name: 'Python',
  count: 18
}, {
  name: 'Rust',
  count: 22
}], m)
```

#### 🗄️ Interactive

`sendInteractive(jid: string, rawButtons?: object[], quote?: object, extraContent?: object, options?: object)`

```javascript
// You can add "icon" to each button to use a custom button icon
const EXAMPLE_BUTTONS = [{
  text: '👉🏻 Click Me',
  id: 'command_id'
}, {
  text: '📃 Copy Code',
  copy: '@itsliaaa/starforge'
}, {
  text: '🌐 Open URL',
  url: 'https://www.npmjs.com/package/@itsliaaa/starforge',
  isPaymentPreview: false,
  useWebview: true
}, {
  text: '📞 Call',
  call: '6281111111111'
}, {
  title: '👉🏻 Tap Here',
  sections: [{
    title: '🧩 Interesting Menu',
    highlight_label: 'Popular',
    rows: [{
      header: '',
      title: '⁉️ Coupon',
      description: '',
      id: 'free_coupon_id'
    }]
  }]
}]

client.sendInteractive(jid, EXAMPLE_BUTTONS, m, {
  text: '🗄️ Interactive Message',
  footer: '@itsliaaa/starforge'
})

// Send with a media header
client.sendInteractive(jid, EXAMPLE_BUTTONS, m, {
  media: /* Buffer | string | Readable */,
  text: '🗄️ Interactive Message'
})

// Send with a location header
client.sendInteractive(jid, EXAMPLE_BUTTONS, m, {
  location: {
    name: '📍 Location Header',
    address: '@itsliaaa/starforge'
  },
  media: /* Buffer | string | Readable */,
  text: '🗄️ Interactive Message'
})

// Send with a product header
client.sendInteractive(jid, EXAMPLE_BUTTONS, m, {
  product: {
    title: '🛒 Product Header',
    businessOwnerJid: '6281111111111@s.whatsapp.net'
  },
  media: /* Buffer | string | Readable */,
  text: '🗄️ Interactive Message'
})

// Additional options
client.sendInteractive(jid, EXAMPLE_BUTTONS, m, {
  media: /* Buffer | string | Readable */,
  title: '✨ Using Various Options',
  text: '🗄️ Interactive Message',

  // Force header type
  document: false,
  location: false,
  product: false,

  // Wrap all buttons in a single option
  optionText: '👉🏻 Tap Here',
  optionTitle: '🧩 Wrapped Buttons',

  // Limited time offer
  offerText: '🔖 Limited Time Offer',
  offerCode: '@itsliaaa/starforge',
  offerUrl: 'https://www.npmjs.com/package/@itsliaaa/starforge',
  offerExpiration: Date.now() + 86_400_000
})
```

#### 🔘 Legacy Button

`sendLegacyButton(jid: string, rawButtons: object[], quote?: object, extraContent?: object, options?: object)`

```javascript
// --- Regular buttons message
client.sendLegacyButton(jid, [{
  text: '👋🏻 SignUp',
  id: '#SignUp'
}], m, {
  text: '👆🏻 Buttons!',
  footer: '@itsliaaa/starforge',

  // Optional, change to "true" if want proper render on WhatsApp Web
  viewOnce: false
})

// --- Buttons with Media & List
client.sendLegacyButton(jid, [{
  text: '👋🏻 Rating',
  id: '#Rating'
}, {
  text: '📋 Select',
  sections: [{
    title: '✨ Section 1',
    rows: [{
      header: '',
      title: '💭 Secret Ingredient',
      description: '',
      id: '#SecretIngredient'
    }]
  }, {
    title: '✨ Section 2',
    highlight_label: '🔥 Popular',
    rows: [{
      header: '',
      title: '🏷️ Coupon',
      description: '',
      id: '#CouponCode'
    }]
  }]
}], m, {
  media: /* Buffer | string | Readable */,
  text: '👆🏻 Buttons and List!',
  footer: '@itsliaaa/starforge'
})
```

#### 📋 Legacy List

`sendLegacyList(jid: string, rawSections: object[], quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendLegacyList(jid, [{
  title: '🚀 Menu 1',
  rows: [{
    title: '✨ AI',
    description: '',
    id: '#AI'
  }]
}, {
  title: '🌱 Menu 2',
  rows: [{
    title: '🔍 Search',
    description: '',
    id: '#Search'
  }]
}], m, {
  text: '📋 List!',
  footer: '@itsliaaa/starforge',
  buttonText: '📋 Select',
  title: '👋🏻 Hello'
})
```

#### ✨ Rich

`sendRich(jid: string, rawSections: object[], quote?: object, extraContent?: object, options?: object)`

```javascript
client.sendRich(jid, [{
  text: '# 🔨 @itsliaaa/starforge\n\n---\n',
}, {
  language: 'javascript',
  code: `console.log("Hello World")`
}, {
  title: 'The Table',
  table: [{
    isHeading: true,
    items: ['', 'Node.js', 'Bun', 'Deno']
  }, {
    isHeading: false,
    items: ['Engine', 'V8 (C++)', 'JavaScriptCore (C++)', 'V8 (C++)']
  }, {
    isHeading: false,
    items: ['Performance', '4/5', '5/5', '4/5']
  }]
}, {
  extWidget: [{
    title: '📋 Section 1',
    buttons: ['menu', 'label', 'infos']
  }, {
    title: '📄 Section 2',
    buttons: ['gif', 'runtime', 'order']
  }],
  canScroll: false
}, {
  // When adding an HTML primitive, set "disableEdit" to true if it causes lag or device stuttering
  htmlPayload: `<h1>🔨 @itsliaaa/starforge</h1><p>A Baileys wrapper designed to make WhatsApp bot development simpler, cleaner, and more flexible.</p>`,
  trustedSources: ['https://github.com/itsliaaa/starforge']
}, {
  video: 'https://path-to-video.com/',
  thumbnailUrl: 'https://path-to-tiny-image.com/',
  mime: 'video/mp4',
  fileLength: 13_603,
  duration: 60
}, {
  image: 'https://path-to-image.com/',
  mime: 'image/jpeg'
}, {
  imagine: 'https://path-to-image.com/',
  mime: 'image/jpeg'
}, {
  reels: [{
    reelUrl: 'https://path-to-web.com/',
    thumbnailUrl: 'https://path-to-image.com/',
    creator: 'Lia Wynn',
    avatarUrl: 'https://path-to-tiny-image.com/',
    title: 'Simple Zapo Helper',
    likesCount: 1,
    sharesCount: 1,
    viewCount: 1,
    source: 'https://path-to-web.com/',
    isVerified: true
  }]
}, {
  posts: [{
    caption: 'A Zapo Helper',
    title: '',
    subtitle: '',
    creator: 'Lia Wynn',
    avatarUrl: 'https://path-to-tiny-image.com/',
    thumbnailUrl: 'https://path-to-image.com/',
    likesCount: 1,
    commentsCount: 1,
    sharesCount: 1,
    postUrl: 'https://path-to-web.com/',
    deepLink: '',
    footerLabel: '',
    footerIcon: '',
    sourceApp: 'FACEBOOK',
    orientation: 'LANDSCAPE',
    type: 'IMAGE',
    isVerified: true,
    isCarousel: false
  }]
}, {
  title: 'Starseed Premium Script',
  brand: 'Starseed',
  price: 'Rp 150.000',
  salePrice: 'Rp 75.000',
  productUrl: 'https://path-to-web.com/',
  imageUrl: 'https://path-to-image.com/',
  additionalImages: [{
      url: 'https://path-to-tiny-image.com/'
  }]
}, {
  products: [{
    title: 'Starseed Premium Script',
    brand: 'Starseed',
    price: 'Rp 150.000',
    salePrice: 'Rp 75.000',
    productUrl: 'https://path-to-web.com/',
    imageUrl: 'https://path-to-image.com/'
  }, {
    title: 'Self-Bot Script',
    brand: 'Starseed',
    price: 'Rp 50.000',
    productUrl: 'https://path-to-web.com/',
    imageUrl: 'https://path-to-image.com/',
    additionalImages: [{
      url: 'https://path-to-tiny-image.com/'
    }]
  }]
}, {
  latex: 'https://quicklatex.com/cache3/82/ql_0676ade0cd04eda37aeb3d0bcd427682_l3.png',
  expression: 'x^2 + 2x + 1',
  mime: 'image/png',
  width: 603,
  height: 111,
  fontHeight: 83.5,
  padding: 15
}, {
  text: '- Citation:',
  entities: [{
    title: 'Example of Citation',
    citationUrl: 'https://wa.me/0',
    displayName: '@itsliaaa/starforge'
  }]
}, {
  text: '- Inline Link:',
  entities: [{
    inlineUrl: 'https://wa.me/0',
    displayName: '@itsliaaa/starforge',
    isTrusted: true
  }]
}, {
  text: '- LaTeX:',
  entities: [{
    expression: 'x^2 + 2x + 1',
    latex: 'https://quicklatex.com/cache3/82/ql_0676ade0cd04eda37aeb3d0bcd427682_l3.png',
    width: 603,
    height: 111,
    fontHeight: 83.5,
    padding: 15
  }]
}, {
  suggestion: '@itsliaaa/starforge'
}, {
  suggestions: ['@itsliaaa/starforge', 'Zapo Helper', 'Zapo']
}, {
  suggestions: ['@itsliaaa/starforge', 'Rich Response', 'Scroll Layout'],
  canScroll: true
}, {
  tip: '@itsliaaa/starforge'
}, {
  foaText: '# 🔥 LARGE Text'
}, {
  actionUrls: [{
    text: '💰 Donate Me!',
    url: 'https://saweria.co/itsliaaa'
  }, {
    text: '🌐 Google',
    url: 'https://www.google.com/'
  }]
}, {
  searchResults: [{
    displayName: 'Simple Zapo Helper',
    sourceUrl: 'https://path-to-web.com/',
    faviconUrl: 'https://path-to-tiny-image.com/',
    mime: 'image/jpeg'
  }]
}], m, {
  notify: false,
  disclaimerText: 'Example Usage of sendRich()',
  disableEdit: false,
  disableForward: false,
  forceAsFooter: false
})
```

#### 🧰 Additional Options

> 💡 Tip: You can use the following additional options in the `options` parameter of every function returned by `extendSocket()`.

```javascript
// The message will disappear after 1 second when you open the chat
client.sendText(jid, '🗄️ Secret Password: *4640*', m, null, {
  readTimeout: 1
})

// The message will be sent as a group status
client.sendText(jid, 'Group Status ✨', null, null, {
  groupStatus: true,

  // Optional, use this if you want to enable Close Friends
  closeFriends: {
    name: 'To My Friends!',
    emoji: '🍅'
  }
})
```

### 👤 Chats

#### `rejectCall(callId: string, callCreatorJid: string)`

#### `resolveUserJid(jid: string)`

#### `updateMemberLabel(jid: string, label: string)`

#### `setChatEphemeral(jid: string, durationSecs: number)`

### ❤️ Credits

<!-- Please do not replace my name with yours. It's disrespectful. -->

**This project is created and maintained by [Lia Wynn](https://github.com/itsliaaa)**

Thanks to the Zapo maintainers and contributors for providing an amazing and modern TypeScript library for interacting with the WhatsApp Web API.

Please do not remove or alter the original credits, copyright notices, or attributions.

### 📄 License

This library is licensed under the [Apache License 2.0](LICENSE)