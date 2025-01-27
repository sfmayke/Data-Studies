_tags:_ #python/tuples
### Concatenate Tuples

> In order to achieve that you will nee to add a comma in the end of the tuple to be concatenated

```python
data = ((0, 1, 2), (3, 4, 5), (6, 7, 8), (9, 10, 11))
data_transpose = ()

for data_el in zip(*data):
    data_transpose += (data_el,)
    
data_transpose
```