# Pyramid JS

A small Node.js script that generates a pattern of `#` characters using string padding and repetition, and prints it to the console.

## Running it

```bash
node pyramid.js
```

## Output

With the current settings (`character = "#"`, `count = 8`), running the script prints:

```
###############
 ############# 
  ###########  
   #########   
    #######    
     #####     
      ###      
       #       
###############
 ############# 
  ###########  
   #########   
    #######    
     #####     
      ###      
       #       
```

This is two identical inverted triangles (widest row first, narrowing down to a single `#`) printed back to back — 16 rows total for `count = 8`. If you're expecting a classic diamond shape (narrow → wide → narrow), note that's not what this currently produces; see [Notes](#notes) below.

## How it works

- `padRow(rowNumber, rowCount)` builds one row: it pads with `rowCount - rowNumber` spaces on each side, and fills the middle with `2 * rowNumber - 1` copies of `character`. Larger `rowNumber` values produce wider rows with less padding.
- A `for` loop from `1` to `count` builds each row via `padRow` and, because `inverted` is `true`, `unshift`s each row onto the front of the `rows` array — so despite counting up, the rows end up ordered widest-to-narrowest in the array (row for `i = count` ends up first).
- A `while (rows.length < count)` loop is present to pad `rows` up to `count` entries, but since the array already has exactly `count` rows after the first loop, this loop never actually runs.
- A second `for` loop counts from `count` down to `1` and **pushes** (rather than unshifts) another full set of rows — this is what produces the second, duplicate triangle in the output.
- All rows are joined with newlines and printed via `console.log`.

## Configuration

Edit the constants at the top of `pyramid.js`:

| Constant | Description |
|---|---|
| `character` | The character used to draw the shape (default `"#"`) |
| `count` | Number of rows / size of the pattern (default `8`) |
| `inverted` | Controls build order in the first loop (see Notes) |

## Notes

- There's a `// TODO: use a different type of loop` comment above the first loop in the source — this script reads like a work-in-progress exercise (possibly a loop-practice kata) rather than a finished "draw a pyramid" utility, and the current output (two stacked inverted triangles) likely isn't the final intended shape.
- The `while` loop that pads `rows` up to `count` is currently unreachable dead code, since the preceding `for` loop already produces exactly `count` rows.
- Toggling `inverted` to `false` changes how the first set of rows is ordered (`push` instead of `unshift`), but the second `for` loop's behavior — and therefore the duplicate second triangle — is unaffected by that flag.

## License

Not specified.
