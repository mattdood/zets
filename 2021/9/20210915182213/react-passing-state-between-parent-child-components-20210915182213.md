---
path: '/2021/9/react-passing-state-between-parent-child-components-20210915182213'
title: 'react passing state between parent-child components'
date: '20210915182213'
category: 'javascript'
tags: ['react', 'state management', 'ui']
---

# react passing state between parent-child components
State utilization within components is an important concept for rendering interactions
on the screen.

Simple user changes that would cause re-rendering of content need to have stateful
maintanence while on the same page (between refreshes, unless pushed to local storage).

[Some reading on React state](https://reactjs.org/docs/state-and-lifecycle.html)
[Using .bind() to operate on the object](https://medium.com/webmonkeys/properly-using-bind-in-react-2e5c7e62bdb8)
[Reducing re-renders with React.memo()](https://scotch.io/tutorials/react-166-reactmemo-for-functional-components-rendering-control)
[A StackOverflow post with a similar example](https://stackoverflow.com/a/45846730/12387496)

Example code:

```javascript

class ParentClass extends Component {

    // declaring baseline state
    constructor(props) {
        super(props)
        this.state = {
            active: false,
        }
    }

    // change state
    // We could optionally pass back an `event`
    onClickToggleHandler = () => {
        let currentState = this.state.active
        this.setState({ active: !currentState })
    }

    render() {
        return (
            <ChildClass
                onClickToggleHandler={this.onClickToggleHandler}
            />
        )
    }
}

// implements the onClickToggleHandler from above
class ChildClass extends Component {

    render() {
        return (
            <>
                <button
                    onClick={this.props.onClickToggleHandler}
                >
                </button>

            </>
        )
    }
}

```

