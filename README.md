This is a single-page application template which uses esbuild.

## Your code

- `src/index.ts`: where you write your code
- `src/index.dev.html`: the development HTML template
- `src/index.prod.html`: the production HTML template
- `src/index.postcss`: your CSS

**Run `bun tw` and `bun esb` in separate terminals to start developing.**

## Other files

- `src/index.dist.d.css.ts`: a declaration file so TypeScript knows
  `index.dist.css` exists and can be imported without causing an error

## Generated files

- `src/index.postcss.css`: the compiled postcss and tailwind code (this isn't in
  `dist` so that esbuild doesn't override it accidentally)
- `dist/...`: esbuild's output directory

Make sure to import `src/index.postcss.css` into your main JavaScript file; this
is how esbuild knows where to get your CSS from.

## Running the project

To develop locally, run `bun tw` and `bun esb` in two separate terminals. If you
think you won't make any CSS modifications, you can just run `bun dev` instead,
which will rebuild the CSS once, then switch to `bun esb`.

To deploy the project, execute `bun run build` to generate the `dist` directory,
then serve the entire `dist/` directory.

## Code-splitting

esbuild code-splitting is enabled, so asynchronous `import(...)` statements will
work. This means, however, that import order is not guaranteed to be stable. See
https://esbuild.github.io/api/#splitting for more information.

Imports will work correctly if you avoid cyclic imports (multiple files
importing each other in a chain). To check the project for cyclic imports, run
`bun lint:cycles`.

## Icons

Use https://realfavicongenerator.net/ to generate these files:

- apple-touch-icon.png
- favicon-96x96.png
- favicon.ico
- favicon.svg
- site.webmanifest
- web-app-manifest-192x192.png
- web-app-manifest-512x512.png

Then, put all those files into a top-level `icon` directory, and change the
"build:icon" script in the package.json to:

```sh
cp -R icon dist/icon && cp icon/favicon.ico dist/favicon.ico
```
