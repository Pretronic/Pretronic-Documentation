---
title: Installation
---

# Installation

The installation is very easy and can be done with the npm or yarn packet manager.
You can find the package on [npmjs](https://www.npmjs.com/package/@pretronic/react-github-languages).


=== "npm"

    ```
    npm install @pretronic/react-github-languages
    ```

=== "yarn"

    ```
    yarn add @pretronic/react-github-languages
    ```

## Language provider setup

After the installation you should warp your app code with the `LanguageProvider`, this wrapper component is responsible for the language management and passes the translations to the `Message` components.

The `repository` property must contain the name of your GitHub repository, see the [repository-setup](repository-setup) guide 
to get more information about the structure. 

Finally, pass the selected language (code) of your user to the language provider with the `language` property.

```typescript
import React from 'react';
import {LanguageProvider} from "@pretronic/react-github-languages";

export default class App extends React.Component<{}, {}> {


  render() {
    return(<LanguageProvider repository={"Pretronic/PretronicAccountTranslations"} branch={"main"} language={"en"} >

      /* Your app code comes here */

    </LanguageProvider>)
  }
}
```

Read more about how to use a message [message](messages).

### Properties

| Property            | Description                                           |
| --------------------| ------------------------------------------------------|
| `repository`        | The name of your GitHub repository                    |
| `branch`            | The name of the branch (usually main)                 |
| `language`          | The selected language                                 |
| `fallbackLanguage`  | The fallback language if the message is not available in the selected language  |
