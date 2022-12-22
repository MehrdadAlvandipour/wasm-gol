# wasm-gol

Game of Life with Rust and Wasm following the tutorial [here](https://rustwasm.github.io/docs/book/game-of-life/implementing.html).

Requires node et al. for server.


## Run

```
cd www
npm install 
npm run start
```

Then check http://localhost:8080/ 

If you are already using 8080, modify "start" under "scripts" in www/package.json use another port e.g. 8090:

```
//..
    "start": "webpack-dev-server --host 0.0.0.0 --port 8090",
//..
```


## Troubleshoot


if npm run start failed with 
```sh
//...
opensslErrorStack: [ 'error:03000086:digital envelope routines::initialization error' ],
  library: 'digital envelope routines',
  reason: 'unsupported',
  code: 'ERR_OSSL_EVP_UNSUPPORTED'
```
run `export NODE_OPTIONS=--openssl-legacy-provider` in your terminal and then run `npm run start` again.


## Summary

[wasm-pack](https://rustwasm.github.io/wasm-pack/installer/) builds Wasm from Rust (`wasm-pack build`). 
Result is stored in /pkg folder. It's ported to npm as dependency with 
`"dependencies": {"wasm-game-of-life": "file:../pkg"},` in www/package.json. Running `npm install` under www/ 
folder installs it as a node module, put under the freshly generated folder www/node_modules/. When you update 
rust code and rebuild (`wasm-pack build` from project root folder), you might need to 
`rm -rf www/node_modules/wasm-game-of-life` and `npm install` again so the npm module gets updated.




