---
layout: page
title: Custom State Behavior Functions
permalink: /codegen-process-guide/ux/state-behavior-functions
parent: CodeBot UX
grand_parent: CodeBot Guide
nav_order: 2
---

# Custom State Behavior Functions

**Disambiguation:** In previous lessons we've been talking about state-bound UI components. Unfortunate name clash, but here we're talking about custom behavior that runs when the *UI navigation* enters a particular state (i.e. a new page). The two "state" concepts are completely unrelated...

--

UML state machines have a neat feature whereby you can specify a *behavior* (i.e. an event handler, or function) that executes at one of 3 stages in a state's lifecycle:

1. entry
2. do
3. exit

![UML state behaviors modeled in Enterprise Architect](../../images/lba/state-behaviors.png "UML state behaviors modeled in Enterprise Architect")

The `entry` behavior executes when the state machine enters a new state; the `do` behavior executes during the state; and `exit` executes when the state transitions away to some other state.

For UI navigation, you can make use of this by specifying a JavaScript function for any of the behaviors. To do this, click on the `Name / Comment` cell next to the behavior, and type a new function name:

![State behavior function names](../../images/lba/state-behavior-function-names.png "State behavior function names")

The name can be anything you like, as long as it's a valid JavaScript name, and not already used in the same state/page.

Then double-click the name, and type in the code on the Code tab:

## State entry behavior

![State entry behavior](../../images/lba/state-entry-behavior.png "State entry behavior")

In the above example, you should see the message logged in the browser console each time the Register page is viewed.

Note the ES6-style "arrow function". Currently there are no arguments passed into the function, but in a future update the domain objects in the current page will be passed in.


## State 'do' behavior

![State do behavior](../../images/lba/state-do-behavior.png "State do behavior")

The 'do' function is called "on repeat" all the time the current page is being viewed in the browser. Currently the function is called every second, though this may be parameterised in a future update.

Because the function is called on a timer, be careful not to invoke any UI actions (such as displaying a modal dialog - e.g. `alert("Uh-oh");`), or to run a long-lasting command, HTTP request, etc.


## State exit behavior

![State exit behavior](../../images/lba/state-exit-behavior.png "State exit behavior")

The 'exit' function is called once whenever the browser navigates away from the relevant page - i.e. when the state is exited.

Note that there's essentially no *guarantee* that the exit code will run; e.g. the user might close the browser, and re-open it with the URL pointing to a different page in the web-app. In this case, the 'exit' code would have been avoided. So it should just be used for non-essential code such as debug logging, or updating the UI in some way.

**Note: Be sure to click Save after editing any of the code functions in EA.**


# Writing the behavior functions

When writing JavaScript (or TypeScript) code for these functions, we recommend that you first generate the project with empty "placeholder" functions such as the ones shown above. Then open up the generated project in an IDE such as VS Code, edit and debug the functions directly, and finally copy & paste them back into the model.

For the generated React TypeScript, the behaviors for a particular state/page will be in the `.tsx` file of the same name - e.g. if the page is called **Register**, look in `Register.tsx`.


--

This concludes the CodeBot process guide. Congratulations for reading this far!!

Next, you might like to explore the [CodeBot reference section](../../codebot-reference/), or our guide to the [Parallel Agile development process](../../parallel-agile-process-guide/).
