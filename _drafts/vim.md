#vim

## entering and exiting vim

```bash
# enter
vim

# exit vim
:q
```

## moving around

h,j,k,l,w,b keys

```
j -> moves down
k -> modews up
```

```
h -> moves left
l -> moves right
```

```
w -> moves forward one word
b -> moves backwards one word
```

## modes

- Normal (esc)
- Insert (i)
- Visual (v)
- Visual-line (shift v)

## saving files

```
:w filename.txt
```

## built-in commands

- delete line ```d d```
- delete line leaving the space ```shift d```

```
# remove inside html tag
cit
# remove inside {}
ci{
# remove inside ""
ci"
```
### combined complex expressions

e.g. ```d5w``` deletes 5 words.

## copy n paste

- enter in visual mode press ```y``` to copy and ```p``` to paste. When deleting ```dd``` it's like cutting. Then you can also paste with ```p```.

## configuring vim

```
:syntax on
:syntax off
:set number
:set nonumber
:set relativenumber
:set norelativenumber
:help option-list
```

## .vimrc

```
syntax on
set number relativenumber
filetype plugin indent on
set tabstop=2 shiftwidth=2 expandtab
set backspace=indent,eol,start
```
