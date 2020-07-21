# notes-careertrack-27.md

## setState
* setState() is the only way to set the set once it's been initialized. 
* Reconciliation process is the way React updates the DOM. The component changes based on the state changing. 
* you can pass functions to setState. Ex this.setState({ this.state.count + 1})
* Can use Object.assign() to copy data from a source. 
* Can access previous state with prevState. 
## Reconciliation
* React works on two assumptions: 
1. Two elements of different types will produce different trees, 
2. The developer can hint at which child elements may be stable across different renders with a key prop. 
* tearing down tree will use componentWillUnmount(), new DOM/tree will require componentWillMount().
* uses key to match children in the original tree with children in next tree
## Typechecking
* TypeScript is a form of typechecking.
* PropTypes checks to make sure the prop is receiving valid values. (shows up in console.)
*   Examples include: PropTypes.array, PropTypes.bool, PropTypes.func, PropTypes.number, PropTypes.object, PropTypes.string, PropTypes.symbol.
* You can give specific prop values to make sure that your props are accurate. (Default props, single child props)
## Snapshot testing
* used this before. It makes a snapshot of your tests, proving they passed so long after you leave there is proof that you're tests were passing. 
```
import React from 'react';
import Link from '../Link.react';
import renderer from 'react-test-renderer';

it('renders correctly', () => {
  const tree = renderer
    .create(<Link page="http://www.facebook.com">Facebook</Link>)
    .toJSON();
  expect(tree).toMatchSnapshot();
});

it('will check the matchers and pass', () => {
  const user = {
    createdAt: new Date(),
    id: Math.floor(Math.random() * 20),
    name: 'LeBron James',
  };

  expect(user).toMatchSnapshot({
    createdAt: expect.any(Date),
    id: expect.any(Number),
  });
});

// Snapshot
exports[`will check the matchers and pass 1`] = `
Object {
  "createdAt": Any<Date>,
  "id": Any<Number>,
  "name": "LeBron James",
}
`;

``` 
--From https://jestjs.io/docs/en/snapshot-testing

## Enzyme
* Enzyme uses Jest to produce snapshots. 
* Static (HTML)
```
describe('<Foo />', () => {
  it('renders three `.foo-bar`s', () => {
    const wrapper = render(<Foo />);
    expect(wrapper.find('.foo-bar')).to.have.lengthOf(3);
  });
``` 
https://enzymejs.github.io/enzyme/docs/api/render.html

* Shallow - tests as a unit
```  
it('simulates click events', () => {
    const onButtonClick = sinon.spy();
    const wrapper = shallow(<Foo onButtonClick={onButtonClick} />);
    wrapper.find('button').simulate('click');
    expect(onButtonClick).to.have.property('callCount', 1);
  });
``` 
https://enzymejs.github.io/enzyme/docs/api/shallow.html

* Full render API - Full DOM rendering is ideal for use cases where you have components that may interact with DOM APIs or need to test components that are wrapped in higher order components. Actually mounts components in the DOM 
```
  it('simulates click events', () => {
    const onButtonClick = sinon.spy();
    const wrapper = mount((
      <Foo onButtonClick={onButtonClick} />
    ));
    wrapper.find('button').simulate('click');
    expect(onButtonClick).to.have.property('callCount', 1);
  });
```
https://enzymejs.github.io/enzyme/docs/api/mount.html<br>
<b>Since it mounts, you may need to unmount as well.</b>



