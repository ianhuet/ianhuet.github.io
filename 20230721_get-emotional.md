---
title: "Get Emotional"
date: "July 2023"
excerpt: "exploring configuration, integration and DevEx options with React, MUI, Emotion CSS & Stylelint"
---

# Get Emotional
Exploring configuration, integration and DevEx options with React, Material UI, Emotion CSS & Stylelint

#### TL;DR
> I have previously used the Material UI.v4 JSS implementation to deliver highly consistent, easily implemented, and easily maintained UI. Emotion CSS now sits at the heart of [MUI.v5](https://mui.com/). This is an experiment to see if Emotion CSS can also deliver maintainable styles and an effective development experience? The result is that it is effective, though automated style linting is problematic.

---

I first started working with CSS at version 2.3 back when HTML tables were the only way to implement layouts. Since then I have worked at scale with nearly all CSS implementations. Coming from a classic CSS background I initially resisted the Javascript implementations. Working with Material UI won me over. Now several successfully delivered projects later I appreciate the benefits it offers. Especially for delivering consistent UI in complex web application development. It is not a perfect tool though, being a runtime system adds the need to carefully monitored for performance impacts.

## An experiment with React, Material UI, Emotion CSS & Stylelint

**Note:**

- As Material UI (MUI v.5) uses Emotion CSS under the hood it will be used as the theming engine.
- All the code is from [this GitHub repository](https://github.com/ianhuet/react-vite-mui-emotion-stylelint).

**Steps Followed**

1. [Create a new Vite based React project](#create-project)
2. [Add Stylelint to lint CSS styles](#add-stylelint)
3. [Add Emotion CSS, and enable the `css` prop](#add-emotion-css)
4. [Migrate the default `App.css` to Emotion CSS](#migrate-css-to-emotion)
5. [Evolve the Stylelint configuration to work with Emotion CSS](#stylelint-emotion-config)
6. [Extract Emotion styles out of the component closure](#extract-emotion)
7. [Integrate MUI theming into the Emotion styling](#emotion-theming)
8. [Create a utility to simplify style implementation](#style-utility)

### 1. Create a new Vite based React project {#create-project}
Run this command, give the project a name, then select 'React' & 'Typescript'.
```
npm create vite@latest
```

### 2. Add Stylelint to lint CSS styles {#add-stylelint}
Install these packages, then add the following script and configuration to integrate Stylelint into the development toolchain.
```
npm i -D stylelint stylelint-config-standard stylelint-order
```

`.stylelintrc.yml`
```
---
extends:
- stylelint-config-standard
plugins:
- stylelint-order
rules:
  declaration-property-value-no-unknown: true
  order/properties-alphabetical-order: true
```
This configuration adds several useful elements to the Stylelint setup. `stylelint-config-standard` is the best practice benchmark rule set offered by Stylelint. `declaration-property-value-no-unknown` is a new rule available with Stylelint v.15 which checks that each property value is valid. `order/properties-alphabetical-order` enables the automated ordering or properties into the most simple and inuitive sequence. Of course this can be greatly customised yet it represents a realistic starting point.

`package.json`
```
"lint:style": "stylelint '**/*.css' --fix",
```
Add this to the `scripts` section to enable style linting, and automated fixing where possible.

### 3. Add Emotion CSS, and enable the `css` prop {#add-emotion-css}
With the base application established and Stylelint integrate next up is the migration of the classic CSS styles to Emotion CSS.
```
npm i @emotion/react
```

In order to play nice with the Typescript compiler this must be added to `tsconfig.ts`, as well as being added to the 'vite.config.ts' React plugin config: `"jsxImportSource": "@emotion/react"`. The next step is to choose between the [JSX Pgrama](https://emotion.sh/docs/css-prop#jsx-pragma) integration or the Babel plugin enabled [css prop](https://emotion.sh/docs/css-prop). I opted for the `css prop` option as I am not keen on the need to add the below code at the top of every component.
```
/** @jsx jsx */
import { jsx } from '@emotion/react'
```

Enabling the 'css prop' first requires these packages be added to the project: `@emotion/babel-plugin @emotion/babel-preset-css-prop`. Then add this additional configuration to the `vite.config.ts` React plugin config.
```
babel: {
  plugins: ["@emotion/babel-plugin"],
},
```

### 4. Migrate the default `App.css` to Emotion CSS {#migrate-css-to-emotion}
With these in place Emotion CSS can now be integrated into the JSX either inline or as a serialised styles object. The serialised styles object option requires the `css` function to convert object or template literal style notation to the data structure compatible with the JSX css prop.
```
import { css } from '@emotion/react'

// serialised styles object
const readTheDocs = css`
  color: 'readTheDocs.invalid';
  font-weight: ${theme.typography.fontWeightBold};
`

<h2>Individual Styles</h2>
<div css={{ padding: '2em' }}>
  ...
</div>
<p css={readTheDocs}>
  Click on the Vite and React logos to learn more
</p>
```

### 5. Evolve the Stylelint configuration to work with Emotion CSS {#stylelint-emotion-config}
The Stylelint configuration needs to be expanded to include cover for the CSS-in-JS implementation introduced by Emotion. The first step is to update the `lint:style` script within the package.json to include the components: `lint:style": "stylelint '**/*.{css,tsx}' --fix`. Next the stylelint configuration also needs to be updated.

`.stylelintrc.yml`
```
- customSyntax: "postcss-styled-syntax"
  files:
  - "**/*.tsx"
```
This establishes an override for the Typescript component implementations, catered for by the [postcss-styled-syntax](https://www.npmjs.com/package/postcss-styled-syntax) custom syntax. Running the linting now surfaces any issues within our Emotion CSS.

### 6. Extract Emotion styles out of the component closure {#extract-emotion}
While functional there are a few issues with this first approach. For starters, I am not a fan of inline styles. They both clutter up the JSX markup and add potentially problematic specificity to the styling. Beyond this there is [a more pronounced issue, performance](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b). Having the styles declared inside the component scope results in them being recreated on every rerender.

All of these concerns can be mitigated by extracting the styles outside the component as shown below. This tidies up the JSX without impacting any of the styling functionality. It removes the performance impact incurred by the styles being reproduced on each render cycle. And it is still covered by stylelint.
```
const templateLiteralStyles = {
  card: css`
    padding: 2em;
  `,
  readTheDocs: css`
    color: 'templateStyles.invalid';
    font-weight: 700;
  `,
}

export function App() {
  const styles = templateLiteralStyles;
  ...
  <h2>Utils.cssProps Styles</h2>
  <div css={styles.card}>
    ...
  </div>
  <p css={styles.readTheDocs}>
    Click on the Vite and React logos to learn more
  </p>
```

### 7. Integrate MUI theming into the Emotion styling {#emotion-theming}
Establishing, and consistently using, a centralised theme is a core element of building high quality UI. So enabling this with Emotion CSS is a essential requirement. Thankfully adjusting the extracted styles just a little makes integrating with a Material UI defined theme easy. This approach is also very easily adapted to any other theme implementation.

```
const makeTemplateLiteralStyles = (theme: Theme) => {
  return {
    card: css`
      padding: 2em;
    `,
    readTheDocs: css`
      color: 'templateStyles.invalid';
      font-weight: ${theme.typography.fontWeightBold};
    `,
  }
}

export function App() {
  const theme = useTheme()
  const styles = makeTemplateLiteralStyles(theme)
```

This change also enables any dynamic value to be used as a factor in the styles creation. For example:
```
const makeTemplateLiteralStyles = (theme: Theme) => {
  const cardLayoutSetting =
    theme.cardLayoutDirection === 'row' ? 'center' : 'flex-start'

  return {
    card: css`
      display: flex;
      flex-flow: ${theme.cardLayoutStyle};
      justify-content: ${cardLayoutSetting};
      padding: 2em;
    `,
    ...
  }
}

export function App() {
  const theme = useTheme()
  const styles = makeTemplateLiteralStyles(  {
    ...theme,
    cardLayoutDirection: 'row',
  })
```

While this functions exactly as intended, this is where I think Stylelint and the CSS-in-JS implementation start to diverge. The super useful `declaration-property-value-no-unknown` Stylelint rule can not verify dynamically assigned property values. Or at least I was not yet able to find a configuration that enables this.

Emotion CSS has it's own [theming capability](https://emotion.sh/docs/theming) though I think the more comprehensive, and structured, MUI implementation is preferable. Both MUI and Emotion CSS use [CSSType](https://www.npmjs.com/package/csstype) to ensure type safety which should result in invalid theme properties being caught in the build process. Though helpful I would prefer if this could be integrated into the same style linting process

### 8. Create a utility to simplify style implementation {#style-utility}
Undettered I pressed on with a further evolution of the extracted styles. As well as using literal templates, Emotion CSS enables the declaration of styles with camelCase object notation. My previous experience with JSS drew me towards this option. While exploring this it occurred to me to try creating a small utility function to simplify the creation of styles another step. This function automatically completes the Emotion `css` serialisation, removing the need to enclose each style object individually.

`utils.ts`
```
import { css, CSSObject, SerializedStyles } from '@emotion/react'

export type StylesObject = Record<string, CSSObject>
export type SerialisedStylesObject = Record<string, SerializedStyles>

const cssProps = (styles: StylesObject): SerialisedStylesObject => {
  return Object.entries<CSSObject>(styles).reduce((acc, [selector, properties]) => {
    acc[selector] = css(properties)
    return acc
  }, {})
}
```

This function is then used to automatically complete the Emotion `css` serialisation. However, while this functions as intended the runtime nature of this implementation means it can not be linted by Stylelint's static analysis. Apparently [Stylis](https://www.npmjs.com/package/stylis) is [a potential option](https://github.com/emotion-js/emotion/issues/1944) but that is a rabbit hole for another day.
```
const makeObjectStyles = (theme: Theme): SerialisedStylesObject => {
  return cssProps({
    card: {
      padding: 'styles.invalid', // '2em',
    },
    readTheDocs: {
      fontWeight: theme.typography.fontWeightBold,
      color: '#888',
    },
  })
}
```

## Final Thoughts
I am pleased with the development experience that has been achieved. However, the lack of automated linting over the themed properties and the [most streamlined DevEx](#style-utility) would be a major concern if considering this for a large production project.

In a broader context, this experiment has served as a reminder of how precarious and "magical" much of the web toolchain is. Don't get me wrong, I am greatly appreciative of the community that has built these tools and made them freely available. Rather this is a reflection on how much more I have to learn. With a better understanding of these tools and how they integrate I would hope to be better able to identify where the gaps are and how to address them.  With that I would then be delighted with this approach to creating and maintaining web application styles.

Not wanting to stray any further outside the time box I set for this experiement I must draw a line under this for now. While this has been informative it hasn't been definitive, there are several more rabbit holes yet to explore before this could be bottomed out.

## Take aways

- Emotion CSS is feature rich, and serves a broad range of user configurations

- Stylelint v.15 brought some [notable changes](https://stylelint.io/migration-guide/to-15/#significant-changes), along with several [breaking changes](https://stylelint.io/migration-guide/to-15#breaking-changes)

- [postcss-styled-syntax](https://www.npmjs.com/package/postcss-styled-syntax) steps up to replace the deprecated [@stylelint/postcss-css-in-js](https://github.com/stylelint/postcss-css-in-js)

- For web application development I think the CSS-in-JS option is still a viable one if the linting issues can be satisfactorially resolved

- Tooling is never a finished task, it requires periodic review and investment to ensure work aides don't become drags


### References:

- [Why We're Breaking Up with CSS-in-JS](https://dev.to/srmagura/why-were-breaking-up-wiht-css-in-js-4g9b)
