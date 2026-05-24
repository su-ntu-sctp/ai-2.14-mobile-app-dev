# Lesson 2.14: Introduction to Cross-Platform Mobile Application Development

## Overview

- **Duration:** ~2 hours (hands-on lab)
- **Prerequisites:** Lessons 2.1–2.13 (full React module)

## Learning Objectives

By the end of this lesson, you will be able to:

1. **Explain** how React Native differs from React for the web, and how the two share the same component model and hooks
2. **Set up** a React Native development environment using Expo and run an app on a physical device or Android emulator
3. **Build** a basic React Native app using core components and familiar hooks

## Introduction

So far in this module you have been building web applications with React. Today you will take those same skills and apply them to mobile development with React Native. The core ideas (components, props, state, and hooks) carry over directly. What changes is the set of UI building blocks you use. By the end of this lab you will have a working Expo project running on your own device or an emulator, and a first app that uses `View`, `Text`, `StyleSheet`, and `useEffect`.

---

## Part 1: Environment Setup

### What is Expo?

Expo is a framework built on top of React Native that handles the complex parts of mobile development for you: project configuration, native build tooling, and device testing. Think of it the way Create React App or Vite scaffolds a React web project: Expo does the same for mobile.

For testing, Expo provides the **Expo Go** app, which lets you load your project on a real device by scanning a QR code, with no need to build or install a native binary.

### Step 1: Create a new Expo project

Open a terminal and run:

```bash
npx create-expo-app --template blank my-first-rn-app
```

> If prompted to install `create-expo-app`, press `y` to proceed.

The `--template blank` flag gives you a minimal project with no extra libraries pre-installed, which keeps things simple while you are learning.

Open the project in VS Code:

```bash
code my-first-rn-app
```

Take a moment to look at the generated files:

```
my-first-rn-app/
├── assets/          # App icons and splash screen images
├── node_modules/
├── App.js           # Entry point (this is where you will write your code)
├── app.json         # App configuration (name, version, Expo SDK version)
├── babel.config.js  # Transpilation config (managed by Expo, no need to edit)
├── package.json
└── package-lock.json
```

A few things to notice compared to a React web project:

- There is no `index.html`; the native shell is provided by Expo and the device OS
- There is no `react-dom` in `package.json`; `react-native` takes its place as the renderer
- `app.json` plays a similar role to `vite.config.js`: it controls how your app is built and identified

### Step 2: Start the development server

```bash
cd my-first-rn-app
npx expo start
```

This starts the **Metro bundler**, which watches your files and bundles your JavaScript for the device. You will see a QR code printed in the terminal.

> `npx expo start` runs the Expo CLI version pinned to your project, which avoids version mismatch errors that can occur with a globally installed CLI.

### Step 3: Run the app on your device

Install the **Expo Go** app on your phone:

