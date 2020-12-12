---
title: Language List
---

# Language List

Now, if you want to give your users the possibility to choose their preferred language, you can use the 
object `LanguageList` to list all available languages.

The `LanguageList` contains all languages from the languages.json file.

```typescript
<LanguageList render={languages => {
    return <ul>
        {languages.map(language => {
            return (<li>{language.name}</li>)
        })}
    </ul>
}} />
```


