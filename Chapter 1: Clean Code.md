# Chapter 1: Clean Code

## Bad Code

They had rushed the product to market and had made a huge mess in the code. As they added more and more features, the code got worse and worse until they simply could not manage it any longer. It was the bad code that brought the company down.

We've all looked at the mess we've just made and then have chosen to leave it for another day. We've all felt the relief of seeing our messy program work and deciding that a working mess is better than nothing. We've all said we'd go back and clean it up later. Of course, later equals never.

## The Total Cost of Owning a Mess

Over time the mess becomes so big and so deep and so tall, they can not clean it up. There is no way at all. As the mess builds, the productivity of the team continues to decrease, asymptotically approaching zero

**_The Grand Redesign in the Sky_**

Eventually the team rebels. They demand a redesign. Management cannot deny that productivity is terrible and authorize the grand redesign in the sky. A new tiger team is selected. They get to start over and create something truly beautiful. Now the two teams are in a race. The tiger team must build a new system that does everything that the old system does. Not only that, they have to keep up with the changes that are continuously being made to the old system. Management will not replace the old system until the new system can do everything that the old system does. This race can go on for a very long time. I've seen it take 10 years. And by the time it's done, the original members of the tiger team are long gone, and the current members are demanding that the new system be redesigned because it's such a mess. If you have experienced even one small part of the story I just told, then you already know that spending time keeping your code clean is not just cost effective; it's a matter of professional survival.

**_Attitude_**

But the fault, dear Dilbert, is not in our stars, but in ourselves. We are unprofessional. This may be a bitter pill to swallow. How could this mess be our fault? What about the requirements? What about the schedule? What about the stupid managers and the useless marketing types? Don't they bear some of the blame? No. The managers and marketers look to us for the information they need to make promises and commitments; and even when they don't look to us, we should not be shy about telling them what we think.

They may defend the schedule and requirements with passion; but that's their job. It's your job to defend the code with equal passion.

So too it is unprofessional for programmers to bend to the will of managers who don't understand the risks of making messes.

**_The Art of Clean Code?_**

Writing clean code requires the disciplined use of a myriad little techniques applied through a painstakingly acquired sense of “cleanliness.” This “code-sense” is the key.

A programmer without “code-sense” can look at a messy module and recognize the mess but will have no idea what to do about it. A programmer with “code-sense” will look at a messy module and see options and variations.

**_What Is Clean Code?_**

> "I like my code to be elegant and efficient. The logic should be straightforward to make it hard for bugs to hide, the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy, and performance close to optimal so as not to tempt people to make the code messy with unprincipled optimizations. Clean code does one thing well."
>
> Bjarne Stroustrup, inventor of C++

Apparently Bjarne thinks that clean code is pleasing to read.

He uses the word "tempt." There is a deep truth here. Bad code tempts the mess to grow! When others change bad code, they tend to make it worse.

Pragmatic Dave Thomas and Andy Hunt said this a different way. They used the metaphor of broken windows. A building with broken windows looks like nobody cares about it. So other people stop caring. They allow more windows to become broken. Eventually they actively break them. They despoil the facade with graffiti and allow garbage to collect. One broken window starts the process toward decay.

Bad code tries to do too much. Clean code is focused.

---

> "Clean code is simple and direct. Clean code reads like well-written prose. Clean code never obscures the designer's intent but rather is full of crisp abstractions and straightforward lines of control."
>
> Grady Booch, author of "Object Oriented Analysis and Design with Applications"

---

> "Clean code can be read, and enhanced by a developer other than its original author. It has unit and acceptance tests. It has meaningful names. It provides one way rather than many ways for doing one thing. It has minimal dependencies, which are explicitly defined, and provides a clear and minimal API. Code should be literate since depending on the language, not all necessary information can be expressed clearly in code alone."
>
> Dave Thomas, founder of OTI, godfather of the Eclipse strategy

Dave asserts that clean code makes it easy for other people to enhance it. There is, after all, a difference between code that is easy to read and code that is easy to change.

Code, without tests, is not clean. No matter how elegant it is, no matter how readable and accessible, if it hath not tests, it be unclean.

The upshot is that the code should be composed in such a form as to make it readable by humans.

---

> Clean code always looks like it was written by someone who cares.
>
> Michael Feathers, author of "Working Effectively with Legacy Code"

---

> "In recent years I begin, and nearly end, with Beck's rules of simple code. In priority order, simple code:
>
> - Runs all the tests;
> - Contains no duplication;
> - Expresses all the design ideas that are in the system;
> - Minimizes the number of entities such as classes, methods, functions, and the like.
>
> Expressiveness to me includes meaningful names, and I am likely to change the names of things several times before I settle in.
>
> I also look at whether an object or method is doing more than one thing. If it's an object, it probably needs to be broken into two or more objects. If it's a method, I will always use the Extract Method refactoring on it, resulting in one method that says more clearly what it does, and some submethods saying how it is done."
>
> Ron Jeffries, author of "Extreme Programming Installed" and "Extreme Programming Adventures in C#"

---

> "You know you are working on clean code when each routine you read turns out to be pretty much what you expected. You can call it beautiful code when the code also makes it look like the language was made for the problem."
>
> Ward Cunningham, inventor of Wiki, inventor of Fit, coinventor of eXtreme Programming.

Ward expects that when you read clean code you won't be surprised at all. You will read it, and it will be pretty much what you expected. It will be obvious, simple, and compelling.

## Schools of Thought

But don't make the mistake of thinking that we are somehow "right" in any absolute sense.

Indeed, many of the recommendations in this book are controversial. You will probably not agree with all of them. You might violently disagree with some of them. That's fine.

## The Boy Scout Rule

It's not enough to write the code well. The code has to be kept clean over time.

The Boy Scouts of America have a simple rule that we can apply to our profession: "_Leave the campground cleaner than you found it_"
