# cmp-dictionary

Dictionary completion source for [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)  

Use the dictionaries set in `dictionary` as the source for cmp.
`:h 'dictionary'`

## setup

```lua
require("cmp").setup({
  -- other settings
  sources = {
    -- other sources
    {
      name = "dictionary",
      keyword_length = 2,
    },
  }
})
```

## Configuration

to pick any dic with `neovim/vim` you can use `set dictionary`:

```vim
set dictionary+=/usr/share/dict/words
```

In lua

```lua
vim.opt.dictionary:append("/usr/share/dict/words")
```

You can download dic from [aspell.net](https://ftp.gnu.org/gnu/aspell/dict/0index.html) or installing by package manager , xbps extract to

```bash
$ ls /usr/share/dict/
american-english  british-english  words
```

## How to create your own dictionary

The dictionary is recognized as a list delimited by `\s`. `\s` is a space, `\t`, `\n`, `\r`, `\f`.
For example, if you use the following file as a dictionary, the source to be added is `{"hello", "world", "!"}`.

```txt
hello
world !
```

## Update dictionary

On `FileType *`, check the `dictionary` and update the dictionary if it is changed.
Updating only the contents of the dictionary will not detect it.

## Use different dictionaries for each filetype

To set the dictionaries for each filetype, use setlocal in autocmd.
setlocal does not pollute the global settings since it is only valid for that buffer.

```vim
augroup MyCmpDictionary
  au!
  au FileType markdown setlocal dictionary=/path/to/dic1,/path/to/dic2
augroup END
```

If you want to enable or disable this source itself by filetype, use [cmp.setup.buffer](https://github.com/hrsh7th/nvim-cmp#sources-type-tablecmpsourceconfig).

## FAQ

#### Some candidates don't show up.

Returns only candidates where the first two letters exact match by default.
You can set `g:cmp_dictionary_exact`.

## Global options

`g:cmp_dictionary_exact` decides how many characters at the beginning are used as the exact match.
If -1, only candidates with an exact prefix match will be returns.  

The default value is 2.
![image](https://user-images.githubusercontent.com/82267684/135990926-846c6289-453a-4261-aa27-612302d6a993.png)

If set to -1.
![image](https://user-images.githubusercontent.com/82267684/135991149-32ddd711-eeba-481b-a47c-a4e63de39921.png)

`g:cmp_dictionary_silent` is a setting for whether to output debug messages.  
The default value is `true`.
