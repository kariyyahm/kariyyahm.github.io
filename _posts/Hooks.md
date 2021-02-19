---
title: Hooks
date: 2020-08-19 23:18:02
tags: React
---

### Hook useMemo
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
返回一个 memoized 值。   
把“创建”函数和依赖项数组作为参数传入 useMemo，它仅会在某个依赖项改变时才重新计算 memoized 值。这种优化有助于避免在每次渲染时都进行高开销的计算。

记住，传入 useMemo 的函数会在渲染期间执行。请不要在这个函数内部执行与渲染无关的操作，诸如副作用这类的操作属于 useEffect 的适用范畴，而不是 useMemo。

如果没有提供依赖项数组，useMemo 在每次渲染时都会计算新的值。

你可以把 useMemo 作为性能优化的手段，但不要把它当成语义上的保证。将来，React 可能会选择“遗忘”以前的一些 memoized 值，并在下次渲染时重新计算它们，比如为离屏组件释放内存。先编写在没有 useMemo 的情况下也可以执行的代码 —— 之后再在你的代码中添加 useMemo，以达到优化性能的目的。

>项目中部分函数组件进行大批量的计算时候，可以使用，返回字符串缓存，项目中部分使用

```
// 依赖函数优化，去除多余渲染
const startTimeStr = useMemo(() => customTime(startTime, formatStr), [startTime])
const endTimeStr = useMemo(() => customTime(endTime, formatStr), [endTime])
```

### Hook useState
```
const [startTime, setStartTime] = useState(initialStartTime)
const [endTime, setEndTime] = useState(initialEndTime)
```

### Hook useEffect
```
useEffect(() => {
    setStartTime(initialStartTime)
    setEndTime(initialEndTime)
    console.log('initialStartTime====')
}, [initialStartTime, initialEndTime])
```

### Hook useCallBack
>在开发函数式组件的时候，难免会遇到一些数据处理，这时候为了减少不必要的渲染可以使用Hook里面的useCallBack来处理

把内联回调函数及依赖项数组作为参数传入 useCallback，它将返回该回调函数的 memoized 版本，该回调函数仅在某个依赖项改变时才会更新。当你把回调函数传递给经过优化的并使用引用相等性去避免非必要渲染（例如 shouldComponentUpdate）的子组件时，它将非常有用。
```
const memoizedCallback = useCallback(
    () => {
        doSomething(a, b);
    }, [a, b]
);
```
>项目中使用
```
// 依赖函数优化，去除多余渲染
const isRightOnPress = useCallback(() => {
    if (buttonType && buttonType[1] !== 3 && rightOnPress) {
    rightOnPress()
    }
}, [buttonType, rightOnPress])
```

### Hook useLocalStore 

```
import { observer, useLocalStore } from 'mobx-react'

// 创建store
 const store = useLocalStore(() => ({
    startTime: initialStartTime,
    setStartTime(val) {
      store.startTime = val
    },
    endTime: initialEndTime,
    setEndTime(val) {
      store.startTime = val
    },
  }))
  const { startTime, endTime, setStartTime, setEndTime } = store
```
