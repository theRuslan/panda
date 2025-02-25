# @pandacss/token-dictionary

## 0.29.0

### Patch Changes

- 7c7340ec: Add support for token references with curly braces like `{path.to.token}` in media queries, just like the
  `token(path.to.token)` alternative already could.

  ```ts
  css({
    // ✅ this is fine now, will resolve to something like
    // `@container (min-width: 56em)`
    '@container (min-width: {sizes.4xl})': {
      color: 'green',
    },
  })
  ```

  Fix an issue where the curly token references would not be escaped if the token path was not found.

- Updated dependencies [5fcdeb75]
- Updated dependencies [250b4d11]
- Updated dependencies [a2fb5cc6]
  - @pandacss/types@0.29.0
  - @pandacss/logger@0.29.0
  - @pandacss/shared@0.29.0

## 0.28.0

### Patch Changes

- d4fa5de9: Fix a typing issue where the `borderWidths` wasn't specified in the generated `TokenCategory` type
- Updated dependencies [f58f6df2]
- Updated dependencies [770c7aa4]
  - @pandacss/types@0.28.0
  - @pandacss/shared@0.28.0

## 0.27.3

### Patch Changes

- Updated dependencies [1ed4df77]
  - @pandacss/types@0.27.3
  - @pandacss/shared@0.27.3

## 0.27.2

### Patch Changes

- @pandacss/shared@0.27.2
- @pandacss/types@0.27.2

## 0.27.1

### Patch Changes

- Updated dependencies [ee9341db]
  - @pandacss/types@0.27.1
  - @pandacss/shared@0.27.1

## 0.27.0

### Minor Changes

- 84304901: Improve performance, mostly for the CSS generation by removing a lot of `postcss` usage (and plugins).

  ## Public changes:

  - Introduce a new `config.lightningcss` option to use `lightningcss` (currently disabled by default) instead of
    `postcss`.
  - Add a new `config.browserslist` option to configure the browserslist used by `lightningcss`.
  - Add a `--lightningcss` flag to the `panda` and `panda cssgen` command to use `lightningcss` instead of `postcss` for
    this run.

  ## Internal changes:

  - `markImportant` fn from JS instead of walking through postcss AST nodes
  - use a fork of `stitches` `stringify` function instead of `postcss-css-in-js` to write the CSS string from a JS
    object
  - only compute once `TokenDictionary` properties
  - refactor `serializeStyle` to use the same code path as the rest of the pipeline with `StyleEncoder` / `StyleDecoder`
    and rename it to `transformStyles` to better convey what it does

- bee3ec85: Add support for aspect ratio tokens in the panda config or preset. Aspect ratio tokens are used to define
  the aspect ratio of an element.

  ```js
  export default defineConfig({
    // ...
    theme: {
      extend: {
        // add aspect ratio tokens
        tokens: {
          aspectRatios: {
            '1:1': '1',
            '16:9': '16/9',
          },
        },
      },
    },
  })
  ```

  Here's what the default aspect ratio tokens in the base preset looks like:

  ```json
  {
    "square": { "value": "1 / 1" },
    "landscape": { "value": "4 / 3" },
    "portrait": { "value": "3 / 4" },
    "wide": { "value": "16 / 9" },
    "ultrawide": { "value": "18 / 5" },
    "golden": { "value": "1.618 / 1" }
  }
  ```

  **Breaking Change**

  The built-in token values has been removed from the `aspectRatio` utility to the `@pandacss/preset-base` as a token.

  For most users, this change should be a drop-in replacement. However, if you used a custom preset in the config, you
  might need to update it to include the new aspect ratio tokens.

### Patch Changes

- Updated dependencies [84304901]
- Updated dependencies [74ac0d9d]
  - @pandacss/shared@0.27.0
  - @pandacss/types@0.27.0

## 0.26.2

### Patch Changes

- @pandacss/shared@0.26.2
- @pandacss/types@0.26.2

## 0.26.1

### Patch Changes

