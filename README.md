# 1DECA
generate one dimensional elementary cellular automata


## Install
`pip install eca`

## Example 1: Basics

```python
from eca import OneDimensionalElementaryCellularAutomata

configuration = OneDimensionalElementaryCellularAutomata(initial_configuration="0000100001011")
configuration.transition(rule_number=110)
str(configuration)
```
> 0001100011111


## Example 2: Displaying CA evolution

```python
from eca import OneDimensionalElementaryCellularAutomata
from matplotlib.pyplot import imshow

configuration = OneDimensionalElementaryCellularAutomata(lattice_width=1000)

for _ in range(400):
    configuration.transition(rule_number=110)

imshow(configuration.evolution(),cmap='gray')
```
![](images/rule110.png)

## Example 3: Viewing Attractor Basins

```python
from eca import OneDimensionalElementaryCellularAutomata
from networkx import DiGraph, draw

RULE = 3
WIDTH = 5
DEPTH = 100
MAX_IC = 30

GRAPH = DiGraph()


for IC in range(MAX_IC):
    cellular_automata = OneDimensionalElementaryCellularAutomata(
        initial_configuration=IC,
        lattice_width=WIDTH
    )
    for _ in range(DEPTH):
        cellular_automata.transition(RULE)
    
    GRAPH.add_edges_from(cellular_automata.graph(RULE).items())
    
draw(GRAPH, with_labels=True)
```
![](images/rule3attractorbasin.png)

## Example 4: Inspecting Each Attractor basin more closely

```python
from eca import OneDimensionalElementaryCellularAutomata
from networkx import DiGraph, draw, weakly_connected_components
from matplotlib.pyplot import show, imshow
from random import choice

RULE = 3
WIDTH = 5
DEPTH = 100
MAX_IC = 30

GRAPH = DiGraph()


for IC in range(MAX_IC):
    cellular_automata = OneDimensionalElementaryCellularAutomata(
        initial_configuration=IC,
        lattice_width=WIDTH
    )
    for _ in range(DEPTH):
        cellular_automata.transition(RULE)
    
    GRAPH.add_edges_from(cellular_automata.graph(RULE).items())
    

for nodes in weakly_connected_components(GRAPH):
    draw(GRAPH.subgraph(nodes), with_labels=True)
    show()
    cellular_automata = OneDimensionalElementaryCellularAutomata(
        initial_configuration= choice(list(nodes)),
        lattice_width=WIDTH
    )
    for _ in range(DEPTH):
        cellular_automata.transition(RULE)
    imshow(cellular_automata.evolution(),cmap='gray')
    show()
```

![](images/rule3attractorbasin1.png)
![](images/rule3attractorbasin2.png)
![](images/rule3attractorbasin3.png)

## Example 5: Plotting Trajectories (e.g. to view Sensitivity to Initial Conditions)
```python

```
![](images/rule110_sensitivity_to_ic.png

## More examples:
see `example.ipynb`
