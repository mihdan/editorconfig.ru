EditorConfig
============

What is EditorConfig?
---------------------

EditorConfig helps maintain consistent coding styles for multiple developers working on the same project across various editors and IDEs. The EditorConfig project consists of **a file format** for defining coding styles and a collection of **text editor plugins** that enable editors to read the file format and adhere to defined styles. EditorConfig files are easily readable and they work nicely with version control systems.

What's an EditorConfig file look like?
--------------------------------------

_(A [formal specification of EditorConfig](https://editorconfig-specification.readthedocs.io/) is also available.)_

### Example file

Below is an example `.editorconfig` file setting end-of-line and indentation styles for Python and JavaScript files.

    # EditorConfig is awesome: https://EditorConfig.org
    
    # top-most EditorConfig file
    root = true
    
    # Unix-style newlines with a newline ending every file
    [*]
    end_of_line = lf
    insert_final_newline = true
    
    # Matches multiple files with brace expansion notation
    # Set default charset
    [*.{js,py}]
    charset = utf-8
    
    # 4 space indentation
    [*.py]
    indent_style = space
    indent_size = 4
    
    # Tab indentation (no size specified)
    [Makefile]
    indent_style = tab
    
    # Indentation override for all JS under lib directory
    [lib/**.js]
    indent_style = space
    indent_size = 2
    
    # Matches the exact files either package.json or .travis.yml
    [{package.json,.travis.yml}]
    indent_style = space
    indent_size = 2

Check the Wiki for some real-world examples of [projects using EditorConfig files](https://github.com/editorconfig/editorconfig/wiki/Projects-Using-EditorConfig).

### Where are these files stored?

When opening a file, EditorConfig plugins look for a file named `.editorconfig` in the directory of the opened file and in every parent directory. A search for `.editorconfig` files will stop if the root filepath is reached or an EditorConfig file with `root=true` is found.

EditorConfig files are read top to bottom and the most recent rules found take precedence. Properties from matching EditorConfig sections are applied in the order they were read, so properties in closer files take precedence.

**For Windows Users:** To create an `.editorconfig` file within Windows Explorer, you need to create a file named `.editorconfig.` (note the trailing dot), which Windows Explorer will automatically rename to `.editorconfig` for you.

### File Format Details

EditorConfig files use an INI format that is compatible with the format used by [Python ConfigParser Library](https://docs.python.org/2/library/configparser.html), but `[` and `]` are allowed in the section names. The section names are filepath [globs](https://en.wikipedia.org/wiki/Glob_(programming)) (case sensitive), similar to the format accepted by [gitignore](https://git-scm.com/docs/gitignore#_pattern_format). Only forward slashes (`/`, not backslashes) are used as path separators and octothorpes (`#`) or semicolons (`;`) are used for comments. Comments should go on their own lines. EditorConfig files should be UTF-8 encoded, with either `CRLF` or `LF` line separators. EditorConfig files are read top to bottom and the most recent rules found take precedence.

Filepath glob patterns and currently-supported EditorConfig properties are explained below.

#### Wildcard Patterns

Special characters recognized in section names for wildcard matching:

`*`

Matches any string of characters, except path separators (`/`)

`**`

Matches any string of characters

`?`

Matches any single character

`[name]`

Matches any single character in _name_

`[!name]`

Matches any single character not in _name_

`{s1,s2,s3}`

Matches any of the strings given (separated by commas) (**Available since EditorConfig Core 0.11.0**)

`{num1..num2}`

Matches any integer numbers between _num1_ and _num2_, where num1 and num2 can be either positive or negative

Special characters can be escaped with a backslash so they won't be interpreted as wildcard patterns.

#### Supported Properties

Note that not all properties are supported by every plugin. The wiki has a [complete list of properties](https://github.com/editorconfig/editorconfig/wiki/EditorConfig-Properties).

*   `indent_style`: set to tab or space to use hard tabs or soft tabs respectively.
*   `indent_size`: a whole number defining the number of columns used for each indentation level and the width of soft tabs (when supported). When set to tab, the value of **`tab_width`** (if specified) will be used.
*   `tab_width`: a whole number defining the number of columns used to represent a tab character. This defaults to the value of **`indent_size`** and doesn't usually need to be specified.
*   `end_of_line`: set to lf, cr, or crlf to control how line breaks are represented.
*   `charset`: set to latin1, utf-8, utf-8-bom, utf-16be or utf-16le to control the character set.
*   `trim_trailing_whitespace`: set to true to remove any whitespace characters preceding newline characters and false to ensure it doesn't.
*   `insert_final_newline`: set to true to ensure file ends with a newline when saving and false to ensure it doesn't.
*   `root`: special property that should be specified at the top of the file outside of any sections. Set to true to stop `.editorconfig` files search on current file.

Currently all properties and values are case-insensitive. They are lowercased when parsed. Generally, if a property is not specified, the editor settings will be used, i.e. EditorConfig takes no effect on that part. For any property, a value of unset is to remove the effect of that property, even if it has been set before. For example, add `indent_size = unset` to undefine **`indent_size`** property (and use editor default).

It is acceptable and often preferred to leave certain EditorConfig properties unspecified. For example, **`tab_width`** need not be specified unless it differs from the value of **`indent_size`**. Also, when **`indent_style`** is set to tab, it may be desirable to leave **`indent_size`** unspecified so readers may view the file using their preferred indentation width. Additionally, if a property is not standardized in your project (**`end_of_line`** for example), it may be best to leave it blank.

No Plugin Necessary
-------------------

These editors come bundled with native support for EditorConfig. Everything should just work.

*   [![BBEdit](logos/bbedit.png)BBEdit](http://barebones.com/support/technotes/editorconfig.html)
*   [![Code Crusader](logos/code-crusader.png)Code Crusader](https://sourceforge.net/projects/codecrusader/)
*   [![CodeLite](logos/codelite.png)CodeLite](https://github.com/eranif/codelite/tree/master/EditorConfigPlugin)
*   [![elementary Code](logos/elementary-code.png)elementary Code](https://github.com/elementary/code#readme)
*   [![GNOME Builder](logos/gnome-builder.png "GNOME Builder")GNOME Builder](https://wiki.gnome.org/Apps/Builder/Features#EditorConfig)
*   [![Gitea](logos/Gitea.png)Gitea](https://gitea.io/)
*   [![GitHub](logos/github.png "GitHub (code viewer and editor)")GitHub](https://github.com/RReverser/github-editorconfig#readme)
*   [![GitLab](logos/gitlab.png "GitLab")GitLab](https://docs.gitlab.com/ee/user/project/web_ide/index.html#configure-the-web-ide)
*   [![GitBucket](logos/gitbucket.png)GitBucket](https://gitbucket.github.io/)
*   [![Gogs](logos/gogs.png)Gogs](https://gogs.io)
*   [![intelliJ logo](logos/intellijIDEA.png)intelliJ](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig)
*   [![jdTextEdit logo](logos/jdTextEdit.png)jdTextEdit](https://gitlab.com/JakobDev/jdTextEdit)
*   [![KTextEditor](logos/ktexteditor.png)KTextEditor](https://api.kde.org/frameworks/ktexteditor/html/)
*   [![Komodo](logos/komodo.png)Komodo](https://www.activestate.com/blog/2015/07/editorconfig-your-komodo)
*   [![Kakoune](logos/kakoune.png)Kakoune](https://github.com/mawww/kakoune/wiki/EditorConfig/)
*   [![MonoDevelop](logos/monodevelop.png)MonoDevelop](https://github.com/mikerochip/editorconfig-monodevelop#readme)
*   [![Nova](logos/nova.png)Nova](https://nova.app/)
*   [![PyCharm](logos/pyCharm.png)PyCharm](https://plugins.jetbrains.com/plugin/7294)
*   [![ReSharper](logos/reSharper.png)ReSharper](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig)
*   [![Rider](logos/rider.png)Rider](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig)
*   [![RubyMine](logos/rubyMine.png)RubyMine](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig)
*   [![sourcehut](logos/sourcehut.png)sourcehut](https://sourcehut.org/)
*   [![SourcLair](logos/sourcelair.png)SourcLair](https://www.sourcelair.com/features/editorconfig)
*   [![TortoiseGit](logos/TortoiseGit.png)TortoiseGit](https://tortoisegit.org/)
*   [![Visual Studio Pro](logos/visualstudio-pro.png)Visual Studio Professional](https://docs.microsoft.com/en-us/visualstudio/releasenotes/vs2017-relnotes-v15.0#coding-convention-support-through-editorconfig)
*   [![WebStorm](logos/webStorm.png)WebStorm](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig)
*   [![Working Copy](logos/working-copy.png)Working Copy](https://workingcopy.app/)

Download a Plugin
-----------------

### Editor

To use EditorConfig with one of these editors, you will need to install a plugin.

*   [![AppCode](logos/appCode.png)AppCode](https://plugins.jetbrains.com/plugin/7294)
*   [![Atom](logos/atom.png)Atom](https://github.com/sindresorhus/atom-editorconfig#readme)
*   [![Brackets](logos/brackets.png)Brackets](https://github.com/kidwm/brackets-editorconfig/)
*   [![CLion](logos/clion.png)CLion](https://github.com/JetBrains/intellij-community/tree/master/plugins/editorconfig)
*   [![Coda](logos/coda.png)Coda](https://panic.com/coda/plugins.php#Plugins)
*   [![Code::Block](logos/codeblocks.png)Code::Block](https://github.com/editorconfig/editorconfig-codeblocks#readme)
*   [![Eclipse](logos/eclipse.png)Eclipse](https://github.com/ncjones/editorconfig-eclipse#readme)
*   [![Emacs](logos/emacs.png)Emacs](https://github.com/editorconfig/editorconfig-emacs#readme)
*   [![Far Manager](logos/far-manager.png)Far Manager](https://github.com/nightroman/FarNet/tree/master/EditorKit)
*   [![Geany](logos/geany.png)Geany](https://github.com/editorconfig/editorconfig-geany#readme)
*   [![Gedit](logos/gedit.png)Gedit](https://github.com/editorconfig/editorconfig-gedit#readme)
*   [![jEdit](logos/jedit.png)jEdit](https://github.com/editorconfig/editorconfig-jedit#readme)
*   [![Lazarus](logos/lazarus.png)Lazarus](https://github.com/skalogryz/editorConfig/tree/master/lazideext)
*   [![Micro](logos/micro.png)Micro](https://github.com/10sr/editorconfig-micro#readme)
*   [![NetBeans](logos/NetBeans.png)NetBeans](https://github.com/welovecoding/editorconfig-netbeans#readme)
*   [![Notepad++](logos/notepad.png)Notepad++](https://github.com/editorconfig/editorconfig-notepad-plus-plus#readme)
*   [![Pluma](logos/pluma.png)Pluma](https://github.com/fszymanski/pluma-plugins/tree/master/editorconfig)
*   [![PHPStorm](logos/phpStorm.png)PHPStorm](https://plugins.jetbrains.com/plugin/7294)
*   [![Sublime Text](logos/sublimetext.png)Sublime Text](https://github.com/sindresorhus/editorconfig-sublime#readme)
*   [![Textadept](logos/textadept.png)Textadept](https://github.com/editorconfig/editorconfig-textadept#readme)
*   [![TextMate](logos/textmate.png)TextMate](https://github.com/Mr0grog/editorconfig-textmate#readme)
*   [![Vim](logos/vim.png)Vim](https://github.com/editorconfig/editorconfig-vim#readme)
*   [![VSCodium](logos/vscodium.png)VSCodium](https://open-vsx.org/extension/EditorConfig/EditorConfig)
*   [![Visual Studio Code](logos/visualstudio-code.png)Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=EditorConfig.EditorConfig)

### Headless Tool

To use EditorConfig with one of these headless tools, you will need to install a plugin.

*   [![Apache Ant](logos/apache-ant.png)Apache Ant](https://github.com/ec4j/editorconfig-ant-tasks)
*   [![Gradle](logos/gradle.png)Gradle](https://github.com/ec4j/editorconfig-gradle-plugin)
*   [![Maven](logos/maven.png)Maven](https://ec4j.github.io/editorconfig-maven-plugin/)

Contributing to EditorConfig
----------------------------

### Give us your feedback

This project is greatly in need of feedback from other developers. We want to hear ideas about how to make this project better. Please use the [mailing list](http://groups.google.com/group/editorconfig) to send an email to the EditorConfig team (subscribe by shooting an email to [editorconfig+subscribe@googlegroups.com](mailto:editorconfig+subscribe@googlegroups.com)) and use the [issue tracker](https://github.com/editorconfig/editorconfig/issues) to submit bugs (but please take a look at the [FAQ](https://github.com/editorconfig/editorconfig/wiki/FAQ) first). Also feel free to [tweet at us](https://twitter.com/EditorConfig).

### Create a plugin

EditorConfig plugins can be developed by using one of the EditorConfig core libraries. The EditorConfig core libraries accept as input the file being edited, find and parse relevant `.editorconfig` files, and pass back the properties that should be used. Please ignore any unrecognized properties and property values in your editor plugin for future compatibility, since new properties and permitted values will be added in the future. Currently there is a [C library](https://github.com/editorconfig/editorconfig-core-c#readme), a [Python library](https://github.com/editorconfig/editorconfig-core-py#readme), a [JavaScript library](https://github.com/editorconfig/editorconfig-core-js#readme), two Java libraries ([EditorConfig Core Java Library](https://github.com/editorconfig/editorconfig-core-java#readme) and [ec4j](https://github.com/ec4j/ec4j#readme)), a [Lua library](https://github.com/editorconfig/editorconfig-core-lua#readme), a [.NET library](https://github.com/editorconfig/editorconfig-core-net#readme), a [Ruby library](https://github.com/editorconfig/editorconfig-core-ruby), and a [Go library](https://github.com/editorconfig/editorconfig-core-go).

If you are planning on creating a new plugin, use the [mailing list](https://groups.google.com/group/editorconfig) to let us know so we can help out and link to your plugin once it's created. If you plan on using one of the EditorConfig cores as a library or command line interface, the [C library documentation](http://docs.editorconfig.org), [Python library documentation](http://pydocs.editorconfig.org) or [Java library documentation](http://javadocs.editorconfig.org) may be helpful.

More details can be found on the [Plugin-How-To wiki page](https://github.com/editorconfig/editorconfig/wiki/Plugin-How-To).

### Main Contributors

Core libraries:

*   EditorConfig C Core: [Hong Xu](http://www.topbug.net) and [Trey Hunner](http://treyhunner.com)
*   EditorConfig Java Core: [Dennis Ushakov](https://github.com/denofevil)
*   ec4j: [Peter Palaga](https://github.com/ppalaga) and [Angelo Zerr](https://angelozerr.wordpress.com/about)
*   EditorConfig Javascript Core: [Trey Hunner](http://treyhunner.com) and [Jed Mao](http://github.com/jedmao)
*   EditorConfig Python Core: [Trey Hunner](http://treyhunner.com)
*   EditorConfig .NET Core: [Martijn Laarman](http://localghost.io/)
*   EditorConfig Ruby Core: [Joshua Peek](https://github.com/josh) and [Brian Lopez](https://github.com/brianmario)

Editor Plugins:

*   Atom plugin: [Sindre Sorhus](http://sindresorhus.com)
*   Brackets plugin: [Chen-Heng Chang](http://kidwm.net/)
*   Code::Blocks plugin: [Hong Xu](http://www.topbug.net)
*   Emacs plugin: [Trey Hunner](http://treyhunner.com), [Johan Sundström](http://ecmanaut.blogspot.com), [10sr](https://github.com/10sr)
*   Geany plugin: [Hong Xu](http://www.topbug.net)
*   Gedit plugin: [Trey Hunner](http://treyhunner.com)
*   GitHub Browser extension: [Ingvar Stepanyan](http://rreverser.com)
*   JetBrain plugin: [Kevin Bell](https://github.com/bellkev/), [Dennis Ushakov](https://github.com/denofevil)
*   jEdit plugin: [Hong Xu](http://www.topbug.net)
*   Micro plugin: [10sr](https://github.com/10sr)
*   NetBeans plugin: [Benny Neugebauer](http://www.bennyn.de/), [Michael Koppen](http://beanbelt.blogspot.de/), [Junichi Yamamoto](http://junichi11.com/)
*   Notepad++ plugin: [Hong Xu](http://www.topbug.net)
*   Sublime Text plugin: [Sindre Sorhus](http://sindresorhus.com)
*   TextMate plugin: [Rob Brackett](http://robbrackett.com)
*   Vim plugin: [Hong Xu](http://www.topbug.net), [Trey Hunner](http://treyhunner.com)
*   Visual Studio plugin: [William Swanson](http://www.swansontec.com), [nulltoken](https://github.com/nulltoken), [Martijn Laarman](http://localghost.io/), [Arkadiy Shapkin](http://kinddragon.blogspot.com), [Jed Mao](http://github.com/jedmao)
*   Visual Studio Code extension: [Jed Mao](https://github.com/jedmao), [Chris Dias](https://github.com/chrisdias)
*   Xcode plugin: [Marco Sero](http://marcosero.com/)

EditorConfig logos drawn by [Kat On](http://squirrelmuffins.com) and [Amon Keishima](https://pittankopta.net/). Website by [Trey Hunner](http://treyhunner.com) and [Hong Xu](http://www.topbug.net). Please attribute appropriately.
