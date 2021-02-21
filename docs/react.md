# React

## `createElement`

```javascript
/**
 * @see This is a simplified source code (step by step), not an actual.
 * 
 * @param type {String | ReactConstants(16 base)}
 * @param config {Record<string, any>}
 * @param ...children
 */
function createElement(type, config, children) {
  // 1. check validation
  hasValidRef(config)
  hasValidKey(config)
  
  // 2. exclude reserved props name
  for (propName in config) {
    if (
      hasOwnProperty.call(config, propName) &&
      !RESERVED_PROPS.hasOwnProperty(propName)
    ) {
      props[propName] = config[propName];
    }
  }

  // 3. extra arguments to props.children
  const childrenLength = arguments.length - 2;
  if (childrenLength === 1) {
    props.children = children;
  } else if (childrenLength > 1) {
    props.children = childArray;
  }

  // 4. resolve default props
  if (type && type.defaultProps) {
    const defaultProps = type.defaultProps;
    for (propName in defaultProps) {
      if (props[propName] === undefined) {
        props[propName] = defaultProps[propName];
      }
    }
  }

  return ReactElement(
    type,
    key,
    ref,
    self,
    source,
    ReactCurrentOwner.current,
    props,
  )
}
```
