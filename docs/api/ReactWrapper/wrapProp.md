# `.wrapProp(propName[, options]) => ReactWrapper`

Returns a new wrapper around the component provided to the original wrapper's prop `propName`.

#### Arguments

1. `propName` (`String`): Name of the prop to be wrapped
2. `options` (`Object` [optional]): Will be passed to the renderer constructor. 
   Refer to the [`mount()` options](https://airbnb.io/enzyme/docs/api/mount.html#arguments).

This essentially does:

```jsx
const Node = () => wrapper.prop('node');
const node = mount(<Node />);
```

#### Returns

`ReactWrapper`: A new wrapper that wraps the node from the provided prop.

#### Examples

##### Test Setup

```jsx
import PropTypes from 'prop-types';

const Inner = () => <div className="inner" />;

const Outer = ({ renderNode, node }) => {
  if (!renderNode) return node;
  return null;
};
Outer.propTypes = {
  renderNode: PropTypes.bool.isRequired,
  node: PropTypes.node.isRequired,
};

/*
  * Just as an example, <Outer> can render or not the provided prop.
  * Independent of what it does, we want to test the component passed in `node`.
*/
const Container = () => {
  const node = <Inner />;
  return <Outer renderNode node={node} />;
};
```

##### Testing with no arguments

```jsx
const wrapper = mount(<Container />)
  .find(Outer)
  .wrapProp('node');

expect(wrapper.find('div').equals(<div className="inner" />)).to.equal(true);
expect(wrapper.html()).to.equal('<div class="inner"></div>');
```
