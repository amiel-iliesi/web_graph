# Progress Outline

## Goal

Since this repository might be a learning tool later on, I might as well
document my learning/drafting progress as well. This outline will note my
ideas, and inevitable roadblocks/solutions I come across along the way--like a
living dev diary.

## Outline

* HTML
1. Create a `<canvas>` that has supplied functionality via JS.
2. Create a skeleton that has various buttons, dropdowns, etc.:
    - radio: {add, remove, edit}
    - radio: {node, edge}
    - **if on edit mode, and element is selected:**
        * node: {checkbox: {start, end}}
        * edge: {weight_A-B: {None, Inf, float}, weight_B-A: {None, Inf, float}}
        * how these values are entered might be from a floating dialog that pops
        up when element is selected, or something?
    - dropdown: {DFS, BFS, A*, Convex Hull, etc.}
    - button: {start, reset, next, previous, play(animate)}
    - slider: animation speed
3. As JS development proceeds, tie the skeleton to the functionality

* CSS
1. Make it look pretty as you go, but mostly at the end. Not too complicated.

* JS
1. Use the skeleton step in the HTML outline to have a modal canvas.
2. Implement node/edge: add, draw, update, remove.
3. Implement/allow dragging of nodes in edit mode, allow dragging of edge ends
to snap to new nodes in edit mode--as well.
4. The canvas' 'start' button initiates the Python backend interop. Package and
send node/edge details via JSON to Python.
5. Wait for Python to send back graph details: ordered array of searched
nodes/edges, separate array of final found path IF a path is determined.
6. When backend algorithm is concluded and received, draw animated nodes/edges
over top of initial canvas. While animation is being played, canvas editing is
disallowed and vice versa; mutually exclusive states.

* Python
1. Create at least two files: 1 for handling JS interop, and another for the
actual algorithms; keep the jobs seperate for readability/pedagogy.
2. interop cycle: recieve nodes/edges JSON array, recieve task (DFS, A*, etc),
parse JSON into Python primitives and send to python algo file, conduct algo
and save steps as we go, when done--send state back to JS in JSON arrays.

## Points of Danger
* There should only be one start node possible. Multiple end nodes are fine,
but multiple start nodes doesn't make much semantic sense.
* An edge with two 'None' weights is semantically unconnected, might need to
remove edge if that value pair is supplied.
* Since directionality is expected in edges, the edges should be displayed with
arrows to denote if that direction is connected.
* 'start node' makes little sense for non-search algorithms like convex hull.
Maybe have the algo type be a seperate dropdown that affects the canvas mode,
and--for example--would disallow start/end nodes in a geometric algorithm like
Convex Hull.
    - A full determination of types of algorithms might be needed before we
    begin on canvas modals, as they might add new complications along the line.
