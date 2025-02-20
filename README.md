React.js Tutorial: Understanding useState and Lifting State Up
Level: Beginner to Intermediate
Tech Stack: React.js (with Vite)




1. Introduction
In React, managing state is crucial for building dynamic user interfaces. One of the most common hooks for handling state is useState. However, as your application grows, you may run into a problem where state needs to be shared between multiple components. This is where lifting state up comes into play.

This tutorial will walk you through:
How to use the useState hook.
The problem of state duplication across components.
How lifting state up resolves these issues.




2. Setting Up the Project
To follow along, create a new React project using Vite:

npm create vite@latest react-useState-tutorial --template react
cd react-useState-tutorial
npm install
npm run dev





3. Understanding useState
Let's start with a simple counter example.
Example: Counter Component
Create a file Counter.jsx:



function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
}

export default Counter;

Then, import this component into App.jsx:

import Counter from "./Counter";

function App() {
  return (
    <div>
      <h1>useState and Lifting State Up</h1>
      <Counter />
    </div>
  );
}

export default App;


Key Takeaways:
useState initializes a piece of state (count).
setCount updates the state when the button is clicked.
The state is local to the Counter component.




4. The Problem: Sharing State Between Components
Now, let's assume we have two counter components, but we want both to stay in sync.

Modify App.jsx to include two Counter components:

function App() {
  return (
    <div>
      <h1>useState and Lifting State Up</h1>
      <Counter />
      <Counter />
    </div>
  );
}


Issue:
Each Counter component maintains its own count state, meaning they operate independently. If you click the button in one counter, it doesn’t affect the other.




5. Solution: Lifting State Up
To solve this, we move the state up to a common ancestor component (App.jsx) and pass it down as props.
Refactored Code: Lifting State Up
Modify App.jsx to manage state:

import { useState } from "react";
import Counter from "./Counter";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>useState and Lifting State Up</h1>
      <Counter count={count} setCount={setCount} />
      <Counter count={count} setCount={setCount} />
    </div>
  );
}

export default App;


Modify Counter.jsx to accept props:

function Counter({ count, setCount }) {
  return (
    <div>
      <h2>Counter: {count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
    </div>
  );
}

export default Counter;





6. How Lifting State Up Solves the Problem
The count state is now managed in App.jsx.
The Counter components receive count and setCount as props.
Clicking a button in one Counter updates the state in App.jsx, reflecting the change across both components.




7. Key Takeaways
✅ useState is great for managing local component state.
✅ When multiple components need the same state, lifting state up avoids duplication and ensures consistency.
✅ State is moved to the closest common ancestor to enable shared state across components.




8. Next Steps
Try adding more counters and see how they all sync up.
Experiment with different UI elements that use shared state.
Explore React Context as an alternative to lifting state up for global state management.





Conclusion:
Lifting state up is a fundamental React pattern that helps synchronize state across multiple components. This technique keeps your code clean, reduces redundancy, and ensures a smooth data flow in your application.
# Lifting-State-Up
