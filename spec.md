# Formdown Specification

*v0.0.1*

## Form block

A form is a block of plain text distict from the rest of the document. In regular Markdown an equivalent pattern is established with three back-ticks for a code block indicating it should be wrappd in a `pre` element and `code` element. Formdown uses three question marks to accomplish a similar outcome.

```markdown
???
???
```

The output of the above in HTML should be:

```html
<form></form>
```

Without a `method` or `action` attribute an HTML form becomes problematic; therefore, another pattern is employed. Attributes can be added on the next line following the form block. There must not be a blank line between them as a blank line betwee the end of the block and next visible character denotes the form has ended. The attribute list should use JavaScript Notation (JSON) and can be applied to any other component or element.

```markdown
???
???
{method:"post",action:"https://8fold.pro"}
```


```html
<form method="post" action="https://8fold.pro"></form>
```

## Form Elements

Form Elements are comprised of two to three parts, in this order:

1. A label
2. The form control
3. Optional attributes using JavaScript Notation

In most cases, form elements are separated from one another by one or more blank lines. Mixing types of elements in a single form element is not allowed. In other words, a multi-line text field cannot incorporate a select field; instead, the first element to be presented will be used and processed as such until reaching the next blank line.

In most cases, the sub-elements of a form element are separated by a single line return character (not a blank line).

By default, form elements are considered required (otherwise why would they be there). To mark a field as optional, prepend the label with a tilde (~) follwed by a space.

### Text Fields

Typically rendered as rectangular elements for accepting either a single line or text, or multiple lines of text. 

To avoid collision with other flavors of Markdown while communicating intent in the plain text file, text fields begin with a single pipe (|) followed by two or more underscores (__). If text is placed as a pre-filled value, the second underscore should be followed by one or more spaces.

#### Input Text (single line)

```markdown
|________________

|________________
{type:"password"}

|__ Hello, World! 

Full
|__ Hello, World! 
{name:"input-field"}
```

```html
<input type="text" required>

<input type="password" required>

<input type="text" value="Hello, World!" required>

<label for="input-field">Full</label>
<input type="text" value="Hello, World!" name="input-field" required>
```

#### Textarea (multi-line)

```markdown
|________________
|________________

|__ Hello, World! 
|________________

Full
|__ Hello, World!
|________________ 
{cols:50, rows:50, disabled:disabled}
```

```html
<textarea required></textarea>

<textarea required>Hello World!</textarea>

<label>Full</label>
<textarea cols="50" rows="50" disabled required>Hello World!</textarea>
```

### Select Fields

Typically ask the user filling out the form to "check off" pre-determined values rather than input values freehand. There are two main types of select fields within a form: single and multiple.

[Task Lists](https://github.github.com/gfm/#task-list-items-extension-) are a Markdown estension used to generate a todo list with checkboxes. Formdown uses the same syntax for checkboes and a similar pattern for all select renderings.

For the purposes of HTML rendering, each select item occupies a single line. Optional attributes may be placed at the end of each line.

#### Single Select

```markdown
( )
(x) This is checked
{name:"select-field"}
```

```html
<input type="radio" name="select-field" required>
<label>This is checked</label>
<input type="radio" name="select-field" required checked>
```

```markdown
{ }
{x} This is checked
{name:"select-field"}
```

```html
<select name="select-field">
    <option></option>
    <option selected>This is checked</option>
</select>
```

#### Multi-select

```markdown
[ ]
[x] This is checked
{name:"select-field"}
```

```html
<input type="checkbox" name="select-field" required>
<label>This is checked</label>
<input type="checkbox" name="select-field" required checked>
```

```markdown
[{ }]
[{x}] This is checked
{name:"select-field"}
```

```html
<select name="select-field" multiple>
    <option></option>
    <option selected>This is checked</option>
</select>
```

### Buttons

Buttons, as a purely interactive element become almost useless in a print format. However, buttons often represent a call to action as well: ex. Submit feedback. From an HTML perspective, there are five button variations, the standalone button element and four input types that render as buttons. 

Formdown only recognizes two, as the others can be achieved via attribute lists.

#### Submit Button

```markdown
}} submit {{
```

```html
<button>submit</button>
```

#### Reset Button

```markdown
}X submit X{
```

```html
<input type="rest" value="submit">
```

### Other Form Controls and Elements

#### Fieldset

Used to wrap a group of form components when multiple labels might help users better understand the form.

```markdown
--- Fieldset legend text ---
---
```

```html
<fieldset>
    <legend>Fieldset legend text</legend>
</fieldset>
```

#### Range

Instructs those completing the form to choose a value between two extremes.

```markdown
<- 0-100 ->
```

```html
<input type="range" min="0" max="100">
```

#### File Upload

Similar to buttons, only makes sense once transpiled and only if uploading files makes sense in the context.

```markdown
|^
```

```html
<input type="file">
```

#### Hidden

```markdown
|X value X|
{name:"name"}
```

```html
<input type="hidden" name="name" vlue="value">
```

#### Color

```markdown
|% %|
```

```html
<input type="color">
```

## Example

The following form incorporates the common elements above to demonstrate visual nature of the plain text rendering as a standalone, usable form.

```markdown
# Change of Address Form

Please complete the following form to begin receiving mail at your *new* address.

???
Occupant name
|                                         |

--- Current Address ---
Street address (and unit)
|                                         |
{name:"address"}

City
|                                         |
{name:"city"}

Region
|                                         |
{name:"region"}

Postal code
|                                         |
{name:"code"}
---

--- New Address ---
Street address (and unit)
|                                         |

City
|                                         |
{name:"city2"}

Region
|                                         |
{name:"region2"}

Postal code
|                                         |
{name:"code2"}
---
???

**Note:** You must drop this off at a post office or with a postal employee before this takes effect. You can also submit this online at our website.
```

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
