# Gatsby Js

## Instalación

```bash
npm install -g gatsby-cli
gatsby new hello-work
cd hello-work
gatsby run develop
gatsby run build
gatsby run serve
```

## Theme Gatsby

```bash
npm install gatsby-theme-blog
```

## Opciones de tema

##### gatsby-config.js

```js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        /*
        - basePath defaults to `/`
        */
        basePath: `/blog`,
      },
    },
  ],
}
```

```bash
npm install theme-ui-sketchy-preset
```
