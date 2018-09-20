# typescript-vue-starter

## Add typescript support

### Change the entry
```
// vue.config.js
module.exports = {
  ...
  pages: {
    index: {
      // page 的入口
      entry: 'src/index.ts',
      // 模板来源
      template: 'public/index.html',
      // 在 dist/index.html 的输出
      filename: 'index.html',
      // 当使用 title 选项时，
      // template 中的 title 标签需要是 <title><%= htmlWebpackPlugin.options.title %></title>
      title: 'Index Page',
      // 在这个页面中包含的块，默认情况下会包含
      // 提取出来的通用 chunk 和 vendor chunk。
      chunks: ['chunk-vendors', 'chunk-common', 'index']
    },
  },
  ...
}
```

### Add ts extensions
```
// vue.config.js
module.exports = {
  ...
  configureWebpack: {
    resolve: {
      extensions: [
        '.ts',
        '.tsx',
        '.js',
        '.jsx',
        '.vue',
        '.json'
      ],
    },
  },
  ...
};
```

### Add ts-loader
You can add `ts-loader` on chainWepack property.
```
// vue.config.js
module.exports = {
  ...
  chainWebpack: config => {
    config.module
      .rule('ts')
      .test(/\.ts$/)
      .use('ts-loader')
      .loader('ts-loader')
      .options({
        appendTsSuffixTo: [/\.vue$/],
      })
      .end()
  }
  ...
}
```
You can also add it on configureWebpack property.
```
module.exports = {
  ...
  configureWebpack: {
    module: {
      rules: [{
        test: /\.ts$/,
        loader: 'ts-loader',
        options: {
          appendTsSuffixTo: [/\.vue$/],
        },
      }],
    },
  },
  ...
}
```
### Final config
```
// vue.config.js
module.exports = {
  pages: {
    index: {
      // page 的入口
      entry: 'src/index.ts',
      // 模板来源
      template: 'public/index.html',
      // 在 dist/index.html 的输出
      filename: 'index.html',
      // 当使用 title 选项时，
      // template 中的 title 标签需要是 <title><%= htmlWebpackPlugin.options.title %></title>
      title: 'Index Page',
      // 在这个页面中包含的块，默认情况下会包含
      // 提取出来的通用 chunk 和 vendor chunk。
      chunks: ['chunk-vendors', 'chunk-common', 'index']
    },
  },
  configureWebpack: {
    resolve: {
      extensions: [
        '.ts',
        '.tsx',
        '.js',
        '.jsx',
        '.vue',
        '.json'
      ],
    },
  //   module: {
  //     rules: [{
  //       test: /\.ts$/,
  //       loader: 'ts-loader',
  //       options: {
  //         appendTsSuffixTo: [/\.vue$/],
  //       },
  //     }],
  //   },
  },
  // 也可以用 configureWebpack里的module实现
  chainWebpack: config => {
    config.module
      .rule('ts')
      .test(/\.ts$/)
      .use('ts-loader')
      .loader('ts-loader')
      .options({
        appendTsSuffixTo: [/\.vue$/],
      })
      .end()
  }
};
```
