|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| vim-filepaths-in-register | vim  | scripts, vim  | 20210608235211 |

# vim filepaths in register
We can get the full paths, relative paths, and filenames within
Vim. This pulls from the current buffer and will output it
to the system clipboard (!).

```vim
" relative path
:let @+ = expand("%")

" full path
:let @+ = expand("%:p")

" just filename
:let @+ = expand("%:t")
```
