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
from eca import OneDimensionalElementaryCellularAutomata
from networkx import Graph, draw

RULE = 3
WIDTH = 10
DEPTH = 100
MAX_IC = 30

GRAPH = Graph()


for IC in range(MAX_IC):
    cellular_automata = OneDimensionalElementaryCellularAutomata(
        initial_configuration=IC,
        lattice_width=WIDTH
    )
    for _ in range(DEPTH):
        cellular_automata.transition(RULE)
    
    GRAPH.add_edges_from(cellular_automata.graph(RULE).items())
    
draw(GRAPH)
```
![](images/rule3.png)

## More examples:
see `example.ipynb`
