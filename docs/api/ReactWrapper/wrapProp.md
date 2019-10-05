# `.wrapProp(propName) => ReactWrapper`

Returns a new wrapper around the component provided to the original wrapper's prop `propName`.`

NOTE: can only be called on wrapper of a single non-DOM component element node.

#### Arguments

1. `propName` (`String`):

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
class Inner extends React.Component {
  render() {
    return <div className="inner" />;
  }
}

class Outer extends React.Component {
  render() {
    if (!this.props.renderNode) return <div />;
    return this.props.node;
  }
}

class Container extends React.Component {
  render() {
    /*
     * Just as an example, <Outer> can render or not the provided prop.
     * Independent of what it does, you want to test the component given to node.
    */
    return <Outer renderNode={false} node={<Inner />} />;
  }
}
```

##### Testing with no arguments

```jsx
const wrapper = mount(<Container />)
  .find(Outer)
  .wrapProp('node');

expect(wrapper.find('div').equals(<div className="inner" />)).to.equal(true);
expect(wrapper.html()).to.equal('<div class="inner"></div>');
```
