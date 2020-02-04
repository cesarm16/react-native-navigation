---
id: stack-api
title: Stack Commands
sidebar_label: Stack
---
## `push()`
Push a screen into the stack and updates the display according to the screen's options.
#### Parameters
| Name        | Required | Type   | Description                                                                                                                                                                                                      |
| ----------- | -------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| componentId | Yes      | string | The componentId of a screen pushed into the stack, or the stack's id.                                                                                                                                            |
| layout      | No       | Layout | The layout being pushed into the stack. Any type of layout (except stack) can be pushed into stacks. Typically, Component layout is pushed into stacks but it's possible to push SideMenu or BottomTabs as well. |

#### Example
<!--DOCUSAURUS_CODE_TABS-->
<!--Component-->
<br>
The most common use case - push a single react component.
```js
Navigation.push(this.props.componentId, {
  component: {
    name: 'example.PushedScreen'
  }
});
```
<!--Update options on push-->
<br>
Options are applied when screen becomes visible.

```js
Navigation.push(this.props.componentId, {
  component: {
    name: 'example.PushedScreen',
    options: {
      topBar: {
        title: {
          text: 'Pushed screen title'
        }
      }
    }
  }
});
```

<!--Push other layouts-->
<br>
Any layout type can be pushed. In this example we push a SideMenu layout.

```js
Navigation.push(this.props.componentId, {
  sideMenu: {
    left: {
      component: {
        name: 'drawerScreen'
      }
    },
    center: {
      component: {
        name: 'centerScreen'
      }
    }
  }
});
```

<!--END_DOCUSAURUS_CODE_TABS-->

## `pop()`
Pop the top screen from the stack.
#### Parameters
| Name         | Required | Type    | Description                                                           |
| ------------ | -------- | ------- | --------------------------------------------------------------------- |
| componentId  | Yes      | string  | The componentId of a screen pushed into the stack, or the stack's id. |
| mergeOptions | No       | Options | Optional options to be merged before popping the screen.              |

```js
Navigation.pop(this.props.componentId);
```

## `popToRoot()`
Pop all screens pushed into the stack.

#### Parameters
| Name         | Required | Type    | Description                                                           |
| ------------ | -------- | ------- | --------------------------------------------------------------------- |
| componentId  | Yes      | string  | The componentId of a screen pushed into the stack, or the stack's id. |
| mergeOptions | No       | Options | Optional options to be merged before popping the screen.              |
```
Navigation.popToRoot(this.props.componentId);
```

## `popTo()`
Pop the stack to a given component.

#### Parameters
| Name         | Required | Type    | Description                                              |
| ------------ | -------- | ------- | -------------------------------------------------------- |
| componentId  | Yes      | string  | The destination componentId                              |
| mergeOptions | No       | Options | Optional options to be merged before popping the screen. |

```js
Navigation.popTo(componentId);
```

## `setStackRoot()`
Reset the stack to the given layout (accepts multiple children).

#### Parameters
| Name        | Required | Type   | Description                                                                                                                                                                                                      |
| ----------- | -------- | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| componentId | Yes      | string | The componentId of a screen pushed into the stack, or the stack's id.                                                                                                                                            |
| layout      | Yes      | [Component](Component.md) or [Component](Component.md)[] | A single Component or array of components. |

#### Example
<!--DOCUSAURUS_CODE_TABS-->
<!--Single child-->
```js
Navigation.setStackRoot(this.props.componentId, {
  component: {
    name: 'example.NewRootScreen'
  }
});
```
<!--Multiple children-->
<br>
In the example below we reset the stack with two components. The first one will be the root component and the second (`PushedScreen`) will be displayed. Pressing the back button (either hardware or software) will pop it, revealing the root component - `NewRootScreen`.
```js
Navigation.setStackRoot(this.props.componentId, [
  {
    component: {
      name: 'NewRootScreen',
    }
  },
  {
    component: {
      name: 'PushedScreen',
    }
  }
]);
```
<!--END_DOCUSAURUS_CODE_TABS-->