- Android: [Expo Go on Google Play](https://play.google.com/store/apps/details?id=host.exp.exponent)
- iOS: [Expo Go on the App Store](https://apps.apple.com/app/expo-go/id982107779)

Then load your project:

- **Android:** open Expo Go and tap **Scan QR code**
- **iOS:** open the Camera app and point it at the QR code

You should see the default app screen: "Open up App.js to start working on your app!"

Make a small change (edit the text inside `App.js`) and watch the app update on your device immediately. This is **hot reload** in action.

> **Troubleshooting:** Your phone and laptop must be on the **same Wi-Fi network** for the QR scan to work. If you are on a campus or corporate network that blocks device-to-device traffic, try creating a mobile hotspot from your laptop and connecting your phone to it, then restart `npx expo start`.

---

### Step 4: Set up the Android Emulator

Testing on a real device is convenient, but an emulator lets you test across different screen sizes and Android versions without needing additional hardware. Follow the steps below; your instructor will also demonstrate this live.

**Install Android Studio**

Download and install Android Studio from [developer.android.com/studio](https://developer.android.com/studio).

During installation, make sure **Android Virtual Device (AVD)** is checked.

**Check that Android API Level 34 is installed**

Open Android Studio. Go to **More Actions → SDK Manager**. Under the **SDK Platforms** tab, confirm that **Android 14 (API Level 34)** is checked. If not, check it and click **Apply**.

**Create a virtual device**

Go to **More Actions → Virtual Device Manager** and click **Create device**. Choose a Pixel phone model that shows the Play Store icon, then select **UpsideDownCake (API 34)** as the system image. Leave the other settings as default and click **Finish**.

**Set environment variables**

The Expo CLI needs to know where your Android SDK is installed.

On **Mac/Linux**, open `~/.zshrc` (or `~/.bashrc`) and add:

```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

Then reload it:

```bash
source ~/.zshrc
```

On **Windows**, open System Properties → Environment Variables and add `ANDROID_HOME` pointing to your SDK location (usually `C:\Users\<your-name>\AppData\Local\Android\Sdk`), then add `%ANDROID_HOME%\emulator` and `%ANDROID_HOME%\platform-tools` to the `Path` variable.

You can verify the setup by running:

```bash
emulator -list-avds    # should list the device you just created
adb devices            # should list connected devices (empty is fine for now)
```

**Launch the emulator from Expo**

Start the emulator from Android Studio by clicking the play button next to your virtual device. Once it has booted, go back to your Expo terminal and press `a`. Expo will install the Expo Go client on the emulator and load your app automatically.

> If the emulator window is too large, press `Ctrl+` (or `Cmd+`) and use the arrow keys to resize it.

Full reference: [Expo: Android Studio Emulator](https://docs.expo.dev/workflow/android-studio-emulator/)

**iOS Simulator (Mac only, optional)**

If you are on a Mac and have Xcode installed, press `i` in the Expo terminal to open your app in the iOS Simulator. This is not available on Windows or Linux.

---

### Step 5: Open the JS Debugger

React Native apps include a built-in debugger accessible at any time:

- **Android emulator:** press `Ctrl+M` (or `Cmd+M` on Mac), then tap **Open JS Debugger**
- **Physical Android device:** shake the device
- **iOS Simulator:** press `Cmd+D`

The debugger opens in your browser and shows:

- The component tree and hook state (like React DevTools)
- Console logs
- Network requests

> If you do not see your changes reflected in the debugger, shake the device (or press the shortcut above) and tap **Reload**.

---

## Part 2: Your First React Native App

### Core components

In React for the web, you build UIs from HTML elements: `<div>`, `<p>`, `<button>`, and so on. React Native does not have HTML; instead it provides its own set of primitive components that map to native UI elements on each platform.

The three you will use today:

| React Native | Closest HTML equivalent | Purpose |
|---|---|---|
| `View` | `<div>` | A generic layout container |
| `Text` | `<p>`, `<span>` | Displays text |
| `Button` | `<button>` | A simple tap target |

Two important rules to remember:

1. **All text must be inside a `Text` component.** Rendering a bare string outside of `Text` will throw an error.
2. **`View` cannot contain raw text directly.** Wrap any text in `Text` first.

### Styling in React Native

React Native does not use CSS files or class names. Instead, styles are JavaScript objects passed via the `style` prop. The `StyleSheet.create()` function validates your styles at development time and gives a minor performance benefit.

```jsx
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    backgroundColor: '#fff',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});
```

Things that differ from CSS:

- Property names are **camelCase** (`backgroundColor`, not `background-color`)
- There are **no units**: numbers are density-independent pixels by default
- **Flexbox is the default layout system**: `flex: 1` makes a container fill available space

### Step 1: Build a simple counter

Open `App.js` and replace its contents with the following:

```jsx
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>My First React Native App</Text>
      <Text>Seconds elapsed: 0</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
});
```

**Device check:** you should see "My First React Native App" and "Seconds elapsed: 0" centred on screen.

Notice `StatusBar` from `expo-status-bar`: it controls the appearance of the device's top status bar (the row showing the time and battery). You can leave it as `style="auto"` for now.

### Step 2: Add a live counter with useState and useEffect

`useState` and `useEffect` work exactly the same way as in React web. Update `App.js`:

```jsx
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View } from 'react-native';
import { useState, useEffect } from 'react';

export default function App() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => clearInterval(timer);
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>My First React Native App</Text>
      <Text>Seconds elapsed: {seconds}</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
});
```

**Device check:** the counter should increment every second.

The cleanup function (`return () => clearInterval(timer)`) runs when the component unmounts, preventing the interval from continuing to fire after the component is gone. This is the same pattern you used in the web lessons.

### Step 3: Add a Start/Pause button

Now add a `Button` to toggle the counter on and off. `Button` is the simplest interactive component in React Native. You will learn to build a fully customised button with `Pressable` in a later lesson.

```jsx
import { StatusBar } from 'expo-status-bar';
import { Button, StyleSheet, Text, View } from 'react-native';
import { useState, useEffect } from 'react';

