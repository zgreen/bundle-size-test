This is a reproduction case for an issue where using `next-swc` instead of `babel` causes bundle sizes to get larger, because `next-swc` does not use `browserslist`. This project was created with `create-next-app` and includes no additional code, and no additional dependencies, except for babel.

Conversation is here: https://github.com/vercel/next.js/discussions/30237#discussioncomment-2288587

## Test results

### With `next-swc`

```
Page                                       Size     First Load JS
┌ ○ /                                      6.26 kB        80.7 kB
├   └ css/149b18973e5508c7.css             655 B
├   /_app                                  0 B            74.5 kB
├ ○ /404                                   192 B          74.7 kB
└ λ /api/hello                             0 B            74.5 kB
+ First Load JS shared by all              74.5 kB
  ├ chunks/framework-00b57966872fc495.js   44.9 kB
  ├ chunks/main-f4ae3437c92c1efc.js        28.3 kB
  ├ chunks/pages/_app-f55443f2448c8e66.js  493 B
  ├ chunks/webpack-69bfa6990bb9e155.js     769 B
  └ css/27d177a30947857b.css               194 B
```

### With `babel`

```
Page                                       Size     First Load JS
┌ ○ /                                      6.67 kB        72.9 kB
├   └ css/149b18973e5508c7.css             655 B
├   /_app                                  0 B            66.2 kB
├ ○ /404                                   2.51 kB        68.7 kB
└ λ /api/hello                             0 B            66.2 kB
+ First Load JS shared by all              66.2 kB
├ chunks/framework-00b57966872fc495.js   44.9 kB
├ chunks/main-ea7e989417432124.js        19.3 kB
├ chunks/pages/_app-61908809f3d5c637.js  553 B
├ chunks/webpack-d27a0b5d1fa67d61.js     1.48 kB
└ css/27d177a30947857b.css               194 B
```

## Test it yourself

Simply add or remove `babel.config.js`, which will toggle the `babel`-based build on and off. You can also try enabling/disabling `swcMinify` in `next.config.js` (note that this has no effect on bundle sizes).
