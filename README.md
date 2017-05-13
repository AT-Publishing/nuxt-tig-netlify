# starter

> Nuxt.js project

package.json to do

```
{
  "dependencies": {
    "nuxt": "^0.9.6",
  },
  "scripts": {
    "dev": "NODE_ENV=development nuxt",
    "build": "nuxt build",
    "start": "npm run build; NODE_ENV=production HOST=0.0.0.0 nuxt start",
    "dev": "npm run build; nuxt start"
  },
  "engines": {
    "node": "7.4.0"
  }
}
```

## Build Setup

``` bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).
