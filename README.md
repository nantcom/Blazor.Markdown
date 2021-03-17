# Blazor.Markdown [![NuGet](https://img.shields.io/badge/nuget-v1.0.0-blue)](https://www.nuget.org/packages/Blazor.Markdown/)
Safely Rendering Markdown in BLazor using Razor Component Library

### Before using Library
This project is not my idea to begin with but due to need of displaying markdown as HTML DOM on my other project
I found a post by [JON BLANKENSHIP](https://blog.jonblankenship.com/2019/01/27/safely-rendering-markdown-in-blazor/)
following his post I have created **Blazor.Markdown** project to fill my need and hope fully this project would be 
useful to other developers.

### Wny using Blazor.Markdown
It’s important to sanitize any user-supplied HTML that you will be rendering back as raw HTML to
prevent malicious users from injecting scripts into you app and making it vulnerable to cross-site
scripting (XSS) attacks. For this task, I use [HtmlSanitizer](https://github.com/mganss/HtmlSanitizer)
, an actively-maintained, highly-configurable .NET library.

### This project using following Libraries
- [Markdig](https://github.com/lunet-io/markdig) - 
 “a fast, powerful, CommonMark compliant, extensible Markdown processor for .NET.”
- [HtmlSanitizer](https://github.com/mganss/HtmlSanitizer) - 
  “a .NET library for cleaning HTML fragments and documents from constructs that can lead to XSS attacks.”

### Download
Blazor.Markdown is available as a NuGet package: [![NuGet](https://img.shields.io/badge/nuget-v1.0.0-blue)](https://www.nuget.org/packages/CoreSharp.ContentToolsJs.Editor/)

## Usage
Add the following using statement to your main `_Imports.razor`

```cs
@using Blazor.Markdown
```

Open `StartUp.cs` in your project and add service of `HtmlSanitizer` as Scoped

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages();
    services.AddServerSideBlazor();
    ...
    services.AddScoped<IHtmlSanitizer, HtmlSanitizer>(x =>
    {
        // Configure sanitizer rules as needed here.
        // For now, just use default rules + allow class attributes
        var sanitizer = new Ganss.XSS.HtmlSanitizer();
        sanitizer.AllowedAttributes.Add("class");
        return sanitizer;
    });
}
```

Binding a Markdown string to rendering HTML DOM:
```html
<MarkdownView Content="@MarkdownString"/>
```