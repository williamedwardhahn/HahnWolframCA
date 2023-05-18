# README

<img src="https://raw.githubusercontent.com/williamedwardhahn/HahnWolframCA/main/CA1.png" style=" width: 600px;">

```wolfram
V[x_List] := Table[RotateLeft[x, i], {i, {-1, 0, 1}}]
w1 = RandomReal[{-1, 1}, {100, 3}];
w2 = RandomReal[{-1, 1}, {1, 100}];
x = Table[If[i == 50, 1, 0], {i, 100}];
X = NestList[Flatten[w2.Tanh[w1.V[#]]] &, x, 50];
ArrayPlot[X, ColorFunction -> "BrightBands"]
```


Designed and programmed by William Hahn, inspired by [Wolfram](https://www.wolframscience.com/nks/)'s 1D CA.

## Overview

This code is an implementation of a 1-dimensional cellular automaton (CA) with analog states. Cellular automata are discrete models used in computer science, mathematics, physics, complexity science, theoretical biology, and microstructure modeling. They consist of a regular grid of cells, each in one of a finite number of states. The grid can be in any finite number of dimensions.

In this particular implementation, the states of the cells are not binary or discrete, but continuous, hence the term "analog". The state of a cell at a given step is determined by the states of its neighbors in the previous step. This is achieved through a combination of rotation, matrix multiplication, and the hyperbolic tangent function.

## Code Explanation

Let's break down the code:

```wolfram
V[x_List] := Table[RotateLeft[x, i], {i, {-1, 0, 1}}]
```
This function `V` takes a list `x` as input and returns a table of three lists. Each list is a rotated version of the original list `x`. The rotations are by -1, 0, and 1 positions. This effectively gives the neighborhood of each cell in the 1D CA, considering the left and right neighbors.

```wolfram
w1 = RandomReal[{-1, 1}, {100, 3}];
w2 = RandomReal[{-1, 1}, {1, 100}];
```
Here, `w1` and `w2` are matrices of random real numbers between -1 and 1. `w1` is a 100x3 matrix and `w2` is a 1x100 matrix. These matrices will be used as weights in the transformation of the cell states.

```wolfram
x = Table[If[i == 50, 1, 0], {i, 100}];
```
This line initializes the state of the 1D CA. It creates a list `x` of 100 elements, all of which are 0 except for the 50th element, which is 1.

```wolfram
X = NestList[Flatten[w2.Tanh[w1.V[#]]] &, x, 50];
```
This line evolves the CA over time. The `NestList` function applies the given function (the second argument) to the initial state `x` (the third argument) 50 times (the fourth argument), and collects all intermediate results in a list `X`. The function being applied involves the following steps:

1. Compute the neighborhood of the current state using the `V` function.
2. Multiply the result by the `w1` weight matrix.
3. Apply the hyperbolic tangent function to the result. This introduces non-linearity and ensures that the resulting cell states remain within the range [-1, 1].
4. Multiply the result by the `w2` weight matrix.
5. Flatten the result to get a 1D list.

```wolfram
ArrayPlot[X, ColorFunction -> "BrightBands"]
```
Finally, this line visualizes the evolution of the CA over time. Each row in the plot corresponds to a state of the CA at a particular time step. The `ColorFunction -> "BrightBands"` option colors the cells according to their states, with different colors representing different state values.

## Usage

To use this code, simply copy and paste it into a Wolfram Language environment, such as Mathematica or the Wolfram Cloud. The code will generate a random 1D analog CA and display its evolution over 50 time steps.

## Customization

You can customize the code

by changing the following parameters:

- **Size of the CA**: Change the size of the CA by modifying the size of the initial state `x` and the weight matrices `w1` and `w2`. For example, to create a CA with 200 cells, you would initialize `x` with 200 elements and `w1` with a 200x3 matrix.

- **Initial state**: Change the initial state of the CA by modifying the `x` list. For example, to start with a random initial state, you could use `x = RandomReal[{-1, 1}, 100];`.

- **Number of time steps**: Change the number of time steps the CA evolves for by modifying the last argument to `NestList`. For example, to evolve the CA for 100 time steps, you would use `NestList[Flatten[w2.Tanh[w1.V[#]]] &, x, 100];`.

- **Weight matrices**: Change the range or distribution of the random weights by modifying `w1` and `w2`. For example, to use weights in the range [0, 1], you would use `w1 = RandomReal[{0, 1}, {100, 3}];` and `w2 = RandomReal[{0, 1}, {1, 100}];`.

- **Color scheme**: Change the color scheme of the plot by modifying the `ColorFunction` option in `ArrayPlot`. For example, to use a black and white color scheme, you would use `ArrayPlot[X, ColorFunction -> "GrayTones"]`.

Remember to ensure that the dimensions of `x`, `w1`, and `w2` are consistent. The length of `x` should match the number of rows in `w1` and the number of columns in `w2`. The number of columns in `w1` should match the number of rotations in the `V` function.
