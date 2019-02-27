# React virtual DOM diffing algorithm

节选自https://reactjs.org/docs/reconciliation.html

React implements a heuristic O(n) algorithm based on two assumptions:

Two elements of different types will produce different trees.
The developer can hint at which child elements may be stable across different renders with a key prop.
