# React Custom Hooks

This section is a collection of custom hooks from the react team, blackstone and the community in general. 

## Table of Contents

  1. [useWindowSize](#useWindowSize)

## useWindowSize

Returns both width and height when the size of the screen changes. 

> Use Example: 
> `const { width,height } = useWindowSize();`

```import { useState, useEffect } from 'react'
const useWindowSize = () => {
  const [windowSize, setWindowSize] = useState({
    width: 0,
    height: 0
  })
  useEffect(() => {
    function handleResize () {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight
      })
    }

    window.addEventListener('resize', handleResize)
    handleResize()
    return () => window.removeEventListener('resize', handleResize)
  }, [])
  return windowSize
}
export default useWindowSize
```