- @pandacss/shared@0.26.1
- @pandacss/types@0.26.1

## 0.26.0

### Patch Changes

- Updated dependencies [657ca5da]
- Updated dependencies [b5cf6ee6]
- Updated dependencies [58df7d74]
  - @pandacss/shared@0.26.0
  - @pandacss/types@0.26.0

## 0.25.0

### Minor Changes

- de282f60: Support token reference syntax when authoring styles object, text styles and layer styles.

  ```jsx
  import { css } from '../styled-system/css'

  const styles = css({
    border: '2px solid {colors.primary}',
  })
  ```

  This will resolve the token reference and convert it to css variables.

  ```css
  .border_2px_solid_\{colors\.primary\} {
    border: 2px solid var(--colors-primary);
  }
  ```

  The alternative to this was to use the `token(...)` css function which will be resolved.

  ### `token(...)` vs `{...}`

  Both approaches return the css variable

  ```jsx
  const styles = css({
    // token reference syntax
    border: '2px solid {colors.primary}',
    // token function syntax
    border: '2px solid token(colors.primary)',
  })
  ```

  However, The `token(...)` syntax allows you to set a fallback value.

  ```jsx
  const styles = css({
    border: '2px solid token(colors.primary, red)',
  })
  ```

### Patch Changes

- Updated dependencies [59fd291c]
  - @pandacss/types@0.25.0
  - @pandacss/shared@0.25.0

## 0.24.2

### Patch Changes

- Updated dependencies [71e82a4e]
  - @pandacss/shared@0.24.2
  - @pandacss/types@0.24.2

## 0.24.1

### Patch Changes

- @pandacss/shared@0.24.1
- @pandacss/types@0.24.1

## 0.24.0

### Patch Changes

- Updated dependencies [f6881022]
  - @pandacss/types@0.24.0
  - @pandacss/shared@0.24.0

## 0.23.0

### Patch Changes

- @pandacss/shared@0.23.0
- @pandacss/types@0.23.0

## 0.22.1

### Patch Changes

- Updated dependencies [8f4ce97c]
- Updated dependencies [647f05c9]
  - @pandacss/types@0.22.1
  - @pandacss/shared@0.22.1

## 0.22.0

### Patch Changes

- Updated dependencies [526c6e34]
- Updated dependencies [8db47ec6]
  - @pandacss/types@0.22.0
  - @pandacss/shared@0.22.0

## 0.21.0

### Patch Changes

- Updated dependencies [26e6051a]
- Updated dependencies [5b061615]
- Updated dependencies [105f74ce]
  - @pandacss/shared@0.21.0
  - @pandacss/types@0.21.0

## 0.20.1

### Patch Changes

- @pandacss/shared@0.20.1
- @pandacss/types@0.20.1

## 0.20.0

### Patch Changes

- Updated dependencies [24ee49a5]
- Updated dependencies [904aec7b]
  - @pandacss/types@0.20.0
  - @pandacss/shared@0.20.0

## 0.19.0

### Patch Changes

- Updated dependencies [61831040]
- Updated dependencies [89f86923]
  - @pandacss/types@0.19.0
  - @pandacss/shared@0.19.0

## 0.18.3

### Patch Changes

- @pandacss/shared@0.18.3
- @pandacss/types@0.18.3

## 0.18.2

### Patch Changes

- @pandacss/shared@0.18.2
- @pandacss/types@0.18.2

## 0.18.1

### Patch Changes

- 566fd28a: Fix issue where virtual color does not apply DEFAULT color in palette
- 43bfa510: Fix issue where composite tokens (shadows, border, etc) generated incorrect css when using the object syntax
  in semantic tokens.
  - @pandacss/shared@0.18.1
  - @pandacss/types@0.18.1

## 0.18.0

### Patch Changes

- Updated dependencies [ba9e32fa]
  - @pandacss/shared@0.18.0
  - @pandacss/types@0.18.0

## 0.17.5

### Patch Changes

