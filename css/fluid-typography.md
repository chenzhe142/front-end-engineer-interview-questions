# Advanced fluid typography
## understand how does browser renders CSS code

- you can add or subtract units with a similar type
    - `font-size: calc(10px + 2rem)`
- multiply & divide CSS units by real numbers
    - `calc(3 * 2rem)`

## responsive typography

- existing responsive typography is not ideal
    - a lot of media queries
- viewport units are different, but it has limitations
- use min font-size (with calc)
    - `calc(18px + 3vw)` => `font-size / (viewport / 100)`
- pixel by screen size quick reference

## advanced fluid typography
`font-size: calc(16px + (24-16) * (100vw - 400px) / (800 - 400))`

- cheating with sass

modular scale
modular scale: http://www.modularscale.com/
