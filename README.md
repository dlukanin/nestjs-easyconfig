<p align="center">
  <a href="http://github.com/nest-easyconfigs/" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a>
</p>
<p align="center">.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjs-eastconfig"><img src="https://img.shields.io/npm/l/nestjs-easyconfig" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjs-eastconfig"><img src="https://img.shields.io/npm/dw/nestjs-easyconfig" alt="NPM Downloads" /></a>
<a href="https://circleci.com/rubiin/nestjs-easyconfig"><img src="https://circleci.com/gh/rubiin/nestjs-easyconfig/tree/master.svg?style=shield" alt="circleci" /></a>
<a href=""><img src="https://badgen.net/dependabot/dependabot/dependabot-core/?icon=dependabot" /></a>
<a href="https://beerpay.io/rubiin/nestjs-easyconfig"><img src="https://beerpay.io/rubiin/nestjs-easyconfig/badge.svg?style=plastic" /></a>

</p>
 
## Description

[Nestjs-easyconfig](https://github.com/rubiin/nestjs-easyconfig) loads configs from your `.env` (Wraps dotenv module) ⚙️ 🔥

## Installation

```bash
$ npm install nestjs-easyconfig
$ yarn add nestjs-easyconfig
```

## Usage

### With config file supplied (basic):

```javascript
import { Module } from '@nestjs/common';
import { EasyconfigModule } from 'nestjs-easyconfig';

@Module({
  imports: [EasyconfigModule.register({ path: './config/.env' })],
})
export class AppModule {}
```

### With config file supplied and safe set to true:

```javascript
import { Module } from '@nestjs/common';
import { EasyconfigModule } from 'nestjs-easyconfig';

@Module({
  imports: [EasyconfigModule.register({ path: './config/.env', safe: true })],
})
export class AppModule {}
```

By default safe is set to false. When safe is set to `true`, the module compares the supplied env
file with the sample env file to find missing keys. If any keys which are in .env.sample but not in the evironment used, it is immediately reported in console.

`Note`: To use this, a sample env file `.env.sample` should be placed in the root dir


Other config include dotenv's configs like encoding (Default: utf8) and debug(Default: false)

### Without config file supplied:

```javascript
import { Module } from '@nestjs/common';
import { EasyconfigModule } from 'nestjs-easyconfig';

@Module({
  imports: [EasyconfigModule.register({})],
})
export class AppModule {}
```

In this case, you have to pass in the <b>NODE_ENV</b> value and the `.env` file to read will be determined accordingly.
Loads environment variables from `.env.[development|test|production][.local]` files
For example, <b>NODE_ENV=dev</b> will make the app read `.env.dev`

> Note: The .env file also has to be in root folder

### Getting environment variables

Regardless of how the `EasyconfigModule` is imported into the app, you can get the variable values using the `EasyconfigService`.

```javascript
import { Controller, Get } from '@nestjs/common';
import { EasyconfigService } from 'nestjs-easyconfig';

@Controller('api')
export class AppController {
  constructor (private config: EasyconfigService) {}
  @Get()
  findAll() {
    return {
      value: this.config.get('key')
    };
  }
}
```

> Note: the `get` method will automatically cast environment variables

### Type processing
Module uses dotenv-parse-variables lib (https://www.npmjs.com/package/dotenv-parse-variables) to process env file.
Example of type processing:

```
    foo=test
    bar=1
    baz=true
    qux=test,1,true,
    bat=false*,
    qwe=`1,2,3`,
    asd=test,1,true*
```
will be processed to
```javascript
    {
        foo: 'test',
        bar: 1,
        baz: true,
        qux: ['test', 1, true],
        bat: 'false',
        qwe: '1,2,3',
        asd: ['test', 1, 'true']
    }
```


## Contributing

In general, we follow the "fork-and-pull" Git workflow.

1. Fork the repo on GitHub
2. Clone the project to your own machine
3. Work on your fork
    1. Make your changes and additions
        - Most of your changes should be focused on `src/` and `test/` folders and/or `README.md`. 
        - Files in `dist/` folder are autogenerated when running tests (`npm run build`) and need not to be changed **manually**. 
    2. Change or add tests if needed
    3. Run tests and make sure they pass
    4. Add changes to README.md if needed
4. Commit changes to your own branch
5. **Make sure** you merge the latest from "upstream" and resolve conflicts if there is any
6. Repeat step 3(3) above
7. Push your work back up to your fork
8. Submit a Pull request so that we can review your changes

## Stay in touch

- Author - [Rubin Bhandari](https://github.com/rubiin)
- Dev․to - [@rubinsays](https://dev.to/rubiin)
- Discord - [@rubin#1186](https://discordapp.com/)

## License

The package is [MIT licensed](LICENSE).

## Support on Beerpay

Hey dude! Help me out for a couple of :beers:!

[![Beerpay](https://beerpay.io/rubiin/nestjs-easyconfig/badge.svg?style=beer-square)](https://beerpay.io/rubiin/nestjs-easyconfig) [![Beerpay](https://beerpay.io/rubiin/nestjs-easyconfig/make-wish.svg?style=flat-square)](https://beerpay.io/rubiin/nestjs-easyconfig?focus=wish)

## Contributors ✨

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
<table>
  <tr>
    <td align="center"><a href="https://github.com/dlukanin"><img src="https://avatars1.githubusercontent.com/u/875405?v=4" width="100px;" alt="Dmitry Lukanin"/><br /><sub><b>Dmitry Lukanin</b></sub></a><br /><a href="#infra-dlukanin" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/rubiin/nestjs-easyconfig/commits?author=dlukanin" title="Tests">⚠️</a> <a href="https://github.com/rubiin/nestjs-easyconfig/commits?author=dlukanin" title="Code">💻</a></td>
    <td align="center"><a href="https://github.com/bradtaniguchi"><img src="https://avatars3.githubusercontent.com/u/10079147?v=4" width="100px;" alt="Brad"/><br /><sub><b>Brad</b></sub></a><br /><a href="#infra-bradtaniguchi" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a> <a href="https://github.com/rubiin/nestjs-easyconfig/commits?author=bradtaniguchi" title="Code">💻</a></td>
    <td align="center"><a href="https://coollabs.io"><img src="https://avatars1.githubusercontent.com/u/5845193?v=4" width="100px;" alt="Andras Bacsai"/><br /><sub><b>Andras Bacsai</b></sub></a><br /><a href="#infra-andrasbacsai" title="Infrastructure (Hosting, Build-Tools, etc)">🚇</a></td>
  </tr>
</table>

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
