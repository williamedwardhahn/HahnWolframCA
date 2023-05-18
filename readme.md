<img style="image-rendering: pixelated" src="https://raw.githubusercontent.com/williamedwardhahn/HahnWolframCA/main/CA1.png" width = 600>


```wolfram
V[x_List] := Table[RotateLeft[x, i], {i, {-1, 0, 1}}]
w1 = RandomReal[{-1, 1}, {100, 3}];
w2 = RandomReal[{-1, 1}, {1, 100}];
x = Table[If[i == 50, 1, 0], {i, 100}];
X = {};
Do[x = Flatten[w2.Tanh[w1.V[x]]];AppendTo[X, x],{i, 50}]
ArrayPlot[X, ColorFunction -> "BrightBands"]
```


# README

## Overview

The provided code is a simulation of a 1-dimensional analog cellular automaton. Unlike traditional cellular automata, which operate on discrete values (usually binary, 0 or 1), this analog cellular automaton operates on continuous values between -1 and 1, approximating real numbers. The state of each cell in the automaton is influenced by its own state and the states of its immediate neighbors.

## Code Explanation

```wolfram
V[x_List] := Table[RotateLeft[x, i], {i, {-1, 0, 1}}]
```
This function `V` takes a list `x` as an argument and returns a table of three lists. Each list is a version of `x` that has been rotated to the left by -1, 0, or 1 places. This effectively gives us the state of each cell along with its left and right neighbors.

```wolfram
w1 = RandomReal[{-1, 1}, {100, 3}];
w2 = RandomReal[{-1, 1}, {1, 100}];
```
`w1` and `w2` are weight matrices that are initialized with random real numbers between -1 and 1. `w1` has dimensions 100x3 and `w2` has dimensions 1x100. These weights will be used to determine how much influence a cell and its neighbors have on the cell's next state.

```wolfram
x = Table[If[i == 50, 1, 0], {i, 100}];
```
This line initializes the state of the automaton. It creates a list of 100 cells, all set to 0, except for the cell at position 50, which is set to 1.

```wolfram
X = {};
```
`X` is an empty list that will be used to store the state of the automaton at each time step.

```wolfram
Do[x = Flatten[w2.Tanh[w1.V[x]]];AppendTo[X, x],{i, 50}]
```
This `Do` loop runs for 50 iterations. In each iteration, it updates the state of the automaton by applying the weights `w1` and `w2` to the current state and its neighbors, passing the result through a hyperbolic tangent function `Tanh` to keep the values between -1 and 1, and then flattening the result to a 1-dimensional list. The updated state is then appended to `X`.

```wolfram
ArrayPlot[X, ColorFunction -> "BrightBands"]
```
Finally, `ArrayPlot` is used to visualize the state of the automaton at each time step, with the `ColorFunction` "BrightBands" mapping the cell values to colors.

## Usage

The output will be a color-coded plot showing the evolution of the cellular automaton over 50 time steps. The initial condition is a single "active" cell in a field of "inactive" cells, and the plot shows how this initial condition evolves under the influence of the randomly initialized weights.
