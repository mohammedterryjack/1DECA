# 1DECA
generate one dimensional elementary cellular automata


## Install
`pip install eca`

## Example

```python
from eca import OneDimensionalElementaryCellularAutomata

configuration = OneDimensionalElementaryCellularAutomata(initial_configuration="0000100001011")

for _ in range(100):
    configuration.transition(rule_number=110)

print(str(configuration))
```

```python
from matplotlib.pyplot import imshow

imshow(configuration.evolution())
```

## Advanced example: Viewing Attractor Basins

```python
from networkx import Graph, draw_spectral

rule = 110
depth = 300
max_ic = 300
graph = Graph()
for ic in range(max_ic):
    ca = OneDimensionalElementaryCellularAutomata(initial_configuration=ic)
    for _ in range(depth):
        ca.transition(rule)
    graph.add_edges_from(ca.graph(rule).items())
draw_spectral(graph)
```

## More examples:
see `example.ipynb`
