# Storybook Testing


---

You already write stories as a natural part of UI development, testing those stories is a **low-effort way to prevent UI bugs over time**.

Storybook offers a **clean-room setting for isolating **[**component testing**](https://www.lambdatest.com/learning-hub/component-testing)**.** No matter how complex a component is, stories make it simple to explore it in all of its permutations.

When we work with component-based UI libraries like React, it helps to improve the web development process but tends to introduce complexities related to testing and debugging. React components are built to support different use cases and are interdependent, which means if you do not follow a structured process, you risk the breakdown of your application.

S**torybook allows developers to build UI components in isolation using independent building blocks. **The creation of UI components can be done using your favorite framework, which is a unique capability.

A Storybook is a specialized framework that has simplified the way we do UI development. This means d**evelopment is faster and easie**r with components being isolated. The UI components are developed without entering data into the database, starting complex development activities, or navigating around the application.

Here are some features of Storybook Testing: 

## Test Runner

Turns all of your stories into executable tests. It is powered by [Jest](https://jestjs.io/) and [Playwright](https://playwright.dev/).

- For those [without a play function](https://storybook.js.org/docs/react/writing-stories/introduction): it verifies whether the story renders without any errors.
- For those [with a play function](https://storybook.js.org/docs/react/writing-stories/play-function): it also checks for errors in the play function and that all assertions passed.

These tests run in a live browser and can be executed via the [command line](https://storybook.js.org/docs/react/writing-tests/test-runner#cli-options) or your [CI server](https://storybook.js.org/docs/react/writing-tests/test-runner#set-up-ci-to-run-tests).

Test runner offers **zero-config support for Storybook.**

You can extend the generated configuration file and provide [testEnvironmentOptions](https://github.com/playwright-community/jest-playwright#configuration) as the test runner also uses [jest-playwright](https://github.com/playwright-community/jest-playwright) under the hood.

You can also configure the test-runner to **run tests on a CI environment.**

## Visual Tests

They catch bugs in UI appearance. 

They work by taking **screenshots of every story and comparing them commit-to-commit** to identify changes.

I**deal for verifying what the user sees:** layout, color, size, and contrast.

#### Using **Chromatic** for visual tests
Each time you run Chromatic, it will generate new snapshots and compare them against the existing baselines. That’s ideal for detecting UI changes and preventing potential UI regressions.
![Screen Shot 2023-05-12 at 11.46.17.png](./attachments/Screen%20Shot%202023-05-12%20at%2011.46.17.png)
## Accessibility Tests

Accessibility is the **practice of making websites inclusive to all.** 

That means supporting requirements such as: 

- keyboard navigation
- screen reader support
- touch-friendly
- usable color contrast
- reduced motion
- and zoom support.

## Interaction Tests

As you build more complex UIs like pages, components become responsible for more than just rendering the UI. They fetch data and manage state. **Interaction tests allow you to verify these functional aspects of UIs.**

In a nutshell:

1.  You start by supplying the appropriate props for the initial state of a component. 
2. Then simulate user behavior such as clicks and form entries using the **Play Function**. 
3. Finally, check whether the UI and component state update correctly.

Important to know:

- The `play` function is a small snippet of code that **runs after a story finishes rendering. **You can use this to test user workflows.
- The test is written using Storybook-instrumented versions of [Jest](https://jestjs.io/) and [Testing Library](https://testing-library.com/).
- `@storybook/addon-interactions` visualizes the test in Storybook and **provides a playback interface for convenient browser-based debugging.**
- `@storybook/test-runner` is a standalone utility—powered by [Jest](https://jestjs.io/) and [Playwright](https://playwright.dev/)—that** executes all of your interactions tests and catches broken stories.**

## Coverage Tests

Test coverage is the practice of measuring whether existing tests fully cover your code. 

That means **surfacing areas which aren't currently being tested, such as: conditions, logic branches, functions and variables.**

Coverage tests **examine the instrumented code against a set of industry-accepted best practices. **They act as the last line of QA to improve the quality of your test suite.

![Screen Shot 2023-05-12 at 11.57.47.png](./attachments/Screen%20Shot%202023-05-12%20at%2011.57.47.png)



