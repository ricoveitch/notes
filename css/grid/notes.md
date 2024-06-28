# CSS Grid

## fr

(fractal units)

Same as flex grow. If you have 2fr = flex-grow: 2

## grid-template

`grid-template-columns`: specify a width for each column (how many columns you want)
`grid-template-rows`: specify a height for each row (how many rows you want). You probably don't need to define this, grid will create implicit rows.

## grid-auto-rows

Use if you don't know how many rows you are going to have. Determines the size of all rows.

If you use `grid-template-rows: 200px` in conjunction with `grid-auto-rows: 150px`, the first row will be 200 followed by 150.

## grid-column and grid-row

defines `<start-line>/<end-line>`

short hand for `grid-column-start`/`grid-column-end`.

start-line and end-line values:

- `<line>` – can be a number to refer to a numbered grid line, or a name to refer to a named grid line
- `span <number>` – the item will span across the provided number of grid tracks
- `span <name>` – the item will span across until it hits the next line with the provided name
- `auto` – indicates auto-placement, an automatic span, or a default span of one

if you do line/line, line-end - line-start will give you the number of cells your taking.

Only use line numbers when you need. Better to span or defaults when you can. Line numbers are powerful can re-arrange the order of the elements in comparison to the DOM. You saying it must start (optionally and end) here.

## grid-template-areas

For more complex grids. It defines areas of your grid and gives them a label.

Its good to use this with media queries.

e.g.

```
grid-template-areas:
    'one one two five'
    'three four four five';
```

This will give the layout in the example. For each element you just need to define which area it needs to use via `grid-area: three`.

No need to spans or setting `grid-column` and `grid-row`.

## gap

gives gap between rows and columns, doesn't display on outside of grid.

## media queries

Easy to define mobile first end overwrite with `min-width` for other devices. You can just set a display of grid and nothing else and will just get a single column with multi rows. Then alter it for a larger device.
