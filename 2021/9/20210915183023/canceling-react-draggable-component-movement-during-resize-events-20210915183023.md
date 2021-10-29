---
path: '/2021/9/canceling-react-draggable-component-movement-during-resize-events-20210915183023'
title: 'canceling react draggable component movement during resize events'
date: '20210915183023'
category: 'javascript'
tags: ['react', 'ui']
---

# cancelling react draggable component movement during resize events
While making a UI I utilized both [`react-draggable`](https://github.com/react-grid-layout/react-draggable)
and [`react-resizeable`](https://github.com/react-grid-layout/react-resizable/)
to handle `div` components that would render content.

I specifically wanted to avoid the [`react-grid-layout`](https://github.com/react-grid-layout/react-grid-layout)
because the snap-in functionality was cumbersome to the user experience on this
particular site.

In doing so, I noticed a few issues in movement of my components when they were
wrapped together during resize events.

Notice that there is a `cancel` modifier for the `<Draggable/>` component.

[Credit](https://stackoverflow.com/a/63807074/12387496)

Example component code:

```javascript

  <Draggable
    positionOffset={{x: this.props.posX, y: this.props.posY}}
    handle={".handle"}
    cancel={".custom-handle"}
    onStart={this.handleStart}
    onDrag={this.handleDrag}
    onStop={this.handleStop}
  >
    <ResizableBox
      style={{
        padding: "0"
      }}
      width={this.props.width}
      height={this.props.height}
      axis={"both"}
      minConstraints={this.props.minConstraints}
      maxConstraints={this.props.maxConstraints}
      resizeHandles={this.props.resizeHandles}
      handle={<CustomResizeHandle/>}
    >
      <div
      >
        {children}
      </div>
    </ResizableBox>
  </Draggable>

```

