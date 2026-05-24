# Assessment / Quiz

## Overview

- **Lesson:** Introduction to Cross-Platform Mobile Application Development / 2.14
- **Format:** 30 questions (mix MCQ / True-False)
- **Time:** ~30 minutes
- **Scoring:** 1 point each (unless stated)

## Questions

### Q1

What is the primary role of the `react` package in both React web and React Native applications?

A - Rendering components to the browser DOM

B - Managing components, state, and the React Element Tree

C - Providing platform-specific UI primitives

D - Bundling and transpiling JavaScript

---

### Q2 (True/False)

React Native compiles your JavaScript component logic directly into native iOS or Android code.

A - True

B - False

---

### Q3

Which package takes the place of `react-dom` in a React Native project?

A - `expo`

B - `react-native`

C - `metro`

D - `hermes`

---

### Q4

In a React Native app, what handles communication between the JavaScript thread and the native UI thread in the older architecture?

A - The Metro bundler

B - The Hermes engine

C - The React Native bridge

D - The Shadow Tree

---

### Q5 (True/False)

Expo Go allows you to preview a React Native app on a physical device without building or installing a native binary.

A - True

B - False

---

### Q6

Which command creates a new Expo project using the blank template?

A - `npm create expo-app --template blank my-app`

B - `npx create-expo-app --template blank my-app`

C - `npx expo init --blank my-app`

D - `npm init expo my-app`

---

### Q7

What is the Metro bundler responsible for in a React Native project?

A - Rendering components to native UI elements

B - Managing the JavaScript and native thread communication

C - Watching source files and bundling JavaScript for the device

D - Running tests and validating styles

---

### Q8 (True/False)

You can use standard HTML elements such as `<div>` and `<p>` in a React Native component.

A - True

B - False

---

### Q9

Which React Native component is the closest equivalent to an HTML `<div>`?

A - `Container`

B - `Section`

C - `Box`

D - `View`

---

### Q10

What will happen if you render a bare string directly inside a `View` without wrapping it in a `Text` component?

A - The string is displayed as plain text with no formatting

B - React Native throws an error

C - The string is silently ignored

D - React Native wraps it in a `Text` component automatically

---

### Q11

Which of the following is the correct way to define styles in React Native?

A - `<View className="container">`

B - `<View style="background-color: white; flex: 1;">`

C - `<View style={styles.container}>` where `styles` is a `StyleSheet.create({})` object

D - `<View css={{ backgroundColor: 'white', flex: 1 }}>`

---

### Q12 (True/False)

In React Native, style property names use kebab-case, the same as CSS (for example, `background-color`).

A - True

B - False

---

### Q13

What does `flex: 1` do when applied to a `View`?

A - Sets the view's font size to 1 rem

B - Limits the view to a single child element

C - Makes the view fill all available space in its parent container

D - Sets the view's border width to 1 pixel

---

### Q14

Which of the following is a valid style definition in React Native?

A - `{ fontSize: '16px', backgroundColor: '#fff' }`

B - `{ font-size: 16, background-color: '#fff' }`

C - `{ fontSize: 16, backgroundColor: '#fff' }`

D - `{ fontSize: '16', background-color: '#fff' }`

---

### Q15 (True/False)

The `useEffect` hook behaves differently in React Native compared to React for the web.

A - True

B - False

---

### Q16

In the counter app built in the lab, why does the `useEffect` include `isRunning` in its dependency array?

A - To prevent the effect from running on the first render

B - So the effect re-runs and either starts or clears the interval whenever `isRunning` changes

C - To make the interval update its speed based on `isRunning`

D - Because `useEffect` always requires at least one dependency

---

### Q17

What does the cleanup function returned from `useEffect` do in the counter app?

A - Resets the `seconds` state to zero

B - Clears the interval to prevent multiple timers from running simultaneously

C - Stops the JavaScript thread

D - Unmounts the component from the screen

---

### Q18 (True/False)

In the counter app, when `isRunning` is `false`, the `useEffect` still starts a new interval before returning.

A - True

B - False

---

### Q19

Which React Native component is used in the lab to add a simple tap interaction?

A - `TouchableOpacity`

B - `Pressable`

C - `Button`

D - `Touchable`

---

### Q20

What prop does the `Button` component use to specify its label text?

A - `label`

B - `text`

C - `children`

D - `title`

---

### Q21

What is the default flex direction in React Native's Flexbox layout?

A - `row`

B - `column`

C - `row-reverse`

D - `column-reverse`

---

### Q22 (True/False)

The `app.json` file in an Expo project controls app configuration such as the name, version, and SDK version.

A - True

B - False

---

### Q23

A learner writes the following code. What is wrong?

```jsx
export default function App() {
  return (
    <View>
      Hello, world!
    </View>
  );
}
```

A - `View` cannot be used as the root element

B - The string "Hello, world!" must be wrapped in a `Text` component

C - The component is missing a `style` prop on `View`

D - There is nothing wrong with this code

---

### Q24

A learner wants to display the number of seconds elapsed. Which of the following is correct?

A - `<View>{seconds}</View>`

B - `<Text>{seconds}</Text>`

C - `<p>{seconds}</p>`

D - `<span>{seconds}</span>`

---

### Q25

Why does `npx expo start` use `npx` rather than a globally installed CLI?

A - Because Expo does not support global installation

B - To ensure the CLI version used matches the SDK version pinned in the project

C - Because `npx` runs faster than a global install

D - To automatically update the Expo SDK on each start

---

### Q26 (True/False)

For the Expo Go QR scan to work, your phone and laptop must be connected to the same Wi-Fi network.

A - True

B - False

---

### Q27

A learner's `useEffect` starts a new interval every time the component re-renders because they forgot to return a cleanup function. What symptom would they observe?

A - The counter never starts

B - The counter increments faster and faster over time

C - The app crashes immediately on load

D - The `isRunning` state stops toggling

---

### Q28

Which of the following correctly describes the relationship between Expo and React Native?

A - Expo replaces React Native and uses a different rendering engine

B - Expo is a framework built on top of React Native that simplifies configuration and tooling

C - React Native is a plugin for Expo that adds native rendering support

D - Expo and React Native are the same thing under different names

---

### Q29

A learner wants the counter to pause when they navigate away from the screen. They already have the cleanup function returning `clearInterval(timer)`. Is any additional code needed?

A - Yes; they must call `clearInterval` manually in an `onBlur` handler as well

B - No; React calls the cleanup function automatically when the component unmounts

C - Yes; they must set `isRunning` to `false` before navigating away

D - No, but only if the dependency array is empty

---

### Q30 (True/False)

The `StatusBar` component from `expo-status-bar` is required in every React Native screen; removing it will cause a runtime error.

A - True

B - False

---
