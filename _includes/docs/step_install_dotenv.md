## Install dotenv

Install [`dotenv`](https://github.com/motdotla/dotenv).

##### CLI
```shell
npm install dotenv --save # Requires dotenv >= 16.1.0
```

Create a `.env` file in the root of your project.

##### .env
```shell
# .env
HELLO="World"
```

As early as possible in your application, import and configure dotenv.

##### index.js
```js
// index.js
require('dotenv').config()
console.log(process.env) // remove this after you've confirmed it is working

const PORT = process.env.PORT || 3000
const http = require('http')
...
```

Try running it locally.

##### CLI
```shell
node index.js
{
  ...
  HELLO: 'World'
}
Server running on port:3000/
```

Perfect. `process.env` now has the keys and values you defined in your `.env` file.

That covers local development. Let's solve for production next.