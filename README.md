# Lightning Wallet Connect

This project includes web components for connecting to Lightning Wallets and enabling [WebLN](https://webln.guide). Websites only need to implement a single interface to connect with multiple wallets (WebLN), and users can connect from both desktop and mobile devices. These components work with pure HTML and all Javascript libraries frameworks such as React, Angular, Vue, Solid.js, etc.

## 🚀 Quick Start

```
npm install @getalby/lightning-wallet-connect
```

or

```
yarn add @getalby/lightning-wallet-connect
```

or for use without any build tools:

```
<script src="https://cdn.jsdelivr.net/npm/@getalby/lightning-wallet-connect@1.0.5/dist/index.browser.js"></script>
```

## 📽️ Demo

https://user-images.githubusercontent.com/33993199/234830578-0baf25f9-0179-4244-941c-0c558c613a7a.mov

## 🤙 Usage

Lightning wallet connect exposes the following web components for allowing user to connect their desired Lightning wallet:

- `<lwc-button/>` - launches the LWC Modal on click
  - Optional Arguments:
    - `icon-only` - display the button as an icon without "Connect wallet"
    - `disabled` - mark the button as disabled. _NOTE: in react disabled={false} will not work - attribute must be omitted_
- `<lwc-modal/>` - render the modal on its own
- `<lwc-connector-list/>` - render the list of connectors on their own
- _more components coming soon_

Lightning wallet connect exposes the following events:

- `lwc:connected` window event which fires when a wallet is connected and window.webln is ready to use
- `lwc:connecting` window event which fires when LWC is connecting to a wallet
- `lwc:disconnected` window event which fires when user has disconnected from their wallet
- `lwc:modalopened` window event which fires when Lightning Wallet Connect modal is opened
- `lwc:modalclosed` window event which fires when Lightning Wallet Connect modal is closed

Current wallets supported:

- [Alby Browser extension] (https://getalby.com)
- [Alby NWC](https://nwc.getalby.com)
- [Generic NWC URL](https://github.com/nostr-protocol/nips/blob/master/47.md)

### Styling

- the following attributes can be configured as hex or rgb: `color-gradient1`, `color-gradient2`, `color-primary`, `color-secondary`

### Pure HTML

> Example codepen: https://codepen.io/rolznz/pen/ZEmXGLd

```html
<html>
  <body>
    <lwc-button></lwc-button>
    <script src="https://cdn.jsdelivr.net/npm/@getalby/lightning-wallet-connect@1.0.5/dist/index.browser.js"></script>
    <script>
      window.addEventListener('lwc:connected', async () => {
        // TODO: hide the lwc-button
        const invoice = // (...invoice generated by backend)
          await window.webln.sendPayment(invoice);
        confetti();
      });
    </script>
  </body>
</html>
```

### React

> Example replit: https://replit.com/@rolznz/make-me-an-image-lwc-version

```tsx
import '@getalby/lightning-wallet-connect';

// in your component, listen to lightning wallet connected event
const [lwcConnected, setLwcConnected] = React.useState(false);

React.useEffect(() => {
  const onConnected = () => setLwcConnected(true);
  window.addEventListener('lwc:connected', onConnected);

  return () => {
    window.removeEventListener('lwc:connected', onConnected);
  };
}, []);

const invoice = // (...invoice generated by backend)

return lwcConnected ? <>
    <button onClick={() => window.webln.sendPayment(invoice)}/>
  </> : <lwc-button/>;
```

# Demos

Open [demos](demos/README.md)

# 🛠️ Development

## Install

Run `yarn install && (cd dev/vite && yarn install)`

## Run Vite

Run `yarn dev`

## Other dev options

Open [dev](dev/README.md)

## Production Build

`yarn build`

### Build (Watch mode - no pure html support)

`yarn dev:build`

### Build (Watch mode - with pure html support)

`yarn dev:build:browser`

## Testing

`yarn test`

## Need help?

We are happy to help, please contact us or create an issue.

- [Twitter: @getAlby](https://twitter.com/getAlby)
- [Telegram group](https://t.me/getAlby)
- support at getalby.com
- [bitcoin.design](https://bitcoin.design/) Discord community (find us on the #alby channel)
- Read the [Alby developer guide](https://guides.getalby.com/overall-guide/alby-for-developers/getting-started) to better understand how Alby packages and APIs can be used to power your app.

# 🔥 Lit

This project is powered by Lit.

See [Get started](https://lit.dev/docs/getting-started/) on the Lit site for more information.

## License

[MIT](./LICENSE)