- @pandacss/shared@0.17.5
- @pandacss/types@0.17.5

## 0.17.4

### Patch Changes

- Updated dependencies [fa77080a]
  - @pandacss/types@0.17.4
  - @pandacss/shared@0.17.4

## 0.17.3

### Patch Changes

- Updated dependencies [529a262e]
  - @pandacss/types@0.17.3
  - @pandacss/shared@0.17.3

## 0.17.2

### Patch Changes

- @pandacss/shared@0.17.2
- @pandacss/types@0.17.2

## 0.17.1

### Patch Changes

- Updated dependencies [5ce359f6]
  - @pandacss/shared@0.17.1
  - @pandacss/types@0.17.1

## 0.17.0

### Patch Changes

- Updated dependencies [12281ff8]
- Updated dependencies [fc4688e6]
  - @pandacss/shared@0.17.0
  - @pandacss/types@0.17.0

## 0.16.0

### Patch Changes

- @pandacss/shared@0.16.0
- @pandacss/types@0.16.0

## 0.15.5

### Patch Changes

- @pandacss/shared@0.15.5
- @pandacss/types@0.15.5

## 0.15.4

### Patch Changes

- @pandacss/types@0.15.4
- @pandacss/shared@0.15.4

## 0.15.3

### Patch Changes

- Updated dependencies [95b06bb1]
- Updated dependencies [1ac2011b]
- Updated dependencies [58743bc4]
  - @pandacss/shared@0.15.3
  - @pandacss/types@0.15.3

## 0.15.2

### Patch Changes

- Updated dependencies [26a788c0]
  - @pandacss/types@0.15.2
  - @pandacss/shared@0.15.2

## 0.15.1

### Patch Changes

- 4e003bfb: - reuse css variable in semantic token alias
- Updated dependencies [26f6982c]
  - @pandacss/shared@0.15.1
  - @pandacss/types@0.15.1

## 0.15.0

### Patch Changes

- Updated dependencies [4bc515ea]
- Updated dependencies [9f429d35]
- Updated dependencies [39298609]
- Updated dependencies [f27146d6]
  - @pandacss/types@0.15.0
  - @pandacss/shared@0.15.0

## 0.14.0

### Minor Changes

- b1c31fdd: - Introduces deep nested `colorPalettes` for enhanced color management

  - Previous color palette structure was flat and less flexible, now `colorPalettes` can be organized hierarchically for
    improved organization

  **Example**: Define colors within categories, variants and states

  ```js
  const theme = {
    extend: {
      semanticTokens: {
        colors: {
          button: {
            dark: {
              value: 'navy',
            },
            light: {
              DEFAULT: {
                value: 'skyblue',
              },
              accent: {
                DEFAULT: {
                  value: 'cyan',
                },
                secondary: {
                  value: 'blue',
                },
              },
            },
          },
        },
      },
    },
  }
  ```

  You can now use the root `button` color palette and its values directly:

  ```tsx
  import { css } from '../styled-system/css'

  export const App = () => {
    return (
      <button
        className={css({
          colorPalette: 'button',
          color: 'colorPalette.light',
          backgroundColor: 'colorPalette.dark',
          _hover: {
            color: 'colorPalette.light.accent',
            background: 'colorPalette.light.accent.secondary',
          },
        })}
      >
        Root color palette
      </button>
    )
  }
  ```

  Or you can use any deeply nested property (e.g. `button.light.accent`) as a root color palette:

  ```tsx
  import { css } from '../styled-system/css'

  export const App = () => {
    return (
      <button
        className={css({
          colorPalette: 'button.light.accent',
          color: 'colorPalette.secondary',
        })}
      >
        Nested color palette leaf
      </button>
    )
  }
  ```

### Patch Changes

- 9e799554: Fix issue where negative spacing tokens doesn't respect hash option
- Updated dependencies [8106b411]
- Updated dependencies [e6459a59]
- Updated dependencies [6f7ee198]
  - @pandacss/types@0.14.0
  - @pandacss/shared@0.14.0

