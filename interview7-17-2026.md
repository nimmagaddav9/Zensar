# Lead UI Developer Interview Preparation Notes

This repository contains interview questions and answers I prepared while interviewing for a Lead UI Developer position. The focus is primarily on React, Redux Saga, asynchronous programming, and frontend architecture.

## Topics Covered

- React Architecture
- Redux Saga
- Async State Management
- Blocking vs Non-Blocking Operations
- Micro Frontends
- API Handling
- Parallel API Calls
- Race Conditions
- Timeout Handling
- Team Leadership
- Enterprise Frontend Development

---

# Interview Questions & Answers

## 1. Tell me about your recent project.

### Answer
- Worked on enterprise banking applications.
- Built client-facing and admin portals.
- Developed client enrollment workflows.
- Implemented user management and reporting features.
- Used React for frontend development.
- Used Java backend APIs.
- Worked with MobX for state management.
- Later contributed to cryptocurrency trading features.

---

## 2. Describe your team structure.

### Answer

- 14-member Agile team
- 3 Frontend Developers
- 3 Backend Developers
- 2 QA Engineers
- Product Owners
- Team Lead
- Engineering Manager

Responsibilities:

- Feature development
- Code reviews
- Production support
- Sprint planning

---

## 3. Have you used Redux Saga?

### Answer

Yes.

Used Redux Saga extensively at United Airlines for:

- API calls
- Authentication
- Async workflows
- Form submissions
- State synchronization

---

## 4. What are Micro Frontends?

### Answer

Micro Frontends split a large frontend into independently deployable applications.

### Benefits

- Independent deployments
- Team autonomy
- Better scalability
- Easier maintenance

Experience:
- Worked with Micro Frontends at Capital Group.

---

## 5. How do you make an API call using Redux Saga?

### Steps

1. Dispatch Action
2. Watcher Saga listens
3. Worker Saga executes
4. Use `call()` to invoke API
5. Use `put()` to dispatch success/failure
6. Reducer updates the store

---

## 6. Is `call()` blocking or non-blocking?

### Answer

`call()` is a **blocking** effect.

The saga waits until the Promise resolves before executing the next statement.

---

## 7. What is Blocking vs Non-Blocking?

### Blocking

Execution waits until the operation completes.

Example:

```javascript
yield call(api);
```

### Non-Blocking

Execution continues immediately.

Example:

```javascript
yield fork(workerSaga);
```

---

## 8. What is `fork()`?

### Answer

`fork()` starts a background task without blocking the current saga.

Used for:

- Background API calls
- WebSockets
- Polling
- Parallel tasks

---

## 9. Difference between `take()` and `takeEvery()`

| take() | takeEvery() |
|---------|-------------|
| Blocking | Non-blocking |
| Waits for one action | Handles every dispatched action |
| Sequential | Parallel |

---

## 10. Difference between `takeEvery()` and `takeLatest()`

### takeEvery

Processes every request.

Example:
- Notifications
- Analytics

### takeLatest

Cancels previous requests.

Example:
- Search
- Auto-complete
- Live filtering

---

## 11. How do you execute two API calls in parallel?

### Answer

Use the `race()` effect.

```javascript
yield race({
  primary: call(primaryApi),
  secondary: call(secondaryApi)
});
```

The first completed API wins.

Redux Saga automatically cancels the losing effect.

---

## 12. How do you add a timeout?

```javascript
yield race({
  response: call(api),
  timeout: delay(1000)
});
```

If the timeout wins:

- Dispatch failure action
- Show timeout message

---

## 13. What is `dataSuccess()`?

### Answer

An Action Creator.

```javascript
yield put(dataSuccess(response));
```

Reducers receive the action and update the Redux store.

---

## 14. Who cancels the losing API call?

### Answer

Redux Saga automatically cancels the losing effects inside `race()`.

For additional cleanup:

```javascript
finally {
   if (yield cancelled()) {
      abortController.abort();
   }
}
```

---

## Important Redux Saga APIs

- take
- takeEvery
- takeLatest
- call
- put
- fork
- spawn
- all
- race
- cancel
- cancelled
- delay
- select

---

# Key Takeaways

- Understand blocking vs non-blocking effects.
- Know when to use `call()`, `fork()`, `takeEvery()`, and `takeLatest()`.
- Be comfortable with `race()` and timeout handling.
- Learn saga cancellation using `cancelled()`.
- Practice writing Saga code without relying on documentation.

---

## Technologies

- React
- TypeScript
- Redux
- Redux Saga
- JavaScript (ES6+)
- REST APIs
- Micro Frontends
- MobX
- Java Backend

---

## License

This repository is intended for interview preparation and learning purposes.
