# Assignment-Refactoring-var-to-const-and-let
To practice refactoring JavaScript code by replacing var declarations with const or let, enhancing the code's readability and reliability.

function checkAccess(loggedIn) {
    var accessLevel;   
    --> replace var with let   
    --> due to: accessLevel is reassigned based on login state and role, so it must remain mutable.

    var userRole;   
    --> replace var with let   
    --> due to: userRole may be reassigned in future logic; let is appropriate for variables whose value can change.

    if (loggedIn) {
        var message = "User is logged in.";   
        --> replace var with const   
        --> due to: message never changes within this block; const communicates immutability and keeps it block‑scoped.

        console.log(message);

        if (userRole === "admin") {
            accessLevel = "full";
        } else {
            accessLevel = "limited";
        }
    } else {
        var message = "User not logged in.";   
        --> replace var with const   
        --> due to: this message is also fixed and never reassigned; const ensures clarity and proper block scoping.

        console.log(message);
        accessLevel = "none";
    }

    return accessLevel;
}

for (var i = 0; i < 3; i++) {   
    --> replace var with let   
    --> due to: i changes each loop iteration; let prevents scope leakage and supports controlled reassignment.

    console.log("Attempt", i);

    var loggedIn = Math.random() >= 0.5;   
    --> replace var with const   
    --> due to: loggedIn is assigned once per iteration and never reassigned; const clearly expresses that intent.

    checkAccess(loggedIn);
    console.log("Access Level:", checkAccess(loggedIn));
}

## Potential Issues Caused by `var` in the Original Code

Using `var` in the original version introduces several risks:

### 1. Lack of block scoping
Variables declared with `var` do not respect block boundaries.  
This means values declared inside `if`, `else`, or `for` blocks can leak outside their intended scope, increasing the chance of accidental overwrites or unexpected behavior.

### 2. Silent redeclaration
`var` allows the same variable to be declared multiple times without throwing an error.  
This can unintentionally overwrite values and make debugging more difficult.

### 3. Hoisting behavior
Variables declared with `var` are hoisted to the top of their function scope and initialized as `undefined`.  
This can lead to confusing situations where a variable is used before it appears in the code, producing unexpected results.

### 4. Loop variable leakage
When `var` is used in loops, the loop counter remains accessible outside the loop after it finishes.  
This can interfere with other logic if the same variable name is reused elsewhere.

### 5. Incorrect access logic due to `userRole`
In the original code, `userRole` was declared with `var` but never assigned a value.  
Because of this, the check for `"admin"` always evaluated to false, resulting in incorrect access levels for logged‑in users.

