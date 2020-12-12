---
title: Repository setup
---

# Repository setup

As the name of the project says, the library consumes language files 
directly from a GitHub repository, you need to create a new repository for this.

If you don't know how to create a repository, use
[this guide](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/create-a-repo) from GitHub.

## Language configuration 

Now let's start configuring your repository. For the first step, you need to define all your languages in the language.json.
Create a new entry for each language and push the finished file (languages.json) to your repository.

```json
{
  "languages": [
    {
      "name": "English",
      "localName": "English",
      "code": "en"
    },
    {
      "name": "German",
      "localName": "Deutsch",
      "code": "de"
    }
  ]
}
```

You can use the command line or add the file directly to the repository, see [this guide](https://docs.github.com/en/free-pro-team@latest/github/managing-files-in-a-repository/adding-a-file-to-a-repository)
if you don't know how to upload a file to a GitHub repository.

## Create a new language file

After configuring the languages, create a new translation file (code.json / en.json) for each language and push it back to your repository.

```json
{
  "name": "English",
  "localName": "English",
  "code": "en",
  "messages": {
    "settings.title": "Settings",
    "settings.name": "Your name is {name}"
  }
}
```

## Final repository
Your repository should now look something like the picture, you can also find an example repository [here](https://github.com/Pretronic/PretronicAccountTranslations)

!!! warning ""
Make sure that your repository is public.


![Example repository]({{config.site_url}}images/example-repo.png)
