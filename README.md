# Themes for Marp

[Marp](https://marp.app/) is great but its included themes are horrid. This is a home for additional
themes.

## Themes

- [Clean](clean/README.md) - A clean and simple theme for Marp presentations. It is designed to be
  easy to read and visually appealing, with a focus on clean typography and layout.

## How to Use

I use [VS Code](https://code.visualstudio.com/) to author Marp presentations, with the
[Marp for VS Code](https://marketplace.visualstudio.com/items/?itemName=marp-team.marp-vscode)
extension. This setup works pretty well, but has one (*) very annoying flaw: the setup for custom
themes is overly cumbersome. Custom themes should be able to be specified as simple paths relative
to the Marp markdown file, or URLs in the markdown. Themes should be able to be found and used without
any setup. The author should be able to choose a theme and expect that anyone viewing the Marp
slides would see the slides with that theme applied. That isn't how Marp works, however. Using the
VS Code extension, everyone viewing the slides has to very manually and painfully set workspace
settings for the path of the custom theme the author chose. And using the Marp CLI, everyone
viewing the slides has to manually specify the theme as well.

This makes it frustratingly difficult to create and share Marp slides. It makes Marp significantly
worse than Powerpoint or Google Slides or any other slide-authoring solution. In every other
slide-authoring system, the typefaces, font sizes, colors, and layout of your slides is stored in
the presentation. Everyone viewing presentations in any other system sees what the author intended.
But not in Marp. In Marp, every author and every viewer must spend 10 minutes every time they open a
Marp presentation, to teach Marp how to find the theme file that is sitting right next to the
markdown file, or to reference a theme published on the web. A lot of the benefit of Marp is "it
just works" - this is a glaring exception to that.

So until Marp matures, you can "install" the Marp themes in this repo by adding the following to
your VS Code workspace `.vscode/settings.json` file:

```
{
    "markdown.marp.themes": [
        "https://raw.githubusercontent.com/osievert/marp-themes/main/clean/theme.css"
    ]
}
```

If you don't want to rely on being internet-connected, you could also clone this repo to your
computer and reference the themes by filesystem path.

```
{
    "markdown.marp.themes": [
        "./path/to/marp-themes/clean/theme.css"
    ]
}
```

Just note that if you clone this repo, the local filesystem path you set in your workspace
`settings.json` file must be a relative path from the root of the workspace, and must point to a
path inside the workspace. You cannot use absolute paths. You cannot use `../` to escape the
workspace directory.

Additionally, you cannot configure your VS Code global settings to globally install
Marp themes. Marp themes can ONLY be installed in a workspace. This means that if you want to use
these themes in multiple workspaces, you have to install them in each workspace. This is a pain, but
it is the way it is.

Because of all of this, the easiest way to use custom themes is to reference them by URL (first option). Otherwise, you not only have to change the VS Code settings for each workspace, but you also have to clone this repo to each workspace.

Either way, once you have configured your VS Code workspace, you can then reference custom themes in
your Marp markdown preamble just like you would a built-in theme:

```
---
marp: true
theme: clean
... (whatever other config you like)
---

...
```

Then you can preview your slides with the standard VS Code markdown preview command 
(`Markdown: Open Preview to the Side`). You can also export your slides to PDF or HTML with the
command `Marp: Export Slide Deck...`. If you are new to Marp, clone this repo and try it with the
included example slides!


(*) OK I lied - this setup using VS Code has one more annoying flaw. The VS Code markdown preview is
not page aware, so you cannot navigate the resulting slides by page. Instead, the VS Code markdown
preview implements continuous scrolling. This works, but is annoying when working with slides. 99%
of the time, slides want to be navigated by full page. PDF viewers understand this and give users
the option to navigate by page or continuously. Hopefully VS Code learns this trick at some point.
