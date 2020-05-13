# Formdown Specification

*v0.0.1*

## Form block

A form is a block of plain text distict from the rest of the document. In regular Markdown an equivalent pattern is established with three back-ticks for a code block indicating it should be wrappd in a `pre` element and `code` element. Formdown uses three question marks to accomplish a similar outcome.

```markdown
???
???
```

The output oof the above in HTML should be:

```html
<form></form>
```

Without a `method` or `action` attribute an HTML form becomes problematic; therefore, another pattern is employed.

```markdown
???post|https://8fold.pro
???
```


Results in:

```html
<form method="post" action="https://8fold.pro"></form>
```

By encapsulating the form in a block, Formdown parsers can be written separately from and plugged into standard Markdown parser pipelines.

## Form Components

A form component is comprised of the HTML form element itself (ex. `input`) and the `label` for the element. A typical pattern for form components consists of linking the `label` and the element by way of three attributes. The `for` attribute goes on the `label` while the `id` and `name` attributes appear on the form element itself; typically with the same value for each. Formdown uses the pattern above along with whitespace to accomplish the same thing.

```markdown
???
Label|name
|   |
???
```

```html
<form>
    <label for="name">Label</label>
    <input id="name" name="name" type="text" required>
</form>
```

A more complex form component can be seen in a `fieldset`. Because this has accessibility implications in the HTML world, we want to use a wrapper here as well.

```markdown
???
--- Fieldset Legend ---
Name|name
|   |

Address|address
|   |

Phone number
|    |
---
???
```

```html
<form>
    <fieldset>
        <legend>Fieldset Legence</legend>
        <label for="name">Name</label>
        <input id="name" name="name" type="text" required>
        <label for="address">Address</label>
        <input id="address" name="address" type="text" required>
        <label for="phone">Phone number</label>
        <input id="phone" name="phone" type="text" required>
    </fieldset>
</form>
```

By default, all fields are considered required (otherwise, why are they there?). To denote a field as optional, prepend the label with a tilde (~) followed by one space.

```markdown
???
~ Label|name
|   |
???
```

```html
<form>
    <label for="name">Label</label>
    <input id="name" name="name" type="text">
</form>
```

Part of the argument in favor of Markdwon is that no special equipment is required and there is only a minimal amount of knowledge required to generate full, rich documents, with or without the Internet. As such, Formdown should follow suit as much as possible. The following example is a form inside a larger Markdown document.

```markdown
# Change of Address Form

Please complete the following form to begin receiving mail at your *new* address.

???
Occupant name
|                                         |

--- Current Address ---
Street address (and unit)|address
|                                         |

City|city
|                                         |

Region|region
|                                         |

Postal code|code
|                                         |
---

--- New Address ---
Street address (and unit)
|                                         |

City|city2
|                                         |

Region|region2
|                                         |

Postal code|code2
|                                         |
---
???

**Note:** You must drop this off at a post office or with a postal employee before this takes effect. You can also submit this online at our website.
```

If there's a zombie apocalypse that crashes the Internet chances are you wouldn't need to change your address, but let's say you do - the same, printed form could be used. And, if the web returns, any changes made over time can be updated and fed through the same code to generate an updated form.

```html
<h1>Change of Address Form</h1
<p>Please complete the following form to begin receiving mail at your <em>new</em> address.</p>
<form>
    <label for="name">Name</label>
    <input id="name" name="name" type="text">
    <fieldset>
        <legend>Current Address</legend>
        <label for="address">Street address (and unit)</label>
        <input id="address" name="address" type="text" required>
        <label for="city">City</label>
        <input id="city" name="city" type="text" required>
        <label for="region">Region</label>
        <input id="region" name="region" type="text" required>
        <label for="code">Postal code</label>
        <input id="code" name="code" type="text" required>
    </fieldset>
    <fieldset>
        <legend>New Address</legend>
        <label for="address2">Street address (and unit)</label>
        <input id="address2" name="address2" type="text" required>
        <label for="city2">City</label>
        <input id="city2" name="city2" type="text" required>
        <label for="region2">Region</label>
        <input id="region2" name="region2" type="text" required>
        <label for="code2">Postal code</label>
        <input id="code2" name="code2" type="text" requireds>
    </fieldset>
</form>
<p><strong>Note:</strong> You must drop this off at a post office or with a postal employee before this takes effect. You can also submit this online at our website.</p>
```

Let's look at individual form elements.

## Form Elements

### Input (text)

Probably the most common element the `text input` field is denoted by being on its own line and consisting of at least two pipes (vertical bars) separated by at least one space. To prefill the value, place text between the pipes with at least one leading space. 

Note: It does not matter how many spaces are between the pipes so long as the line starts and ends with a pipe and has at least one leading space before any content between.

```markdown
|              |

| Helo, World! |
```

```html
<input type="text" required>

<input type="text" value="Hello, World!" required>
```

### Input (variable types)

Some input types are represented as text fields, but are a more specific type. These more specific types help modern browsers validate the form for you. The following Formdown patterns can be used to achieve those more specific types.

#### Email

```markdown
|@              |
```

```html
<input type="email" required>
```

#### Number

```markdown
|#               |
```

#### Phone number

```markdown
|@#              |
```

### Textarea

The `textarea` element represents multi-line text and uses the text field pattern as the base. For lack of a better explanation, if two or more text fields are placed on consecutive lines, they become a `textarea`.

```markdown
|              |
|              |
```

```html
<textarea required></textarea>
```