## 0.13.1

### Patch Changes

- @pandacss/shared@0.13.1
- @pandacss/types@0.13.1

## 0.13.0

### Patch Changes

- @pandacss/shared@0.13.0
- @pandacss/types@0.13.0

## 0.12.2

### Patch Changes

- @pandacss/shared@0.12.2
- @pandacss/types@0.12.2

## 0.12.1

### Patch Changes

- @pandacss/shared@0.12.1
- @pandacss/types@0.12.1

## 0.12.0

### Patch Changes

- @pandacss/shared@0.12.0
- @pandacss/types@0.12.0

## 0.11.1

### Patch Changes

- Updated dependencies [c07e1beb]
- Updated dependencies [23b516f4]
  - @pandacss/shared@0.11.1
  - @pandacss/types@0.11.1

## 0.11.0

### Patch Changes

- Updated dependencies [5b95caf5]
  - @pandacss/types@0.11.0
  - @pandacss/shared@0.11.0

## 0.10.0

### Patch Changes

- 9d4aa918: Fix issue where svg asset tokens are seen as invalid in the browser
- Updated dependencies [24e783b3]
- Updated dependencies [386e5098]
- Updated dependencies [a669f4d5]
  - @pandacss/shared@0.10.0
  - @pandacss/types@0.10.0

## 0.9.0

### Patch Changes

- Updated dependencies [c08de87f]
  - @pandacss/types@0.9.0
  - @pandacss/shared@0.9.0

## 0.8.0

### Patch Changes

- ac078416: Fix issue with extracting nested tokens as color-palette. Fix issue with extracting shadow array as a
  separate unnamed block for the custom dark condition.
- Updated dependencies [be0ad578]
  - @pandacss/types@0.8.0
  - @pandacss/shared@0.8.0

## 0.7.0

### Patch Changes

- Updated dependencies [f59154fb]
- Updated dependencies [a9c189b7]
  - @pandacss/shared@0.7.0
  - @pandacss/types@0.7.0

## 0.6.0

### Patch Changes

- @pandacss/types@0.6.0
- @pandacss/shared@0.6.0

## 0.5.1

### Patch Changes

- Updated dependencies [8c670d60]
- Updated dependencies [c0335cf4]
- Updated dependencies [762fd0c9]
- Updated dependencies [1ed239cd]
- Updated dependencies [78ed6ed4]
  - @pandacss/types@0.5.1
  - @pandacss/shared@0.5.1

## 0.5.0

### Patch Changes

- Updated dependencies [60df9bd1]
- Updated dependencies [ead9eaa3]
  - @pandacss/shared@0.5.0
  - @pandacss/types@0.5.0

## 0.4.0

### Patch Changes

- Updated dependencies [c7b42325]
- Updated dependencies [5b344b9c]
  - @pandacss/types@0.4.0
  - @pandacss/shared@0.4.0

## 0.3.2

### Patch Changes

- @pandacss/shared@0.3.2
- @pandacss/types@0.3.2

## 0.3.1

### Patch Changes

- efd79d83: Baseline release for the launch
- Updated dependencies [efd79d83]
  - @pandacss/shared@0.3.1
  - @pandacss/types@0.3.1

## 0.3.0

### Patch Changes

- Updated dependencies [6d81ee9e]
  - @pandacss/types@0.3.0
  - @pandacss/shared@0.3.0

## 0.0.2

### Patch Changes

- fb40fff2: Initial release of all packages

  - Internal AST parser for TS and TSX
  - Support for defining presets in config
  - Support for design tokens (core and semantic)
  - Add `outExtension` key to config to allow file extension options for generated javascript. `.js` or `.mjs`
  - Add `jsxElement` option to patterns, to allow specifying the jsx element rendered by the patterns.

- Updated dependencies [c308e8be]
- Updated dependencies [fb40fff2]
  - @pandacss/types@0.0.2
  - @pandacss/shared@0.0.2
