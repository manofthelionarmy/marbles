[Links?](#)
[Embbed Videos?](#)
[Dart Setup](https://www.rockyourcode.com/dart/flutter-support-for-vim-with-dartfmt-ale-and-language-server-protocol/)
[Dart lsp from dart sdk](https://github.com/dart-lang/sdk/blob/master/pkg/analysis_server/tool/lsp_spec/README.md)
# Summary
- Treesitter support for dart is really bad, and not well developed.
	- Bad indentation. Slow.
- Use vim out of the box syntax highlighting.

----
# Related Stuff
[[Dart Lists]]
[[Dart linting]]
#dart 
#flutter 

----
# Notes:
- Delegate formatting.
	- coc-nvim -> ale
	- lvim (native lsp) -> null-ls
	- both use dart format
- Install a syntax highlighter for dart.
- Treesitter is very slow.
- Use flutter tools for lvim. Make sure to have  this important snippet:
```lua
 lsp = {
    on_attach = require('lvim.lsp').common_on_attach,
    capabilities = require('lvim.lsp').default_capabilities,
  }
```
- Make sure to get telescope extension for flutter tools.
- For coc-nvim, install `coc-flutter`. 
	- For it to work faster, add this:
```json
{
  "suggest.labelMaxLength": 50,
}
```
- ^ Cosmetically, this will make the completion look better and not display to much info.
	- And I think it does improve the speed and smoothness of the completion window appearing (because I noticed a significant different).
	- It could even be less.
- Maybe even this can help too:
```
"suggest.maxCompleteItemCount"				*coc-config-suggest-maxCompleteItemCount*

	Maximum number of complete items shown in vim.

```
- ^ The default for this is 256 completion items. I don't think I need that much tbh. Maybe I can reduce it to 50, or even 10-20. Realistically, when using a library, I won't be coming through over 50 items. 
	- However, when combing through the completion items, I learn more about the api library or core libraries.
#### 12:22pm:
- Something I noticed is the item label includes info about the return type and other details. I don't need that because I have the preview and I can jump to definition or do a hover over definition to learn more about what item (i.e. function, struct, class, etc) I'm using.
#### 2:42pm:
- I followed some ways that the maintainers of coc-flutter configured their coc-setting.json for dart and flutter.
- The native lsp in neovim is way faster and beats coc-nvim. I think I'm going to use lunarvim for flutter dev now.
## Questions:

## Follow Up:
