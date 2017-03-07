#Positioning

## `static`
- Let the element use the normal behavior. It is laid out in its current position in the flow.
- `top` `right` `bottom` `left` and `z-index` do not apply.

## `relative`
- It is relative to its original position. 
- Its original position's space is reserved.

![position relative demo](http://g.recordit.co/MHxEaKCvdv.gif)

## `absolute`
- If none of its parent container set `position: relative`, it is `absolute` to the initial containing block.
- If it has parent set `position: relative`, then the element is `absolute` to that element.
- Its original position's space is removed.
- It can have margins, and they do not collapse with any other margins.

## `fixed`
- Its original position's space is removed.
- **Relative to viewport**, and do not move it when scrolling.

## `sticky` (experimental feature)
