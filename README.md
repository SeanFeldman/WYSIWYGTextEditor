# Blazored TextEditor
Rich text editor for Blazor applications - Uses [Quill JS](https://quilljs.com/ "Quill JS.com")

![Screenshot](HTMLExample.png)


### Helpful Articles

* [Creating Reusable Custom Blazor Controls](http://blazorhelpwebsite.com/Blog/tabid/61/EntryId/4365/Creating-Reusable-Custom-Blazor-Controls.aspx "BlazorHelpWebsite.com")
* [Creating A Rich Text Editor In Blazor Using Quill](http://blazorhelpwebsite.com/Blog/tabid/61/EntryId/4364/Creating-A-Rich-Text-Editor-In-Blazor-Using-Quill.aspx "BlazorHelpWebsite.com")

### Installing

You can install from NuGet using the following command:

`Install-Package Blazored.TextEditor`

Or via the Visual Studio package manger.

### Setup
Blazor Server applications will need to include the following CSS and JS files in their `Pages\_Host.cshtml`.

In the `head` tag add the following CSS.

```html
    <link href="//cdn.quilljs.com/1.3.6/quill.snow.css" rel="stylesheet">
    <link href="//cdn.quilljs.com/1.3.6/quill.bubble.css" rel="stylesheet">
```

Then add the JS script at the bottom of the page using the following script tag.

```html
    <script src="https://cdn.quilljs.com/1.3.6/quill.js"></script>
    <script src="_content/Blazored.TextEditor/Blazored-BlazorQuill.js"></script>
```

**NOTE** If you're using Blazor WebAssembly then these need to be added to your `wwwroot\index.html`.

You can add the following using statement to your main `_Imports.razor` to make referencing the component a bit easier.

```cs
@using Blazored.TextEditor
```

## Usage

Below is a list of all the options available on the Text Editor.

**Templates**

- `ToolbarContent` (optional) - Allows the user to define the Toolbar (above the editor control, or in-line when using the bubble theme, and a user highlights text in the editor).
- `EditorContent` (Required) - Allows the user to define the initial content

**Parameters**

- `ReadOnly` (Optional - Default: `false`) - Determines if the editor will load in read-only mode. This mode can be toggled.
- `Placeholder` (Optional - Default: `Compose an epic...`) - The text to show when editor is empty.
- `Theme` (Optional - Default: `snow`) - Use `snow` to show the Toolbar on top of the editor, and `bubble` for inline editing.
- `DebugLevel` (Optional - Default: `info`) - Determines the level of debug information returned to the web browser console window. Options are `error`, `warn`, `log`, or `info`.


### Basic Example
(see code in the [Index.razor page](https://github.com/Blazored/TextEditor/blob/master/samples/BlazorServerSide/Pages/Index.razor) in the repo for more examples)
```cs
@using Blazored.TextEditor

<BlazoredTextEditor @ref="@QuillHtml">
    <ToolbarContent>
        <select class="ql-header">
            <option selected=""></option>
            <option value="1"></option>
            <option value="2"></option>
            <option value="3"></option>
            <option value="4"></option>
            <option value="5"></option>
        </select>
        <span class="ql-formats">
            <button class="ql-bold"></button>
            <button class="ql-italic"></button>
            <button class="ql-underline"></button>
            <button class="ql-strike"></button>
        </span>
        <span class="ql-formats">
            <select class="ql-color"></select>
            <select class="ql-background"></select>
        </span>
        <span class="ql-formats">
            <button class="ql-list" value="ordered"></button>
            <button class="ql-list" value="bullet"></button>
        </span>
        <span class="ql-formats">
            <button class="ql-link"></button>
        </span>
    </ToolbarContent>
    <EditorContent>
        <h4>This Toolbar works with HTML</h4>
        <a href="http://BlazorHelpWebsite.com">
        BlazorHelpWebsite.com</a>
    </EditorContent>
</BlazoredTextEditor>
<br />
<button class="btn btn-primary" 
        @onclick="GetHTML">Get HTML</button>
<br />
<div>
    <br />
    @((MarkupString)QuillHTMLContent)
    @QuillHTMLContent
</div>
<br />

@code {

BlazoredTextEditor QuillHtml;
string QuillHTMLContent;

    public async void GetHTML()
    {
        QuillHTMLContent = await this.QuillHtml.GetHTML();
        StateHasChanged();
    }
}
```
### Rich Text Screenshot
![Screenshot](DeltaExample.png)
### Read Only Screenshot
![Screenshot](InlineEditingExample.png)
