# Chapter 3: Functions

## Small!

The first rule of functions is that they should be small. The second rule of functions is that they should be smaller than that.

Functions should hardly ever be 20 lines long.

### Blocks and Indenting

This implies that the blocks within `if` statements, `else` statements, `while` statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within the block can have a nicely descriptive name.

This also implies that functions should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two. This, of course, makes the functions easier to read and understand.

## Do One Thing

FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL.THEY SHOULD DO IT ONLY.

### Sections within Functions

The problem with this statement is that it is hard to know what "one thing" is.

```java
public static String renderPageWithSetupsAndTeardowns(PageData pageData, boolean isSuite) throws Exception {
    if (isTestPage(pageData))
        includeSetupAndTeardownPages(pageData, isSuite);
    return pageData.getHtml();
}
```

We can describe the function by describing it as a brief `TO` paragraph:

> TO RenderPageWithSetupsAndTeardowns, we check to see whether the page is a test page and if so, we include the setups and teardowns. In either case we render the page in HTML.

If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing.

## Use Descriptive Names

Remember Ward's principle: _"You know you are working on clean code when each routine turns out to be pretty much what you expected"_. Half the battle to achieving that principle is choosing good names for small functions that do one thing. The smaller and more focused a function is, the easier it is to choose a descriptive name.

Don't be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Don’t be afraid to spend time choosing a name. Indeed, you should try several different names and read the code with each in place.

Choosing descriptive names will clarify the design of the module in your mind and help you to improve it.

Be consistent in your names. Use the same phrases, nouns, and verbs in the function names you choose for your modules. Consider, for example, the names `includeSetupAndTeardownPages`, `includeSetupPages`, `includeSuiteSetupPage`, and `includeSetupPage`. The similar phraseology in those names allows the sequence to tell a story.

## Function Arguments

The ideal number of arguments for a function is zero. Next comes one, followed closely by two. Three arguments should be avoided where possible.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly.

### Common Monadic Forms

Try to avoid any monadic functions that don’t follow these forms, for example, _void includeSetupPageInto(StringBuffer pageText)_. Using an output argument instead of a return value for a transformation is confusing. If a function is going to transform its input argument, the transformation should appear as the return value.

### Argument Objects

When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider, for example, the difference between the two following declarations:

```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```

## Have No Side Effects

Side effects are lies. Your function promises to do one thing, but it also does other _hidden_ things. Sometimes it will make unexpected changes to the variables of its own class or to system globals. Consider, for example, the seemingly innocuous function. This function uses a standard algorithm to match a `userName` to a `password`. It returns `true` if they match and `false` if anything goes wrong. But it also has a side effect.

```java
public class UserValidator {
    private Cryptographer cryptographer;

    public boolean checkPassword(String userName, String password) {
        User user = UserGateway.findByName(userName);
        if (user != User.NULL) {
            String codedPhrase = user.getPhraseEncodedByPassword();
            String phrase = cryptographer.decrypt(codedPhrase, password);
            if ("Valid Password".equals(phrase)) {
                Session.initialize();
                return true;
            }
        }
        return false;
    }
}
```

The side effect is the call to `Session.initialize()`. The `checkPassword` function, by its name, says that it checks the password. The name does not imply that it initializes the session. So a caller runs the risk of erasing the existing session data when he or she decides to check the validity of the user.

This side effect creates a temporal coupling. That is, `checkPassword` can only be called at certain times (in other words, when it is safe to initialize the session). If you must have a temporal coupling, you should make it clear in the name of the function. In this case we might rename the function `checkPasswordAndInitializeSession`, though that certainly violates "Do one thing."

### Output Arguments

Arguments are most naturally interpreted as `inputs` to a function. If you have been programming for more than a few years, I’m sure you’ve done a double-take on an argument that was actually an `output` rather than an input. For example:

```java
public void appendFooter(StringBuffer report);
```

In OO languages much of the need for output arguments disappears because `this` is _intended_ to act as an output argument. In other words, it would be better for `appendFooter` to be invoked as:

```java
report.appendFooter();
```

If your function must change the state of something, have it change the state of its owning object.

## Command Query Separation

Functions should either do something or answer something, but not both. Consider, for example, the following function:

```java
public boolean set(String attribute, String value);
```

This function sets the value of a named attribute and returns true if it is successful and false if no such attribute exists. This leads to odd statements like this:

```java
if (set("username", "unclebob")) {
    ...
}
```

The solution is to separate the command from the query so that the ambiguity cannot occur.

```java
if (attributeExists("username")) {
    setAttribute("username", "unclebob");
    ...
}
```

## Don’t Repeat Yourself

Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it.

## How Do You Write Functions Like This?

Writing software is like any other kind of writing. When you write a paper or an article, you get your thoughts down first, then you massage it until it reads well. The first draft might be clumsy and disorganised, so you wordsmith it and restructure it and refine it until it reads the way you want it to read.

When I write functions, they come out long and complicated. But I also have a suite of unit tests that cover every one of those clumsy lines of code.

So then I massage and refine that code, splitting out functions, changing names, eliminating duplication. I shrink the methods and reorder them. Sometimes I break out whole classes, all the while keeping the tests passing. In the end, I wind up with functions that follow the rules I’ve laid down in this chapter.

I don’t write them that way to start. I don’t think anyone could.
