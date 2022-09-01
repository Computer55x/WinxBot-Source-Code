# Discord API Types

Simple type definitions for the [Discord API](https://discord.com/developers/docs/intro).

## Installation

Install with [npm](https://www.npmjs.com/) / [yarn](https://yarnpkg.com) / [pnpm](https://pnpm.js.org/):

```sh
npm install discord-api-types
yarn add discord-api-types
pnpm add discord-api-types
```

### Usage

You can only import this module by specifying the API version you want to target. Append `/v*` to the import path, where the `*` represents the API version. Below are some examples

```js
const { APIUser } = require('discord-api-types/v9');
```

```ts
// TypeScript/ES Module support
import { APIUser } from 'discord-api-types/v9';
```

You may also import just certain parts of the module that you need. The possible values are: `globals`, `gateway`, `gateway/v*`, `payloads`, `payloads/v*`, `rest`, `rest/v*`, `rpc`, `rpc/v*`, `utils`, `utils/v*`, `voice`, and `voice/v*`. Below are some examples

```js
const { GatewayVersion } = require('discord-api-types/gateway/v9');
```

```ts
// TypeScript/ES Module support
import { GatewayVersion } from 'discord-api-types/gateway/v9';
```

> _**Note:** The `v*` exports (`discord-api-type/v*`) include the appropriate version of `gateway`, `payloads`, `rest`, `rpc`, and `utils` you specified, alongside the `globals` exports_

### Deno

We also provide typings compatible with the [deno](https://deno.land/) runtime. You have 3 ways you can import them:

1. Directly from GitHub

```ts
// Importing a specific API version
import { APIUser } from 'https://raw.githubusercontent.com/discordjs/discord-api-types/main/deno/v9.ts';
```

2. From [deno.land/x](https://deno.land/x)

```ts
// Importing a specific API version
import { APIUser } from 'https://deno.land/x/discord_api_types/v9.ts';
```

3. From [skypack.dev](https://www.skypack.dev/)

```ts
// Importing a specific API version
import { APIUser } from 'https://cdn.skypack.dev/discord-api-types/v9?dts';
```

## Project Structure

The exports of each API version is split into three main parts:

- Everything exported with the `API` prefix represents a payload you may get from the REST API _or_ the Gateway.

- Everything exported with the `Gateway` prefix represents data that ONLY comes from or is directly related to the Gateway.

- Everything exported with the `REST` prefix represents data that ONLY comes from or is directly related to the REST API.

  - For endpoint options, they will follow the following structure: `REST<HTTP Method><Type><Query|(JSON|FormData)Body|Result>` where the type represents what it will return.

    - For example, `RESTPostAPIChannelMessageJSONBody` or `RESTGetAPIGatewayBotInfoResult`.

    - Some exported types (specifically OAuth2 related ones) may not respect this entire structure due to the nature of the fields. They will start with either `RESTOAuth2` or with something similar to `REST<HTTP Method>OAuth2`

  - If a type ends with `Result`, then it represents the expected result by calling its accompanying route.

    - Types that are exported as `never` usually mean the result will be a `204 No Content`, so you can safely ignore it. This does **not** account for errors.

- Anything else that is miscellaneous will be exported based on what it represents (for example the `REST` route object).

- There may be types exported that are identical for all versions. These will be exported as is and can be found in the `globals` file. They will still be prefixed accordingly as described above.

**Warning**: This package documents just KNOWN (and documented) properties. Anything that isn't documented will NOT be added to this package (unless said properties are in an open Pull Request to Discord's [API Documentation repository](https://github.com/discord/discord-api-docs) or known through other means _and have received the green light to be used_). For clarification's sake, this means that properties that are only known through the process of data mining and have not yet been confirmed in a way as described will **NOT** be included.
