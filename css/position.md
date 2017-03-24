# Positioning

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

# `z-index`
For a **positioned** box (that is, one with any position other than static), the z-index property specifies:

1. The stack level of the box in the current stacking context.
1. Whether the box establishes a local stacking context.

# z-index & position
[Phillip Walton - What no one told you about z-index](https://philipwalton.com/articles/what-no-one-told-you-about-z-index/)

## stacking order
1. When the z-index and position properties aren’t involved, the rules are pretty simple: basically, the stacking order is the same as the order of appearance in the HTML. (OK, it’s actually a little more complicated than that, but as long as you’re not using negative margins to overlap inline elements, you probably won’t encounter the edge cases.)

2. When you introduce the position property into the mix, any positioned elements (and their children) are displayed in front of any non-positioned elements. (To say an element is “positioned” means that it has a position value other than static, e.g., relative, absolute, etc.)

3. Finally, when z-index is involved, things get a little trickier. At first it’s natural to assume elements with higher z-index values are in front of elements with lower z-index values, and any element with a z-index is in front of any element without a z-index, but it’s not that simple. First of all, z-index only works on positioned elements. If you try to set a z-index on an element with no position specified, it will do nothing. Secondly, z-index values can create stacking contexts, and now suddenly what seemed simple just got a lot more complicated.
