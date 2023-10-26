# Assignment Submission

## Project Selected: Redux

## I. Introduction
- Briefly introduce the purpose of this section, which is to provide a detailed description of two test cases in the selected open-source project.

## II. Test Case 1: ["it works with Thunk middleware"]
### A. Description
- Provide a concise overview of what this test case is designed to verify or validate within the project.

    This test case is verifying that middleware is dispatching actions, which in Redux, is the primary
    way state is updated. This test dispatches multiple actions and then verifies the state updated as expected.

### B. Gherkin Syntax (if applicable)
- If you choose to use Gherkin syntax, write the Gherkin scenario for this test case.

    Feature: State is managed through separated components (actions -> middleware -> reducers), which allows modularity in state management.

    Scenario: Add a "Todo" object to my state
    Given: The state is empty
    When: The programmer calls the store's dispatch on an action
    Then: Proceed through middleware and reducers such that state is updated.

    Example:
    store.dispatch(addTodo('Hello') as any)
    expect(store.getState()).toEqual([
      {
        id: 1,
        text: 'Hello'
      }
    ])

### C. Test Steps
- Enumerate the sequence of steps or actions involved in the test case.
    
    1. Create a new Todo called "Hello"
    2. Verify "Hello" exists
    3. Create a new Todo called "World"
    4. Verify "Hello" still exists and "World" was added to state
    5. Asynchronously add new Todo "Hello"
    6. Await the return of the asynchronous function and verify correct state.

### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.

    This unit test tests the addTodo action, the store.dispatch function, and most importantly, the middleware
    triggering a reducer to update state.

```Java
// Enter code
```
### E. Initial State
- Describe the initial state or conditions of the system or component before executing the test.
    
    The initial state of the test was a newly instantiated store.

### F. Transition
- Explain the actions or events that trigger a change in the system's state.
    
    The store.dispatch method is used on Actions. Actions typically do not contain
    any code or functionality themselves, rather, they are just classes that contain
    the data (in this case, a string for the name of the Todo) that the middleware can use
    to determine what changes to state must be made.

### G. Expected State
- Clearly outline the expected state or outcome after the test steps have been completed.

    The store should now have three Todos, "Hello" "World" "Maybe" respectively.

## III. Test Case 2: [preserves the state when replacing a reducer]
### A. Description
- Provide a concise overview of the purpose of the second test case.

    This test tests the way state gets updated by reducers and how replacing reducers with others modifies state.

### B. Gherkin Syntax (if applicable)
- If you choose to use Gherkin syntax, write the Gherkin scenario for this test case.

    Feature: Dynamically updating reducers
    
    Scenario: Programmer wants to update reducer
    Given: We have an initial state with data already inside
    When: We replace a reducer with a new one
    Then: Update state with the new reducer, leaving original data untouched

    Example:
    store.replaceReducer(reducers.todosReverse)
    expect(store.getState()).toEqual([
      {
        id: 1,
        text: 'Hello'
      },
      {
        id: 2,
        text: 'World'
      }
    ])

    store.dispatch(addTodo('Perhaps'))
    expect(store.getState()).toEqual([
      {
        id: 3,
        text: 'Perhaps'
      },
      {
        id: 1,
        text: 'Hello'
      },
      {
        id: 2,
        text: 'World'
      }
    ])

### C. Test Steps
- Enumerate the sequence of steps or actions involved in this test case.

    1. Create empty store
    2. Create two new Todos, "Hello" and "World".
    3. Verify the Todos were created in sequential order.
    4. Replace the reducer with one the works in reverse.
    5. Add a new Todo "Perhaps".
    6. Verify the state contains the newest Todo first, followed by the other two still in sequential order.
    7. Replace the reducer again with the original reducer.
    8. Add a new Todo "Surely".
    9. Verify the state remained the same but an additional Todo was added to the end.

### D. Code Segments Under Test
- Identify specific code segments or functions that are being tested in this case.

    This test tests the store.dispatch method and more importantly the store.replaceReducer method.

```Java
// Enter code
```
### E. Initial State
- Describe the initial state or conditions of the system or component before executing the test.

    The initial state is an empty store.

### F. Transition
- Explain the actions or events that trigger a change in the system's state.

    Dispatched actions are processed through middleware, which uses whichever reducer
    we have specified to process the modifications that need to be made to state.

### G. Expected State
- Clearly outline the expected state or outcome after the test steps have been completed.

    We should have a state that contains Todos in the order:
    Perhaps -> Hello -> World -> Surely

