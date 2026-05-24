# Pre-Reading: Lesson 2.14: Introduction to Cross-Platform Mobile Application Development

Timebox **2–3 hours** across these resources before the lesson. You do not need to memorise everything; focus on building a mental model so the hands-on lab clicks faster.

---

## 1. What is React Native and How Does It Work?

**Read (15 min)**

- [React Native: Introduction](https://reactnative.dev/docs/getting-started): The official overview. Read "Core Components and Native Components" to understand how React Native components map to real native UI elements.

**Watch (8 min)**

- [React Native in 100 Seconds](https://www.youtube.com/watch?v=gvkqT_Uoahw): Fireship. A fast overview of what React Native is, how it differs from a web app, and where Expo fits in.

**Key idea to take away:** React Native uses the same component model as React for the web, but instead of rendering to the browser DOM, it renders to native iOS and Android UI elements. Your JavaScript logic stays the same; only the UI primitives change.

---

## 2. Expo and the Development Workflow

**Read (10 min)**

- [Expo: Introduction](https://docs.expo.dev/get-started/introduction/): Read the "What is Expo?" section and skim "Create your first app" so the setup commands in the lab are familiar.

**Key idea to take away:** Expo is a managed framework that handles native toolchain configuration for you. The Expo Go app lets you preview your project on a real device instantly by scanning a QR code, without building or installing a native binary.

---

## 3. Core Components: View, Text, and StyleSheet

**Read (15 min)**

- [React Native: Core Components and APIs](https://reactnative.dev/docs/components-and-apis): Read the entries for `View`, `Text`, and `StyleSheet`. Pay attention to the rules: all text must be inside a `Text` component, and styles use JavaScript objects, not CSS strings.

**Key ideas:**

- `View` is the equivalent of a `<div>`: a generic, invisible layout container.
- `Text` is required for every piece of visible text; React Native will throw an error if you render a bare string outside of `Text`.
- `StyleSheet` properties use camelCase (`backgroundColor`, not `background-color`) and numbers without units (`fontSize: 16`, not `fontSize: "16px"`).

---

## 4. Styling and Layout in React Native

**Read (10 min)**

- [React Native: Style](https://reactnative.dev/docs/style): Skim the page for the syntax, then read the "Flexbox" entry linked at the bottom. Note that Flexbox in React Native works almost identically to CSS Flexbox, but `flexDirection` defaults to `column` instead of `row`.

**Key idea to take away:** There is no CSS in React Native. All layout is done through JavaScript style objects, and Flexbox is the primary tool for arranging elements on screen.

---

## 5. Hooks in React Native

React Native uses the same hooks as React for the web. No new APIs to learn; the patterns carry over directly.

**Read (10 min)**

- [React: useEffect](https://react.dev/reference/react/useEffect): Review the "Usage" section, specifically "Connecting to an external system" and the cleanup function examples. These patterns appear in the lab when you set up a timer.

**Quick check:** Can you read the following and predict what happens when `isRunning` changes from `true` to `false`?

```js
useEffect(() => {
  if (!isRunning) return;

  const timer = setInterval(() => {
    setSeconds((prev) => prev + 1);
  }, 1000);

  return () => clearInterval(timer);
}, [isRunning]);
```

---

## Reflection (5 min)

Before the lesson, write down answers to these three questions (a notebook or a text file is fine):

1. What is the difference between `react` and `react-native` as packages? What does each one do?
2. Why can you not use a `<div>` or a `<p>` tag in a React Native app?
3. What is one thing you are still unclear about after the pre-reading?

Bring question 3 to class.
