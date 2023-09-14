# Concepts you should now about

## First of all, how does component testing in Storybook work?

Easy, there are 3 simple stages: 

1. You start by writing a [**story**](https://storybook.js.org/docs/react/writing-stories/introduction) to set up the component's initial state. 
2. Then simulate user behavior using the **play** function. 

> The `play` function is a small snippet of code that runs after a story finishes rendering. You can use this to test user workflows.

  3. Finally, use the **test-runner** to confirm that the component renders correctly and that your     interaction tests with the **play** function pass. 

> Additionally, you can automate test execution via the [command line](https://storybook.js.org/docs/react/writing-tests/test-runner#cli-options) or in your [CI environment](https://storybook.js.org/docs/react/writing-tests/test-runner#set-up-ci-to-run-tests).


