# Material Theme Tips

## Admonition

### Types of Admonitions

The three `!` will be rendered as the admonition block:

```text
!!! note "The tile of the note"
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

!!! note "The tile of the note"
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

!!! question "Question Block"
    This is a question type

### Collapsible Blocks

To enable the [Details](https://facelessuser.github.io/pymdown-extensions/extensions/details/) extension in *mkdocs.yaml*:

```yaml
markdown_extensions:
  - admonition
  - pymdownx.details
```

Replace the `!` with `?` to render as a collapsible block:

```text
??? note "Collapsible blocks"
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```

??? note "Collapsible blocks"
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

## Keys

```text
++ctrl+alt+delete++
```

++ctrl+alt+delete++

## Mark

```text
==mark me==

==smart==mark==
```

==mark me==

==smart==mark==

## Tasklist

```text
- [X] item 1
- [ ] item 2
- [ ] item 3
```

- [X] item 1
- [ ] item 2
- [ ] item 3

## Hight Lines

```text
python hl_lines="3 4"
```

``` python hl_lines="3 5"
""" Bubble sort """
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
