# Chapter 4: Comments

If our programming languages were expressive enough, we would not need comments very much, perhaps not at all.

The proper use of comments is to compensate for our failure to express ourself in code. So when you find yourself in a position where you need to write a comment, think it through and see whether there isn't some way to turn the tables and express yourself in code.

Why am I so down on comments? The reason is simple. Programmers can't realistically maintain them.

It is possible to make the point that programmers should be disciplined enough to keep the comments in a high state of repair, relevance, and accuracy. I agree, they should. But I would rather that energy go toward making the code so clear and expressive that it does not need the comments in the first place.

## Comments Do Not Make Up for Bad Code

One of the more common motivations for writing comments is bad code. We write a module and we know it is confusing and disorganized. We know it's a mess. So we say to ourselves, "Ooh, I'd better comment that!" No! You'd better clean it!

## Explain Yourself in Code

Which would you rather see? This:

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```

Or this?

```java
if (employee.isEligibleForFullBenefits())
```

It takes only a few seconds of thought to explain most of your intent in code. In many cases it's simply a matter of creating a function that says the same thing as the comment you want to write.

## Good Comments

### Legal Comments

Sometimes our corporate coding standards force us to write certain comments for legal reasons. For example, copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file. Here, for example, is the standard comment header that we put at the beginning of every source file in FitNesse.

```java
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```

### Informative Comments

It is sometimes useful to provide basic information with a comment. For example, consider this comment that explains the return value of an abstract method:

```java
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
```

### TODO Comments

It is sometimes reasonable to leave "To do" notes in the form of `//TODO` comments. In the following case, the `TODO` comment explains why the function has a degenerate implementation and what that function's future should be.

```java
//TODO-MdM these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception {
    return null;
}
```

Whatever else a TODO might be, it is not an excuse to leave bad code in the system.

## Bad Comments

### Mumbling

If you decide to write a comment, then spend the time necessary to make sure it is the best comment you can write.

Here, for example, is a case I found in FitNesse, where a comment might indeed have been useful. But the author was in a hurry or just not paying much attention. His mumbling left behind an enigma:

```java
public void loadProperties() {
    try
    {
        String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
        FileInputStream propertiesStream = new FileInputStream(propertiesPath);
        loadedProperties.load(propertiesStream);
    }
    catch(IOException e) {
        // No properties files means all defaults are loaded
    }
}
```

What does that comment in the catch block mean? Our only recourse is to examine the code in other parts of the system to find out what's going on. Any comment that forces you to look in another module for the meaning of that comment has failed to communicate to you.

### Redundant Comments

In the following example, the header comment that is completely redundant. The comment probably takes longer to read than the code itself.

```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis) throws Exception {
    if(!closed){
        wait(timeoutMillis);
        if(!closed)
            throw new Exception("MockResponseSender could not be closed");
    }
}
```

What purpose does this comment serve? It's certainly not more informative than the code.

### Misleading Comments

Consider for another moment the misleading comment we saw above. The method does not return when `this.closed` becomes `true`. It returns _if_ `this.closed` is `true`; otherwise, it waits for a blind time-out and then throws an exception _if_ `this.closed` is still not `true`.

### Scary Noise

What purpose do the following Javadocs serve? Answer: nothing. They are just redundant noisy comments written out of some misplaced desire to provide documentation.

```java
/** The name. */
private String name;

/** The version. */
private String version;
```

### Closing Brace Comments

Sometimes programmers will put special comments on closing braces. Although this might make sense for long functions with deeply nested structures. So if you find yourself wanting to mark your closing braces, try to shorten your functions instead.

```java
public class wc {
    public static void main(String[] args) {
        try {
            while ((line = in.readLine()) != null) {
                ...
            } //while
        } // try
        catch (IOException e) {
            System.err.println("Error:" + e.getMessage());
        } //catch
    } //main
}
```

### Commented-Out Code

Few practices are as odious as commenting-out code. Don't do this!

```java
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
```

Why are those two lines of code commented? Others who see that commented-out code won't have the courage to delete it. They'll think it is there for a reason and is too important to delete.
