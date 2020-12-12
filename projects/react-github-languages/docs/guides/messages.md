---
title: Messages
---

# Messages

The `Message` object is used to replace a conventional message with a configured translatable message.

The `name` property must contain the name of your message key configured in the translation file. Optionally, you 
can pass variables to your message, which will be replaced and converted to a string.

```
<Message name={"settings.name"} variables={{name: "Jack"}} />
```

### Example

This example shows how you can replace your current messages with translatable messages.

=== "Before"

    ```typescript
    <div>
        <p>Hello {name}, how are you?</p>
    </div>
    ```

=== "After"

    ```typescript
    <div>
         <p> <Message name={"question"} variables={{name: "Jack"}} /> </p>
    </div>
    ```

The configured translation file will look similar to this:

```json
{
  "name": "English",
  "localName": "English",
  "code": "en",
  "messages": {
    "question": "Hello {name}, how are you?"
  }
}
```


## Properties

| Property      | Description                                           |
| --------------| ------------------------------------------------------|
| `name`        | The name is the key of the message                    |
| `variables`   | Variables to be replaced in the message               |
| `default`     | A default message if the message could not be found   |

