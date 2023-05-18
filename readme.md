
```
V[x_List] := Table[RotateLeft[x, i], {i, {-1, 0, 1}}]
w1 = RandomReal[{-1, 1}, {100, 3}];
w2 = RandomReal[{-1, 1}, {1, 100}];
x = Table[If[i == 50, 1, 0], {i, 100}];
X = {};
Do[x = Flatten[w2.Tanh[w1.V[x]]];AppendTo[X, x],{i, 50}]
ArrayPlot[X, ColorFunction -> "BrightBands"]
```
