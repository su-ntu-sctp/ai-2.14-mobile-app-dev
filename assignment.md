# Optional Assignment: Personal Profile Card App

## Overview

- **Lesson:** Introduction to Cross-Platform Mobile Application Development / 2.14
- **Type:** Optional Take-Home Assignment
- **Estimated Time:** 1–2 hours
- **Due:** Before next lesson
- **Submission:** GitHub repository link or ZIP file

## Learning Objectives Covered

This assignment reinforces:

- Creating a new Expo project and running it on a device or emulator
- Using core React Native components: `View`, `Text`, `Button`, and `StyleSheet`
- Applying `useState` to manage simple interactive state
- Styling with JavaScript objects and Flexbox layout

## Assignment Description

Build a **Personal Profile Card App** that displays a simple profile and lets the user interact with it. The focus is on getting comfortable with React Native's core components and the `StyleSheet` approach to layout before the next lesson introduces more complex UI patterns.

### What You Will Build

A single-screen app that displays:

- A profile section with a name, a short bio, and a location
- A counter showing how many times the profile has been "liked"
- A Like button that increments the counter each time it is tapped
- A Reset button that sets the counter back to zero

## Requirements

### Core Requirements

#### 1. Project Setup

- [ ] Create a new Expo project: `npx create-expo-app --template blank profile-card-app`
- [ ] Confirm the app runs on your device via Expo Go or on the Android emulator

#### 2. Profile Section

In `App.js`, build a profile section using `View` and `Text`:

- [ ] Display a name (your own or a made-up one)
- [ ] Display a one-line bio (for example, "Aspiring mobile developer")
- [ ] Display a location (for example, "Singapore")
- [ ] All text must be inside `Text` components

#### 3. Like Counter

- [ ] Add a `likes` state using `useState`, initialised to `0`
- [ ] Display the current like count: for example, "Likes: 3"
- [ ] Add a `Button` labelled "Like" that increments `likes` by 1 on each press
- [ ] Add a `Button` labelled "Reset" that sets `likes` back to `0`

#### 4. Styling

- [ ] Use `StyleSheet.create` for all styles; no inline style objects
- [ ] Centre the profile card on screen using Flexbox
- [ ] Give the profile section a visible background colour, padding, and rounded corners (`borderRadius`)
- [ ] Make the name text larger than the bio and location text

### Starter Structure

```jsx
import { useState } from 'react';
import { Button, StyleSheet, Text, View } from 'react-native';

export default function App() {
  const [likes, setLikes] = useState(0);

  return (
    <View style={styles.screen}>
      {/* Profile card goes here */}
      {/* Like counter and buttons go here */}
    </View>
  );
}

const styles = StyleSheet.create({
  screen: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    backgroundColor: '#f0f0f0',
  },
  // add more styles here
});
```

## Bonus Challenges

### Easy

- [ ] Change the Like button label to "Liked!" when `likes` is greater than zero, and back to "Like" when it is zero
- [ ] Display a short message below the counter: "Be the first to like this!" when `likes` is `0`, and "Thanks for the love!" when `likes` is greater than `0`

### Medium

- [ ] Add a second profile that can be liked independently, each with its own counter
- [ ] Add an `isLiked` boolean state. When `true`, show a filled heart character next to the counter; when `false`, show an empty heart. Tapping Like should toggle this alongside incrementing the count

### Hard

- [ ] Add a `useEffect` that logs the current like count to the console every time it changes (check the output in the Expo terminal or JS debugger)
- [ ] Add an auto-like feature: a "Start Auto-Like" button that increments the counter once per second using `setInterval`, and a "Stop" button that clears the interval. Make sure the interval is cleaned up correctly when the component unmounts

## Resources

- [Expo: Get Started](https://docs.expo.dev/get-started/introduction/)
- [React Native: Core Components](https://reactnative.dev/docs/components-and-apis)
- [React Native: Style](https://reactnative.dev/docs/style)
- [React Native: Flexbox](https://reactnative.dev/docs/flexbox)