export default function App() {
  const [seconds, setSeconds] = useState(0);
  const [isRunning, setIsRunning] = useState(true);

  useEffect(() => {
    if (!isRunning) return;

    const timer = setInterval(() => {
      setSeconds((prev) => prev + 1);
    }, 1000);

    return () => clearInterval(timer);
  }, [isRunning]);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>My First React Native App</Text>
      <Text style={styles.counter}>Seconds: {seconds}</Text>
      <Button
        title={isRunning ? 'Pause' : 'Start'}
        onPress={() => setIsRunning((prev) => !prev)}
      />
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    justifyContent: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 16,
  },
  counter: {
    fontSize: 32,
    marginBottom: 24,
  },
});
```

**Device check:** tapping the button should pause and resume the counter.

A few things to note about the `useEffect` here:

- When `isRunning` is `false`, the effect returns early; there is nothing to set up or clean up
- When `isRunning` is `true`, the effect starts a new interval and returns its cleanup function
- React runs the cleanup automatically before the effect re-runs (when `isRunning` changes) and when the component unmounts, so there is never more than one interval running at a time

---

## Bonus Challenges

Work on as many as you can; they are listed in order of difficulty.

### Challenge 1: Reset button

Add a second `Button` labelled "Reset" that stops the counter and resets `seconds` back to zero.

**Hints:**
- You will need to set both `isRunning` to `false` and `seconds` to `0` in the handler
- Render the two buttons side by side using a `View` with `flexDirection: 'row'` and a `gap` between them

### Challenge 2: MM:SS display

Instead of showing a raw number of seconds, display elapsed time in `MM:SS` format (for example, `01:05`).

**Hints:**
- `Math.floor(seconds / 60)` gives you the minutes; `seconds % 60` gives you the remaining seconds
- `String.padStart(2, '0')` left-pads a number with a leading zero when it is less than 10

### Challenge 3: Lap times

Add a "Lap" button that records the current elapsed time. Display the list of recorded lap times below the counter.

**Hints:**
- Add a `laps` state as an array, initialised to `[]`
- Each time the Lap button is pressed, append the current `seconds` value to `laps`
- Render the list using `.map()`; you will not need `FlatList` for a short list, so plain `Text` components inside a `View` are fine for now

---

## Common Pitfalls

**Text outside of a `Text` component**

```jsx
// Wrong: will throw an error
<View>
  Hello
</View>

// Correct
<View>
  <Text>Hello</Text>
</View>
```

**Using CSS property names**

```jsx
// Wrong: kebab-case and string values do not work
const styles = StyleSheet.create({
  box: {
    'background-color': 'red',
    'font-size': '16px',
  },
});

// Correct: camelCase, no units
const styles = StyleSheet.create({
  box: {
    backgroundColor: 'red',
    fontSize: 16,
  },
});
```

**Making the `useEffect` callback itself `async`**

```jsx
// Wrong: useEffect expects a cleanup function or nothing, not a Promise
useEffect(async () => {
  await doSomething();
}, []);

// Correct: define the async function inside and call it
useEffect(() => {
  async function run() {
    await doSomething();
  }
  run();
}, []);
```

---

## Summary

- **React Native vs React web:** the component model and hooks are identical; only the UI primitives change (`View` and `Text` instead of `div` and `p`)
- **Expo:** a managed framework that handles project setup, native tooling, and device testing via the Expo Go app
- **Core components:** `View` for layout, `Text` for all text output, `Button` for simple tap interactions
- **Styling:** JavaScript objects with camelCase property names, no units, Flexbox by default
- **Hooks:** `useState` and `useEffect` behave exactly as they do in React web; the cleanup pattern and dependency array work the same way

---

## Additional Resources

- [Expo: Get Started](https://docs.expo.dev/get-started/introduction/)
- [React Native: Core Components](https://reactnative.dev/docs/components-and-apis)
- [React Native: Style](https://reactnative.dev/docs/style)
- [Expo: Android Studio Emulator Setup](https://docs.expo.dev/workflow/android-studio-emulator/)
