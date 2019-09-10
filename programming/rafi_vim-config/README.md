# Rafael Bodill's Neo/vim Config

Lean mean Neo/vim machine, 30-45ms startup time.

Best with Neovim or Vim8 with +python3 extensions enabled.

<details>
  <summary>
    <strong>Table of Contents</strong>
    <small><i>(🔎 Click to expand)</i></small>
  </summary>

<!-- vim-markdown-toc GFM -->

* [Features](#features)
* [Screenshot](#screenshot)
* [Pre-requisites](#pre-requisites)
* [Install](#install)
  * [Recommended Fonts](#recommended-fonts)
  * [Recommended Linters](#recommended-linters)
  * [Recommended Tools](#recommended-tools)
* [Upgrade](#upgrade)
* [User Custom Config](#user-custom-config)
* [Structure](#structure)
* [Plugin Highlights](#plugin-highlights)
* [Plugins Included](#plugins-included)
  * [Non Lazy-Loaded Plugins](#non-lazy-loaded-plugins)
  * [Lazy-Loaded Plugins](#lazy-loaded-plugins)
    * [Language](#language)
    * [Commands](#commands)
    * [Interface](#interface)
    * [Completion](#completion)
    * [Denite](#denite)
    * [Operators & Text Objects](#operators--text-objects)
* [Custom Key-mappings](#custom-key-mappings)
  * [General](#general)
  * [File Operations](#file-operations)
  * [Editor UI](#editor-ui)
  * [Window Management](#window-management)
  * [Plugin: Denite](#plugin-denite)
  * [Plugin: Defx](#plugin-defx)
  * [Plugin: Deoplete and Emmet](#plugin-deoplete-and-emmet)
  * [Plugin: Caw (comments)](#plugin-caw-comments)
  * [Plugin: Edge Motion](#plugin-edge-motion)
  * [Plugin: Signature](#plugin-signature)
  * [Plugin: Easygit](#plugin-easygit)
  * [Plugin: GitGutter](#plugin-gitgutter)
  * [Plugin: Linediff](#plugin-linediff)
  * [Misc Plugins](#misc-plugins)
* [Credits & Contribution](#credits--contribution)

</details>

<!-- vim-markdown-toc -->

## Features

- Fast startup time
- Robust, yet light-weight
- Lazy-load 95% of plugins with [Shougo/dein.vim]
- Custom side-menu (try it out! <kbd>Leader</kbd>+<kbd>l</kbd>)
- Custom context-menu (try it! <kbd>;</kbd>+<kbd>c</kbd>)
- Modular configuration (see [structure](#structure))
- Denite centric work-flow (lists)
- Extensive Deoplete setup (auto-completion)
- Light-weight but informative status/tabline
- Easy customizable theme
- Premium color-schemes
- Central location for tags and sessions

## Screenshot

![Vim screenshot](http://rafi.io/static/img/project/vim-config/features.png)

## Pre-requisites

* Python 3 (`brew install python`)
* Neovim (Optional, `brew install neovim`)
* virtualenv for python3:
  ```bash
  pip3 install virtualenv
  ```
  On Ubuntu you can use:
  ```bash
  apt-get install -y python3-venv
  ```

## Install

**_1._** Let's clone this repo! Clone to `~/.config/nvim`,
we'll also symlink it for Vim:

```bash
mkdir ~/.config
git clone git://github.com/rafi/vim-config.git ~/.config/nvim
ln -s ~/.config/nvim ~/.vim
```

- _Note:_ If your system sets `$XDG_CONFIG_HOME`,
  use that instead of `~/.config` in the code above.
  Neovim follows the XDG base-directories convention.

**_2._** If you are a _first-time **Neovim** user_, you need the `pynvim`
package. Don't worry, run the script provided:

```sh
cd ~/.config/nvim
./venv.sh
```

Otherwise, or additionally, if you use Vim, you can run
`pip3 install --user pynvim`

**_3._** Run `make test` to test your nvim/vim version and compatibility.

**_4._** Run `make` to install all plugins.

**_5._** If you are experiencing problems, try running `nvim -c checkhealth`

Enjoy!

### Recommended Fonts

- [Pragmata Pro] (€19 – €1,990): My preferred font
- Any of the [Nerd Fonts]

On macOS with Homebrew, choose one of the [Nerd Fonts],
for example, to install the [Hack](https://sourcefoundry.org/hack/) font:

```bash
brew tap homebrew/cask-fonts
brew search nerd-font
brew cask install font-hack-nerd-font
```

[Pragmata Pro]: https://www.fsd.it/shop/fonts/pragmatapro/
[Nerd Fonts]: https://www.nerdfonts.com

### Recommended Linters

- Node.js based linters:

```sh
npm -g install jshint jsxhint jsonlint stylelint sass-lint
npm -g install raml-cop markdownlint-cli write-good
```

- Python based linters:

```sh
pip install --user pycodestyle pyflakes flake8 vim-vint proselint yamllint
```

- Shell lint: [shellcheck.net](https://www.shellcheck.net/)
- HTML Tidy: [html-tidy.org](http://www.html-tidy.org/)

### Recommended Tools

- ag (The Silver Searcher): [ggreer/the_silver_searcher](https://github.com/ggreer/the_silver_searcher)
- z (jump around): [rupa/z](https://github.com/rupa/z)
- Universal ctags: [ctags.io](https://ctags.io/)
- Fuzzy file finders: [fzf](https://github.com/junegunn/fzf), [fzy](https://github.com/jhawthorn/fzy), or [peco](https://github.com/peco/peco)
- Tern: `npm -g install tern`

## Upgrade

Run `make update`

## User Custom Config

If you want to add your own configuration, create the `config/local.vim` file
and add your personal settings there. If you'd like to install plugins by
yourself, create a `config/local.plugins.yaml` file and manage your own plugin
collection.

If you want to disable some of the plugins I use, you can overwrite them, e.g.:

```yaml
- { repo: benekastah/neomake, if: 0 }
```

## Structure

- [config/](./config) - Configuration
  - [plugins/](./config/plugins) - Plugin configurations
    - [all.vim](./config/plugins/all.vim) - Plugin mappings
    - […](./config/plugins)
  - [filetype.vim](./config/filetype.vim) - Language behavior
  - [general.vim](./config/general.vim) - General configuration
  - local.plugins.yaml - Custom user plugins
  - local.vim - Custom user settings
  - [mappings.vim](./config/mappings.vim) - Key-mappings
  - [plugins.yaml](./config/plugins.yaml) - _**Plugins!**_
  - [terminal.vim](./config/terminal.vim) - Terminal configuration
  - [vimrc](./config/vimrc) - Initialization
- [ftplugin/](./ftplugin) - Language specific custom settings
- [plugin/](./plugin) - Customized small plugins
- [snippets/](./snippets) - Personal code snippets
- [themes/](./themes) - Colorscheme overrides
- [filetype.vim](./filetype.vim) - Custom filetype detection

## Plugin Highlights

- Package management with caching enabled and lazy loading
- Project-aware tabs and label
- Defx as file-manager + Git status icons
- Go completion via vim-go and gocode
- Javascript completion via Tern
- Python Jedi completion, PEP8 convention
- Languages: PHP, Ansible, css3, csv, json, less, markdown, mustache, and more

_Note_ that 95% of the plugins are **[lazy-loaded]**.

## Plugins Included

### Non Lazy-Loaded Plugins

| Name           | Description
| -------------- | ----------------------
| [Shougo/dein.vim] | Dark powered Vim/Neovim plugin manager
| [rafi/awesome-colorschemes] | Awesome color-schemes
| [thinca/vim-localrc] | Enable configuration file of each directory
| [christoomey/tmux-navigator] | Seamless navigation between tmux panes and vim splits
| [romainl/vim-cool] | Simple plugin that makes hlsearch more useful
| [tpope/vim-sleuth] | Heuristically set buffer indent options
| [sgur/vim-editorconfig] | EditorConfig plugin written entirely in Vimscript
| [itchyny/vim-gitbranch] | Lightweight git branch detection
| [itchyny/vim-parenmatch] | Efficient alternative to the standard matchparen plugin
| [itchyny/cursorword] | Underlines word under cursor
| [roxma/nvim-yarp] | Remote Plugin Framework for Neovim (Loads in Vim8 only)
| [roxma/vim-hug-neovim-rpc] | Vim8 compatibility layer for neovim rpc client

### Lazy-Loaded Plugins

#### Language

| Name           | Description
| -------------- | ----------------------
| [othree/html5.vim] | HTML5 omnicomplete and syntax
| [mustache/vim-mustache-handlebars] | Mustache and handlebars syntax
| [pearofducks/ansible-vim] | Improved YAML support for Ansible
| [groenewege/vim-less] | Syntax for LESS
| [hail2u/vim-css3-syntax] | CSS3 syntax support to vim's built-in `syntax/css.vim`
| [othree/csscomplete.vim] | Updated built-in CSS complete with latest standards
| [cakebaker/scss-syntax.vim] | Syntax file for scss (Sassy CSS)
| [ap/vim-css-color] | Preview colors in source-code while editing
| [plasticboy/vim-markdown] | Markdown syntax highlighting
| [rhysd/vim-gfm-syntax] | GitHub Flavored Markdown syntax highlight extension
| [pangloss/vim-javascript] | Enhanced Javascript syntax
| [othree/jspc.vim] | JavaScript Parameter Complete
| [posva/vim-vue] | Syntax Highlight for Vue.js components
| [heavenshell/vim-jsdoc] | Generate JSDoc to your JavaScript code
| [jparise/vim-graphql] | GraphQL file detection, syntax highlighting, and indentation
| [moll/vim-node] | Superb development with Node.js
| [elzr/vim-json] | Better JSON support
| [MaxMEllon/vim-jsx-pretty] | React JSX syntax pretty highlighting
| [fatih/vim-go] | Go development
| [vim-python/python-syntax] | Enhanced version of the original Python syntax
| [Vimjas/vim-python-pep8-indent] | A nicer Python indentation style
| [vim-scripts/python_match.vim] | Extend the % motion for Python files
| [tmhedberg/SimpylFold] | No-BS Python code folding
| [raimon49/requirements.txt.vim] | Python requirements file format
| [StanAngeloff/php.vim] | Up-to-date PHP syntax file (5.3 – 7.1 support)
| [shawncplus/phpcomplete.vim] | PHP completion
| [vim-ruby/vim-ruby] | Ruby configuration files
| [tbastos/vim-lua] | Improved Lua 5.3 syntax and indentation support
| [keith/swift.vim] | Swift support
| [vim-jp/syntax-vim-ex] | Improved Vim syntax highlighting
| [chrisbra/csv.vim] | Handling column separated data
| [tpope/vim-git] | Git runtime files
| [ekalinin/Dockerfile.vim] | Syntax and snippets for Dockerfile
| [tmux-plugins/vim-tmux] | Plugin for tmux.conf
| [MTDL9/vim-log-highlighting] | Syntax highlighting for generic log files
| [hashivim/vim-terraform] | Base Terraform integration
| [cespare/vim-toml] | Syntax for TOML
| [mboughaba/i3config.vim] | i3 window manager config syntax
| [dag/vim-fish] | Fish shell edit support
| [jstrater/mpvim] | Macports portfile configuration files
| [robbles/logstash.vim] | Highlights logstash configuration files
| [lifepillar/pgsql.vim] | PostgreSQL syntax and indent
| [chr4/nginx.vim] | Improved nginx syntax and indent
| [IN3D/vim-raml] | Syntax and language settings for RAML

#### Commands

| Name           | Description
| -------------- | ----------------------
| [Shougo/defx.nvim] | Dark powered file explorer implementation
| [kristijanhusak/defx-git] | Git status implementation for Defx
| [kristijanhusak/defx-icons] | Filetype icons for Defx
| [liuchengxu/vim-which-key] | Shows key-bindings in pop-up
| [t9md/vim-choosewin] | Choose window to use, like tmux's 'display-pane'
| [kana/vim-niceblock] | Make blockwise Visual mode more useful
| [guns/xterm-color-table.vim] | Display 256 xterm colors with their RGB equivalents
| [mbbill/undotree] | Ultimate undo history visualizer
| [metakirby5/codi.vim] | The interactive scratchpad for hackers
| [reedes/vim-wordy] | Uncover usage problems in your writing
| [brooth/far.vim] | Fast find and replace plugin
| [jreybert/vimagit] | Ease your git work-flow within Vim
| [tweekmonster/helpful.vim] | Display vim version numbers in docs
| [lambdalisue/gina.vim] | Asynchronously control git repositories
| [cocopon/colorswatch.vim] | Generate a beautiful color swatch for the current buffer
| [kana/vim-altr] | Switch to the alternate file without interaction
| [lambdalisue/suda.vim] | An alternative sudo.vim for Vim and Neovim
| [tyru/open-browser.vim] | Open URI with your favorite browser
| [tyru/open-browser-unicode.vim] | Open info page about character on current cursor
| [tyru/open-browser-github.vim] | Open GitHub URL of current file
| [tyru/caw.vim] | Robust comment plugin with operator support
| [Shougo/vinarise.vim] | Hex editor
| [mzlogin/vim-markdown-toc] | Generate table of contents for Markdown files
| [chemzqm/vim-easygit] | Git wrapper focus on simplity and usability
| [liuchengxu/vista.vim] | Viewer & Finder for LSP symbols and tags in Vim
| [Ron89/thesaurus_query.vim] | Multi-language thesaurus query and replacement

#### Interface

| Name           | Description
| -------------- | ----------------------
| [haya14busa/vim-asterisk] | Improved * motions
| [rhysd/accelerated-jk] | Up/down movement acceleration
| [haya14busa/vim-edgemotion] | Jump to the edge of block
| [t9md/vim-quickhl] | Quickly highlight words
| [rafi/vim-sidemenu] | Small side-menu useful for terminal users
| [airblade/vim-gitgutter] | Show git changes at Vim gutter and un/stages hunks
| [nathanaelkane/vim-indent-guides] | Visually display indent levels in code
| [kshenoy/vim-signature] | Display and toggle marks
| [hotwatermorning/auto-git-diff] | Display Git diff for interactive rebase
| [rhysd/committia.vim] | Pleasant editing on Git commit messages
| [benekastah/neomake] | Asynchronous linting and make framework
| [junegunn/goyo] | Distraction-free writing
| [junegunn/limelight] | Hyperfocus-writing
| [itchyny/calendar.vim] | Calendar application
| [vimwiki/vimwiki] | Personal Wiki for Vim

#### Completion

| Name           | Description
| -------------- | ----------------------
| [Shougo/deoplete.nvim] | Neovim: Dark powered asynchronous completion framework
| [Shougo/neosnippet.vim] | Snippets with integration to Deoplete
| [ludovicchabant/vim-gutentags] | Manages your tag files
| [mattn/emmet-vim] | Provides support for expanding abbreviations alá emmet
| [Shougo/echodoc.vim] | Print objects' documentation in echo area
| [ncm2/float-preview.nvim] | Pretty completion preview with neovim's floating win
| [Raimondi/delimitMate] | Auto-completion for quotes, parens, brackets
| [Shougo/neosnippet-snippets] | Standard snippets repository for neosnippet
| [Shougo/context_filetype.vim] | Context filetype library for Vim script
| [Shougo/neco-vim] | Deoplete source for Vimscript
| [Shougo/neoinclude.vim] | Include completion framework for Deoplete
| [Shougo/neco-syntax] | Syntax source for Deoplete
| [davidhalter/jedi-vim] | Python jedi autocompletion library
| [zchee/deoplete-go] | deoplete.nvim source for Go
| [zchee/deoplete-jedi] | deoplete.nvim source for Python
| [carlitux/deoplete-ternjs] | deoplete.nvim source for javascript
| [wellle/tmux-complete.vim] | Completion of words in adjacent tmux panes
| [fszymanski/deoplete-emoji] | Deoplete source for emoji codes
| [juliosueiras/vim-terraform-completion] | Autocompletion and linter for Terraform
| [ternjs/tern_for_vim] | Provides Tern-based JavaScript editing support

#### Denite

| Name           | Description
| -------------- | ----------------------
| [Shougo/denite.nvim] | Dark powered asynchronous unite all interfaces
| [raghur/fruzzy] | Freaky fast fuzzy finder
| [Shougo/neoyank.vim] | Denite plugin for yank history
| [Shougo/junkfile.vim] | Denite plugin for temporary files
| [chemzqm/unite-location] | Denite location & quickfix lists
| [chemzqm/denite-git] | gitlog, gitstatus and gitchanged sources
| [rafi/vim-denite-z] | Filter and browse Z (jump around) data file
| [rafi/vim-denite-session] | Browse and open sessions
| [rafi/vim-denite-mpc] | Denite source for browsing your MPD music library

#### Operators & Text Objects

| Name           | Description
| -------------- | ----------------------
| [kana/vim-operator-user] | Define your own custom operators
| [kana/vim-operator-replace] | Operator to replace text with register content
| [machakann/vim-sandwich] | Search, select, and edit sandwich text objects
| [haya14busa/vim-operator-flashy] | Highlight yanked area
| [kana/vim-textobj-user] | Create your own text objects
| [terryma/vim-expand-region] | Visually select increasingly larger regions of text
| [AndrewRadev/sideways.vim] | Match function arguments
| [AndrewRadev/splitjoin.vim] | Transition code between multi-line and single-line
| [AndrewRadev/linediff.vim] | Perform diffs on blocks of code
| [AndrewRadev/dsf.vim] | Delete surrounding function call
| [osyo-manga/vim-textobj-multiblock] | Handle bracket objects
| [kana/vim-textobj-function] | Text objects for functions

[Shougo/dein.vim]: https://github.com/Shougo/dein.vim
[rafi/awesome-colorschemes]: https://github.com/rafi/awesome-vim-colorschemes
[thinca/vim-localrc]: https://github.com/thinca/vim-localrc
[christoomey/tmux-navigator]: https://github.com/christoomey/vim-tmux-navigator
[romainl/vim-cool]: https://github.com/romainl/vim-cool
[tpope/vim-sleuth]: https://github.com/tpope/vim-sleuth
[sgur/vim-editorconfig]: https://github.com/sgur/vim-editorconfig
[itchyny/vim-gitbranch]: https://github.com/itchyny/vim-gitbranch
[itchyny/vim-parenmatch]: https://github.com/itchyny/vim-parenmatch
[itchyny/cursorword]: https://github.com/itchyny/vim-cursorword
[roxma/nvim-yarp]: https://github.com/roxma/nvim-yarp
[roxma/vim-hug-neovim-rpc]: https://github.com/roxma/vim-hug-neovim-rpc

[othree/html5.vim]: https://github.com/othree/html5.vim
[mustache/vim-mustache-handlebars]: https://github.com/mustache/vim-mustache-handlebars
[pearofducks/ansible-vim]: https://github.com/pearofducks/ansible-vim
[groenewege/vim-less]: https://github.com/groenewege/vim-less
[hail2u/vim-css3-syntax]: https://github.com/hail2u/vim-css3-syntax
[othree/csscomplete.vim]: https://github.com/othree/csscomplete.vim
[cakebaker/scss-syntax.vim]: https://github.com/cakebaker/scss-syntax.vim
[ap/vim-css-color]: https://github.com/ap/vim-css-color
[plasticboy/vim-markdown]: https://github.com/plasticboy/vim-markdown
[rhysd/vim-gfm-syntax]: https://github.com/rhysd/vim-gfm-syntax
[pangloss/vim-javascript]: https://github.com/pangloss/vim-javascript
[othree/jspc.vim]: https://github.com/othree/jspc.vim
[posva/vim-vue]: https://github.com/posva/vim-vue
[heavenshell/vim-jsdoc]: https://github.com/heavenshell/vim-jsdoc
[jparise/vim-graphql]: https://github.com/jparise/vim-graphql
[moll/vim-node]: https://github.com/moll/vim-node
[elzr/vim-json]: https://github.com/elzr/vim-json
[MaxMEllon/vim-jsx-pretty]: https://github.com/MaxMEllon/vim-jsx-pretty
[fatih/vim-go]: https://github.com/fatih/vim-go
[vim-python/python-syntax]: https://github.com/vim-python/python-syntax
[Vimjas/vim-python-pep8-indent]: https://github.com/Vimjas/vim-python-pep8-indent
[vim-scripts/python_match.vim]: https://github.com/vim-scripts/python_match.vim
[tmhedberg/SimpylFold]: https://github.com/tmhedberg/SimpylFold
[raimon49/requirements.txt.vim]: https://github.com/raimon49/requirements.txt.vim
[StanAngeloff/php.vim]: https://github.com/StanAngeloff/php.vim
[shawncplus/phpcomplete.vim]: https://github.com/shawncplus/phpcomplete.vim
[vim-ruby/vim-ruby]: https://github.com/vim-ruby/vim-ruby
[tbastos/vim-lua]: https://github.com/tbastos/vim-lua
[keith/swift.vim]: https://github.com/keith/swift.vim
[vim-jp/syntax-vim-ex]: https://github.com/vim-jp/syntax-vim-ex
[chrisbra/csv.vim]: https://github.com/chrisbra/csv.vim
[tpope/vim-git]: https://github.com/tpope/vim-git
[ekalinin/Dockerfile.vim]: https://github.com/ekalinin/Dockerfile.vim
[tmux-plugins/vim-tmux]: https://github.com/tmux-plugins/vim-tmux
[MTDL9/vim-log-highlighting]: https://github.com/MTDL9/vim-log-highlighting
[hashivim/vim-terraform]: https://github.com/hashivim/vim-terraform
[cespare/vim-toml]: https://github.com/cespare/vim-toml
[mboughaba/i3config.vim]: https://github.com/mboughaba/i3config.vim
[dag/vim-fish]: https://github.com/dag/vim-fish
[jstrater/mpvim]: https://github.com/jstrater/mpvim
[robbles/logstash.vim]: https://github.com/robbles/logstash.vim
[lifepillar/pgsql.vim]: https://github.com/lifepillar/pgsql.vim
[chr4/nginx.vim]: https://github.com/chr4/nginx.vim
[IN3D/vim-raml]: https://github.com/IN3D/vim-raml

[Shougo/defx.nvim]: https://github.com/Shougo/defx.nvim
[kristijanhusak/defx-git]: https://github.com/kristijanhusak/defx-git
[kristijanhusak/defx-icons]: https://github.com/kristijanhusak/defx-icons
[liuchengxu/vim-which-key]: https://github.com/liuchengxu/vim-which-key
[t9md/vim-choosewin]: https://github.com/t9md/vim-choosewin
[kana/vim-niceblock]: https://github.com/kana/vim-niceblock
[guns/xterm-color-table.vim]: https://github.com/guns/xterm-color-table.vim
[mbbill/undotree]: https://github.com/mbbill/undotree
[metakirby5/codi.vim]: https://github.com/metakirby5/codi.vim
[reedes/vim-wordy]: https://github.com/reedes/vim-wordy
[brooth/far.vim]: https://github.com/brooth/far.vim
[jreybert/vimagit]: https://github.com/jreybert/vimagit
[tweekmonster/helpful.vim]: https://github.com/tweekmonster/helpful.vim
[lambdalisue/gina.vim]: https://github.com/lambdalisue/gina.vim
[cocopon/colorswatch.vim]: https://github.com/cocopon/colorswatch.vim
[kana/vim-altr]: https://github.com/kana/vim-altr
[lambdalisue/suda.vim]: https://github.com/lambdalisue/suda.vim
[tyru/open-browser.vim]: https://github.com/tyru/open-browser.vim
[tyru/open-browser-unicode.vim]: https://github.com/tyru/open-browser-unicode.vim
[tyru/open-browser-github.vim]: https://github.com/tyru/open-browser-github.vim
[tyru/caw.vim]: https://github.com/tyru/caw.vim
[Shougo/vinarise.vim]: https://github.com/Shougo/vinarise.vim
[mzlogin/vim-markdown-toc]: https://github.com/mzlogin/vim-markdown-toc
[chemzqm/vim-easygit]: https://github.com/chemzqm/vim-easygit
[liuchengxu/vista.vim]: https://github.com/liuchengxu/vista.vim
[Ron89/thesaurus_query.vim]: https://github.com/Ron89/thesaurus_query.vim

[haya14busa/vim-asterisk]: https://github.com/haya14busa/vim-asterisk
[rhysd/accelerated-jk]: https://github.com/rhysd/accelerated-jk
[haya14busa/vim-edgemotion]: https://github.com/haya14busa/vim-edgemotion
[t9md/vim-quickhl]: https://github.com/t9md/vim-quickhl
[rafi/vim-sidemenu]: https://github.com/rafi/vim-sidemenu
[airblade/vim-gitgutter]: https://github.com/airblade/vim-gitgutter
[nathanaelkane/vim-indent-guides]: https://github.com/nathanaelkane/vim-indent-guides
[kshenoy/vim-signature]: https://github.com/kshenoy/vim-signature
[hotwatermorning/auto-git-diff]: https://github.com/hotwatermorning/auto-git-diff
[rhysd/committia.vim]: https://github.com/rhysd/committia.vim
[benekastah/neomake]: https://github.com/neomake/neomake
[junegunn/goyo]: https://github.com/junegunn/goyo.vim
[junegunn/limelight]: https://github.com/junegunn/limelight.vim
[itchyny/calendar.vim]: https://github.com/itchyny/calendar.vim
[vimwiki/vimwiki]: https://github.com/vimwiki/vimwiki

[Shougo/deoplete.nvim]: https://github.com/Shougo/deoplete.nvim
[Shougo/neosnippet.vim]: https://github.com/Shougo/neosnippet.vim
[ludovicchabant/vim-gutentags]: https://github.com/ludovicchabant/vim-gutentags
[mattn/emmet-vim]: https://github.com/mattn/emmet-vim
[Shougo/echodoc.vim]: https://github.com/Shougo/echodoc.vim
[ncm2/float-preview.nvim]: https://github.com/ncm2/float-preview.nvim
[Raimondi/delimitMate]: https://github.com/Raimondi/delimitMate
[Shougo/neosnippet-snippets]: https://github.com/Shougo/neosnippet-snippets
[Shougo/context_filetype.vim]: https://github.com/Shougo/context_filetype.vim
[Shougo/neco-vim]: https://github.com/Shougo/neco-vim
[Shougo/neoinclude.vim]: https://github.com/Shougo/neoinclude.vim
[Shougo/neco-syntax]: https://github.com/Shougo/neco-syntax
[davidhalter/jedi-vim]: https://github.com/davidhalter/jedi-vim
[zchee/deoplete-go]: https://github.com/zchee/deoplete-go
[zchee/deoplete-jedi]: https://github.com/zchee/deoplete-jedi
[carlitux/deoplete-ternjs]: https://github.com/carlitux/deoplete-ternjs
[wellle/tmux-complete.vim]: https://github.com/wellle/tmux-complete.vim
[fszymanski/deoplete-emoji]: https://github.com/fszymanski/deoplete-emoji
[juliosueiras/vim-terraform-completion]: https://github.com/juliosueiras/vim-terraform-completion
[ternjs/tern_for_vim]: https://github.com/ternjs/tern_for_vim

[Shougo/denite.nvim]: https://github.com/Shougo/denite.nvim
[raghur/fruzzy]: https://github.com/raghur/fruzzy
[Shougo/neoyank.vim]: https://github.com/Shougo/neoyank.vim
[Shougo/junkfile.vim]: https://github.com/Shougo/junkfile.vim
[chemzqm/unite-location]: https://github.com/chemzqm/unite-location
[chemzqm/denite-git]: https://github.com/chemzqm/denite-git
[rafi/vim-denite-z]: https://github.com/rafi/vim-denite-z
[rafi/vim-denite-session]: https://github.com/rafi/vim-denite-session
[rafi/vim-denite-mpc]: https://github.com/rafi/vim-denite-mpc

[kana/vim-operator-user]: https://github.com/kana/vim-operator-user
[kana/vim-operator-replace]: https://github.com/kana/vim-operator-replace
[machakann/vim-sandwich]: https://github.com/machakann/vim-sandwich
[haya14busa/vim-operator-flashy]: https://github.com/haya14busa/vim-operator-flashy
[kana/vim-textobj-user]: https://github.com/kana/vim-textobj-user
[terryma/vim-expand-region]: https://github.com/terryma/vim-expand-region
[AndrewRadev/sideways.vim]: https://github.com/AndrewRadev/sideways.vim
[AndrewRadev/splitjoin.vim]: https://github.com/AndrewRadev/splitjoin.vim
[AndrewRadev/linediff.vim]: https://github.com/AndrewRadev/linediff.vim
[AndrewRadev/dsf.vim]: https://github.com/AndrewRadev/dsf.vim
[osyo-manga/vim-textobj-multiblock]: https://github.com/osyo-manga/vim-textobj-multiblock
[kana/vim-textobj-function]: https://github.com/kana/vim-textobj-function

## Custom Key-mappings

Note that,

* Leader key is set as <kbd>Space</kbd>
* Local-leader is set as <kbd>;</kbd> and used for navigation and search mostly
  (Denite and Defx)

### General

| Key   | Mode | Action
| ----- |:----:| ------------------
| `Space` | _All_ | **Leader**
| `;` | _All_ | **Local Leader**
| Arrows | Normal | Resize splits (* Enable `g:elite_mode` in `.vault.vim`)
| `;`+`c` | Normal | Open context-menu
| `Backspace` | Normal | Match bracket (%)
| `gK` | Normal | Open Zeal or Dash on some file-types
| `Y` | Normal | Yank to the end of line (y$)
| `<Return>` | Normal | Toggle fold (za)
| `S`+`<Return>` | Normal | Focus the current fold by closing all others (zMza)
| `S`+`<Return>` | Insert | Start new line from any cursor position (<C-o>o)
| `hjkl` | Normal | Smart cursor movements (g/hjkl)
| `Ctrl`+`f` | Normal | Smart page forward (C-f/C-d)
| `Ctrl`+`b` | Normal | Smart page backwards (C-b/C-u)
| `Ctrl`+`e` | Normal | Smart scroll down (3C-e/j)
| `Ctrl`+`y` | Normal | Smart scroll up (3C-y/k)
| `Ctrl`+`q` | Normal | Remap to `Ctrl`+`w`
| `Ctrl`+`x` | Normal | Rotate window placement
| `!` | Normal | Shortcut for `:!`
| `<` | Visual | Indent to left and re-select
| `>` | Visual | Indent to right and re-select
| `Tab` | Visual | Indent to right and re-select
| `Shift`+`Tab` | Visual | Indent to left and re-select
| `gh` | Normal | Show highlight groups for word
| `gp` | Normal | Select last paste
| `Q` | Normal | Start/stop macro recording
| `gQ` | Normal | Play macro 'q'
| `<Leader>`+`j`/`k` | Normal/Visual | Move lines down/up
| `<leader>`+`cp` | Normal | Duplicate paragraph
| `<leader>`+`cn`/`cN` | Normal/Visual | Change current word in a repeatable manner
| `sg` | Visual | Replace within selected area
| `Ctrl`+`a` | Command | Navigation in command line
| `Ctrl`+`b` | Command | Move cursor backward in command line
| `Ctrl`+`f` | Command | Move cursor forward in command line
| `Ctrl`+`r` | Visual | Replace selection with step-by-step confirmation
| `<leader>`+`cw` | Normal | Remove all spaces at EOL
| `<leader>`+`<leader>` | Normal | Enter visual line-mode
| `<leader>`+`os` | Normal | Load workspace session
| `<leader>`+`se` | Normal | Save current workspace session
| `<leader>`+`d` | Normal/Visual | Duplicate line or selection
| `<leader>`+`S` | Normal/Visual | Source selection
| `<leader>`+`ml` | Normal | Append modeline

### File Operations

| Key   | Mode | Action
| ----- |:----:| ------------------
| `<leader>`+`cd` | Normal | Switch to the directory of opened buffer (:lcd %:p:h)
| `<leader>`+`w` | Normal/Visual | Write (:w)
| `<leader>`+`y` / `<leader>`+`Y` | Normal | Copy (relative / absolute) file-path to clipboard
| `Ctrl`+`s` | _All_ | Write (:w)

### Editor UI

| Key   | Mode | Action
| ----- |:----:| ------------------
| `<leader>`+`ti` | Normal | Toggle indentation lines
| `<leader>`+`ts` | Normal | Toggle spell-checker (:setlocal spell!)
| `<leader>`+`tn` | Normal | Toggle line numbers (:setlocal nonumber!)
| `<leader>`+`tl` | Normal | Toggle hidden characters (:setlocal nolist!)
| `<leader>`+`th` | Normal | Toggle highlighted search (:set hlsearch!)
| `<leader>`+`tw` | Normal | Toggle wrap (:setlocal wrap! breakindent!)
| `g0` | Normal | Go to first tab (:tabfirst)
| `g$` | Normal | Go to last tab (:tablast)
| `g5` | Normal | Go to previous tab (:tabprevious)
| `Ctrl`+`j` | Normal | Move to split below
| `Ctrl`+`k` | Normal | Move to upper split
| `Ctrl`+`h` | Normal | Move to left split
| `Ctrl`+`l` | Normal | Move to right split
| `*` | Visual | Search selection forwards
| `#` | Visual | Search selection backwards
| `]`+`c`/`q` | Normal | Next on location/quickfix list
| `]`+`c`/`q` | Normal | Previous on location/quickfix list
| `s`+`h` | Normal | Toggle colorscheme background dark/light
| `s`+`-` | Normal | Lower colorscheme contrast (Support solarized8)
| `s`+`=` | Normal | Raise colorscheme contrast (Support solarized8)

### Window Management

| Key   | Mode | Action
| ----- |:----:| ------------------
| `q` | Normal | Quit window (and Vim, if last window)
| `Ctrl`+`Tab` | Normal | Next tab
| `Ctrl`+`Shift`+`Tab` | Normal | Previous tab
| `s`+`v` | Normal | Horizontal split (:split)
| `s`+`g` | Normal | Vertical split (:vsplit)
| `s`+`t` | Normal | Open new tab (:tabnew)
| `s`+`o` | Normal | Close other windows (:only)
| `s`+`b` | Normal | Previous buffer (:b#)
| `s`+`c` | Normal | Closes current buffer (:close)
| `s`+`x` | Normal | Remove buffer, leave blank window
| `<leader>`+`sv` | Normal | Split with previous buffer
| `<leader>`+`sg` | Normal | Vertical split with previous buffer

### Plugin: Denite

| Key   | Mode | Action
| ----- |:----:| ------------------
| `;`+`r` | Normal | Resumes last Denite window
| `;`+`f` | Normal | File search
| `;`+`b` | Normal | Buffers and MRU
| `;`+`d` | Normal | Directories
| `;`+`v` | Normal/Visual | Yank history
| `;`+`l` | Normal | Location list
| `;`+`q` | Normal | Quick fix
| `;`+`n` | Normal | Dein plugin list
| `;`+`g` | Normal | Grep search
| `;`+`j` | Normal | Jump points
| `;`+`u` | Normal | Junk files
| `;`+`o` | Normal | Outline tags
| `;`+`s` | Normal | Sessions
| `;`+`t` | Normal | Tag list
| `;`+`p` | Normal | Jump to previous position
| `;`+`h` | Normal | Help
| `;`+`m` | Normal | Memo list
| `;`+`z` | Normal | Z (jump around)
| `;`+`/` | Normal | Buffer lines
| `;`+`*` | Normal | Match word under cursor with lines
| `;`+`;` | Normal | Command history
| `<leader>`+`gl` | Normal | Git log (all)
| `<leader>`+`gs` | Normal | Git status
| `<leader>`+`gc` | Normal | Git branches
| `<leader>`+`gt` | Normal | Find tags matching word under cursor
| `<leader>`+`gf` | Normal | Find file matching word under cursor
| `<leader>`+`gg` | Normal/Visual | Grep word under cursor
| **Within _Denite_ window** ||
| `jj` / `kk` | Insert | Leave Insert mode
| `q` / `Escape` | Normal | Exit denite window
| `Space` | Normal | Select entry
| `Tab` | Normal | List and choose action
| `i` | Normal | Open filter input
| `dd` | Normal | Delete entry
| `p` | Normal | Preview entry
| `st` | Normal | Open in a new tab
| `sg` | Normal | Open in a vertical split
| `sv` | Normal | Open in a split
| `r` | Normal | Redraw
| `yy` | Normal | Yank
| `'` | Normal | Quick move

### Plugin: Defx

| Key   | Mode | Action
| ----- |:----:| ------------------
| `;`+`e` | Normal | Open file explorer (toggle)
| `;`+`a` | Normal | Open file explorer and select current file
| **Within _Defx_ window** ||
| `h/j/k/l` | Normal | Movement, collapse/expand, open
| `]`+`g` | Normal | Next dirty git item
| `]`+`g` | Normal | Previous dirty git item
| `w` | Normal | Toggle window size
| `N` | Normal | Create new file or directory
| `yy` | Normal | Yank selected item to clipboard
| `st` | Normal | Open file in new tab
| `sv` | Normal | Open file in a horizontal split
| `sg` | Normal | Open file in a vertical split
| `&` | Normal | Jump to project root
| `gx` | Normal | Execute associated system application
| `gd` | Normal | Open git diff on selected file
| `gl` | Normal | Open terminal file explorer
| `gr` | Normal | Grep in selected directory
| `gf` | Normal | Find files in selected directory

### Plugin: Deoplete and Emmet

| Key   | Mode | Action
| ----- |:----:| ------------------
| `Tab` | Insert/select | Smart completion
| `Enter` | Insert | Select completion or expand snippet
| `Ctrl`+`j/k/f/b/d/u` | Insert | Movement in completion pop-up
| `Ctrl`+`<Return>` | Insert | Expand Emmet sequence
| `Ctrl`+`o` | Insert | Expand snippet
| `Ctrl`+`g` | Insert | Refresh candidates
| `Ctrl`+`l` | Insert | Complete common string
| `Ctrl`+`e` | Insert | Cancel selection and close pop-up
| `Ctrl`+`y` | Insert | Close pop-up

### Plugin: Caw (comments)

| Key   | Mode | Action
| ----- |:----:| ------------------
| `gc` | Normal/visual | Prefix
| `gcc` | Normal/visual | Toggle comments
| `<leader>`+`v` | Normal/visual | Toggle single-line comments
| `<leader>`+`V` | Normal/visual | Toggle comment block

### Plugin: Edge Motion

| Key   | Mode | Action
| ----- |:----:| ------------------
| `g`+`j` | Normal/Visual | Jump to edge downwards
| `g`+`k` | Normal/Visual | Jump to edge upwards

### Plugin: Signature

| Key   | Mode | Action
| ----- |:----:| ------------------
| `m`+`/`/`?` | Normal | Show list of buffer marks/markers
| `m`+`m` | Normal | Toggle mark on current line
| `m`+`,` | Normal | Place next mark
| `m`+`-` | Normal | Purge all marks on current line
| `m`+`n` | Normal | Jump to next mark
| `m`+`p` | Normal | Jump to previous mark
| `m`+`j` | Normal | Jump to next marker
| `m`+`k` | Normal | Jump to previous marker

### Plugin: Easygit

| Key   | Mode | Action
| ----- |:----:| ------------------
| `<leader>`+`ga` | Normal | Git add current file
| `<leader>`+`gS` | Normal | Git status
| `<leader>`+`gd` | Normal | Git diff
| `<leader>`+`gD` | Normal | Close diff
| `<leader>`+`gc` | Normal | Git commit
| `<leader>`+`gb` | Normal | Git blame
| `<leader>`+`gB` | Normal | Open in browser
| `<leader>`+`gp` | Normal | Git push

### Plugin: GitGutter

| Key   | Mode | Action
| ----- |:----:| ------------------
| `[`+`g` | Normal | Jump to next hunk
| `]`+`g` | Normal | Jump to previous hunk
| `g`+`S` | Normal | Stage hunk
| `<leader>`+`gr` | Normal | Revert hunk
| `g`+`s` | Normal | Preview hunk

### Plugin: Linediff

| Key   | Mode | Action
| ----- |:----:| ------------------
| `m`+`d`+`f` | Visual | Mark lines and open diff if 2nd region
| `m`+`d`+`a` | Visual | Mark lines for diff
| `m`+`d`+`s` | Normal | Shows the diff between all the marked areas
| `m`+`d`+`r` | Normal | Removes the signs denoting the diff regions

### Misc Plugins

| Key   | Mode | Action
| ----- |:----:| ------------------
| `v` / `V` | Visual/select | Expand/reduce selection (expand-region)
| `m`+`g` | Normal | Open Magit
| `m`+`t` | Normal/Visual | Toggle highlighted word (quickhl)
| `-` | Normal | Choose a window to edit (choosewin)
| `<leader>`+`-` | Normal | Switch editing window with selected (choosewin)
| `<leader>`+`l` | Normal | Open sidemenu
| `<leader>`+`o` | Normal | Open tag-bar (:Vista)
| `<leader>`+`G` | Normal | Toggle distraction-free writing (goyo)
| `<leader>`+`gu` | Normal | Open undo-tree
| `<leader>`+`W` | Normal | VimWiki
| `<leader>`+`K` | Normal | Thesaurus

## Credits & Contribution

Big thanks to the dark knight [Shougo].

[Shougo]: https://github.com/Shougo
[lazy-loaded]: ./config/plugins.yaml#L28
[yaml2json]: https://github.com/bronze1man/yaml2json
