# Capacitor E-Mail Composer

![Maintenance](https://img.shields.io/maintenance/yes/2023)
[![npm](https://img.shields.io/npm/v/capacitor-email-composer)](https://www.npmjs.com/package/capacitor-email-composer)

This Plugin is used to open a native E-Mail Composer within your Capacitor App.

<!-- DONATE -->
[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG_global.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=LMX5TSQVMNMU6&source=url)

This and other Open-Source Cordova/Capacitor Plugins are developed in my free time.
To help ensure this plugin is kept updated, new features are added and bugfixes are implemented quickly, please donate a couple of dollars (or a little more if you can stretch) as this will help me to afford to dedicate time to its maintenance.
Please consider donating if you're using this plugin in an app that makes you money, if you're being paid to make the app, if you're asking for new features or priority bug fixes.
<!-- END DONATE -->

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Content**

- [Capacitor E-Mail Composer](#capacitor-e-mail-composer)
  - [Install](#install)
    - [Consuming Published Version](#consuming-published-version)
    - [Consuming Local Version](#consuming-local-version)
  - [Updating the plugin](#updating-the-plugin)
    - [Publishing](#publishing)
  - [Usage](#usage)
    - [Attachments](#attachments)
      - [Device Storage](#device-storage)
      - [Native resources](#native-resources)
      - [Assets](#assets)
      - [Base64](#base64)
  - [API](#api)
    - [hasAccount()](#hasaccount)
    - [open(...)](#open)
    - [Interfaces](#interfaces)
      - [OpenOptions](#openoptions)
      - [Attachment](#attachment)
  - [Changelog](#changelog)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Install

### Consuming Published Version

```bash
yarn add git+https://github.com/flarehealth/capacitor-email-composer.git
yarn run cap sync
```

### Consuming Local Version

In order to make local development easier, you can link the local version of the plugin to another project. To do this you can clone the repo on your machine and use the `link` function of yarn so that you don't have to keep building the plugin and adding it in flare-mobile.

```
yarn add link:</path/to/capacitor-email-composer>
```

## Updating the plugin

If you would like to add additional functionality to this repo, you can clone this repo under the Flare Health Organization and start making changes. Once you have tested and are done with the changes, you can publish the changes and add it to Flare Mobile.

### Publishing

```
yarn verify
yarn build
```

Be sure to commit the `/dist` directory. This is needed for us to actually add the package in other projects.

## Usage

### Attachments

You can add attachments to the draft mail by using the `attachments` option in the `open(...)` method.
Every attachment needs a `type` and a `path`. If you are adding a `base64` type attachment, you also need to set the `name`:

#### Device Storage

The path to the files must be defined absolute from the root of the file system. On Android the user has to allow the app first to read from external storage!

```ts
import { EmailComposer } from 'capacitor-email-composer'

EmailComposer.open({
  attachments: [{
    type: 'absolute',
    path: 'storage/sdcard/icon.png' // Android
  }]
})
```

#### Native resources

Each app has a resource folder, e.g. the res folder for Android apps or the Resource folder for iOS apps. The following example shows how to attach the app icon from within the app's resource folder.

```ts
import { EmailComposer } from 'capacitor-email-composer'

EmailComposer.open({
  attachments: [{
    type: 'resource',
    path: 'icon.png'
  }]
})
```

#### Assets

The path to the files must be defined relative from the root of the mobile web app assets folder, which is located under the build folder.

```ts
import { EmailComposer } from 'capacitor-email-composer'

EmailComposer.open({
  attachments: [{
    type: 'asset',
    path: '/icon/favicon.png' // starting slash is important
  }]
})
```

#### Base64

The code below shows how to attach a base64 encoded image which will be added as an image. **You must set a name**.

```ts
import { EmailComposer } from 'capacitor-email-composer'

EmailComposer.open({
  attachments: [{
    type: 'base64',
    path: 'iVBORw0KGgoAAAANSUhEUgAAADwAAAA8CAYAAAA6...',
    name: 'icon.png' // this is required
  }]
})
```

## API

<docgen-index>

* [`hasAccount()`](#hasaccount)
* [`open(...)`](#open)
* [Interfaces](#interfaces)

</docgen-index>

<docgen-api>
<!--Update the source file JSDoc comments and rerun docgen to update the docs below-->

### hasAccount()

```typescript
hasAccount() => Promise<{ hasAccount: boolean; }>
```

Checks if the User can send a Mail
iOS: Check if the current Device is configured to send mail
Android: Currently does nothing

**Returns:** <code>Promise&lt;{ hasAccount: boolean; }&gt;</code>

--------------------


### open(...)

```typescript
open(options?: OpenOptions) => Promise<{ message: string; }>
```

Open the E-Mail Composer

| Param         | Type                                                | Description                            |
| ------------- | --------------------------------------------------- | -------------------------------------- |
| **`options`** | <code><a href="#openoptions">OpenOptions</a></code> | optional Options to prefill the E-Mail |

**Returns:** <code>Promise&lt;{ message: string; }&gt;</code>

--------------------


### Interfaces


#### OpenOptions

| Prop              | Type                      | Description                                                              |
| ----------------- | ------------------------- | ------------------------------------------------------------------------ |
| **`to`**          | <code>string[]</code>     | email addresses for TO field                                             |
| **`cc`**          | <code>string[]</code>     | email addresses for CC field                                             |
| **`bcc`**         | <code>string[]</code>     | email addresses for BCC field                                            |
| **`subject`**     | <code>string</code>       | subject of the email                                                     |
| **`body`**        | <code>string</code>       | email body                                                               |
| **`isHtml`**      | <code>boolean</code>      | indicates if the body is HTML or plain text (primarily iOS)              |
| **`attachments`** | <code>Attachment[]</code> | attachments that are added to the mail file paths or base64 data streams |


#### Attachment

| Prop       | Type                                                         | Description                                                                                            |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **`path`** | <code>string</code>                                          | The path of the attachment. See the docs for explained informations.                                   |
| **`type`** | <code>'absolute' \| 'resource' \| 'asset' \| 'base64'</code> | The type of the attachment. See the docs for explained informations.                                   |
| **`name`** | <code>string</code>                                          | The name of the attachment. See the docs for explained informations. Required for base64 attachements. |

</docgen-api>

## Changelog

The full Changelog is available [here](CHANGELOG.md)
