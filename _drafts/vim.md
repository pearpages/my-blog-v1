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

### combined complex expressions

e.g. ```d5w``` deletes 5 words.
