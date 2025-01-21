# React useEffect Infinite Loop Bug

This repository demonstrates a common bug in React applications involving the `useEffect` hook. The `useEffect` hook is used to perform side effects, like setting up timers or fetching data, but if it's not used correctly, it can lead to unexpected behavior such as infinite loops.

## The Bug

The bug lies in the dependency array of the `useEffect` hook in `bug.js`. The dependency array is empty (`[]`), which means the effect will run only once after the component mounts.  However, the effect sets up an interval, continuously updating the state, without ever clearing the interval.  This leads to an infinite loop as the state is always changing which causes the component to re-render, triggering the effect again.

## The Solution

The solution involves adding `count` to the dependency array, so the interval is only run when the `count` changes. This is a more accurate reflection of the side-effect's need. To properly clean up the interval, the `clearInterval` function is called within the return function of the `useEffect` hook. This ensures that any active intervals are cleared when the component unmounts or when the `count` changes, preventing the infinite loop. See `bugSolution.js` for the fix.