# Code Comments

### Goal:
To produce code that can be easily understood by other developers as *quickly as possible*.

### General Rules:

1. Always think about how well your code explains itself to the next developer.

1. Eschew "magic" constants.

    **Good**:
    ```
    const value = db.query('SELECT * FROM users WHERE name = ?', [username])
    ```

    **Better**:
    ```
    const QUERIES = {
      userByName: 'SELECT * FROM users WHERE name = ?'
    }
    ...
    const value = db.query(QUERIES.userByName, [username])
    ```

    **Rationale:**
    Locating constants at the top of the file makes them more accessible, easier to modify, and more understandable.

1. Use a formal ordering of required modules to clarify a module's use of resources.

     A good pattern to follow is:

    - pragmas
    - debug module
    - node-intrinsic modules
    - third-party modules
    - local lib modules

     <br/>where each section is delimited by a blank line.

     For example:
     ```
     'use strict'   // pragma

     /** @module */   // pragma

     const debug = require('debug')('tag, tag:tag, tag:tag:tag')

     const fs = require('fs')
     const emitter = require('event')

     const _ = require('lodash')

     const errorHandler = require('./lib/errorHandler')

     // REST OF CODE
     ```

      Note: While the pragmas are not required, it's a best practice to explicitly state all requirements or 'state-changing' values affecting the module.

1. Always use `debug` with well thought-out, hierarchically organized tags.

     Since `debug` uses minimal resources when not activated by the `DEBUG` environment variable, do not be afraid to use it anywhere there might be a question of what occurs in the code.

1. Gather global constants at the top of the module, directly after requirements.
    ```
    const _ = require('lodash')

    const TRUE = !false
    const MULTIPLIER = 10
    const QUERIES = {
      userByName: 'SELECT * FROM users WHERE name = ?'
    }
    ```

1. Always use `{}` to clarify the code's intent.

    **Good:**
    ```
    if(cond) return val
    ```

    **Better:**

    ```
    if (cond) {
      return val
    }
    ```

---
### Best Practices

- **Good:**
    ```
    val = getResult()
    if(!val) return false
    return true
    ```

- **Better:**
    ```
        return getResult()
    ```
- **Rationale:**

  There are four falsey values in JS: *false*, *0*, *null*, and *undefined*. Everything else is truthy.

  In the general case, where a function is supposed to return any non-falsey value, return the result of the function call.

  If you require the return value to be a Boolean, use `return !!getResult()` which will coerce the result to a Boolean value.

  If the function call result is expected to be a Boolean but the actual value is a number, check its type explicitly, as in: `return getResult() >= 0`

---

- **Good**:
- **Better**:
- **Rationale**:

---

### Bones Of Contention:

There are as many opinions about code formatting as there are stars in the sky.

Of specific note are:

- line delineation, indentation, & spacing
- use of spaces
- location of braces in control statements

I favor:

- line delineation: no semi-colons
- line indentation: 2 spaces (never tabs)
- line spacing: code sections separated a single blank line
- location of spaces: after keywords, and before and after brackets and curly-braces, i.e. contents of explicit arrays and objects.

  ex:
  ```
  if (cond) {         // between 'if' and cond
    res = [ 1, 2, 3 ] // before and after brackets
  } else {
    res = { k: v }    // and curly-braces
  }
  ```
- location of braces: so-called *'true brace style'*
  where:
  1. opening braces occur on same line as conditional statement
  1. further conditional clauses (else, else if, etc.) on the same line as last closing brace.
  1. closing braces on their own line

  ex:
  ```
  if (cond) { // same line as conditional statement
    ...
  } else if (cond) {
    ...
  } else {
    ...
  }
  ```
  and
  ```
  try {
    val = somethingThatCanFail()
  } catch (e) {
    ...
  }
  ```

---
