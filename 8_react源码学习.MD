### react源码学习

#### 1. reactDOM.render方法：
根据官网说明，这个方法接受两个参数
```
ReactDOM.render(
  <Game />,
  document.getElementById('root')
);
```
打开源码，在ReactDOMLegacy这个文件中定义render方法，其实它有三个参数
```
export function render(
  element: React$Element<any>,
  container: Container,
  callback: ?Function,
) {
  ...
  return legacyRenderSubtreeIntoContainer(
    null,
    element,
    container,
    false,
    callback,
  );
}
```
它返回的是legacyRenderSubtreeIntoContainer这个方法，然后下面这个方法，在id为root的dom节点，增加_reactRootContainer属性，这个东西带_，表示内部属性
```
root = container._reactRootContainer = legacyCreateRootFromDOMContainer(
      container,
      forceHydrate,
    );
```

nodeType是9表示DOM树的根节点document，返回document.documentELement; 否则，返回container.firstChild，表示里面的第一个元素。如果没有data-reactroot这个属性，shouldHydrate为false，就把里面的清空。这个东西可能是为了服务端渲染，但是v18版本不在支持，改为用ReactDOM.hydrate()。源码如下
```
if (container.nodeType === DOCUMENT_NODE) {
    return container.documentElement;
  } else {
    return container.firstChild;
  }
```

#### 2. _reactRootContainer的生成
react-dom/src/ReactDOMRoot.js这个文件里， _reactRootContainer为new一个构造函数返回的对象，这个对象有属性_internalRoot，这个是createContainer方法生成的，这个方法来自另一个库：
```
import {
  createContainer,
} from 'react-reconciler/src/ReactFiberReconciler';
```

监听事件：
```
ensureListeningTo(container, 'onMouseEnter', null);
```
_reactRootContainer对象有一些属性，看不出来有什么用


