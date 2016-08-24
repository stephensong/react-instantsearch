---
title: NumericRefinementList
layout: api.ejs
nav_groups:
  - main
---

# NumericRefinementList

Lets the user pick between a list of refinement ranges for a particular numeric facet.

## Props
attributeName: PropTypes.string.isRequired,

Name | Type | Default |Description
:- | :- | :- | :-
`attributeName` | `string` | | Name of the attribute for faceting
`items` | `[object]` | | List of options. Items should have the shape `{label: ?none, start: ?number, end: ?number}`, where `start` represents the inclusive starting value of the range, and `end` the inclusive ending value.
`id` | `?string` | | URL state serialization key. Defaults to the value of `attributeName`.

### Theme

`root`, `items`, `item`, `itemSelected`, `itemLabel`

## Implementing your own NumericRefinementList

```
import {connectNumericRefinementList} from 'instantsearch-react';

function Item(props) {
  const value = props.selected ? null : props.item.value;
  return (
    <a
      key={item.value}
      className={props.selected ? 'selected' : 'not-selected'}
      href={props.createURL(value)}
      onClick={e => {
        e.preventDefault();
        props.refine(value);
      }}
    >
      {item.label}
    </a>
  );
}

function MyNumericRefinementList(props) {
  return (
    <div>
      {props.items.map(item =>
        <Item
          key={item.value}
          item={item}
          selected={item.value === props.selectedItem}
          refine={props.refine}
          createURL={props.createURL}
        />
      )}
    </div>
  );
}

// `connectNumericRefinementList` accepts the same `id`, `attributeName` and
// `items` props as `NumericRefinementList`.
// `items` are transformed into a simpler `{label: ?node, value: string}`
// shape before being passed to the connected component.
export default connectNumericRefinementList(MyNumericRefinementList);
```