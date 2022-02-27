# Chapter 10: Classes

## Classes Should Be Small!

The first rule of classes is that they should be small. With classes we measured size by responsibilities.

The name of a class should describe what responsibilities it fulfills. If we cannot derive a concise name for a class, then it's likely too large. The more ambiguous the class name, the more likely it has too many responsibilities.

We move on to the next problem rather than going back and breaking the overstuffed classes into decoupled units with single responsibilities.

Every sizable system will contain a large amount of logic and complexity. The primary goal in managing such complexity is to organize it so that a developer knows where to look to find things and need only understand the directly affected complexity at any given time.

We want our systems to be composed of many small classes, not a few large ones. Each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviors.

So breaking a large function into many smaller functions often gives us the opportunity to split several smaller classes out as well. This gives our program a much better organization and a more transparent structure.

## Organizing for Change

Dependencies upon concrete details create challenges for testing our system. Instead of designing Portfolio so that it directly depends upon TokyoStockExchange, we create an interface, StockExchange, that declares a single method:

```java
public interface StockExchange {
    Money currentPrice(String symbol);
}
```

Now our test can create a testable implementation of the StockExchange interface that emulates the TokyoStockExchange. Our test implementation of the StockExchange interface reduces to a simple table lookup.

If a system is decoupled enough to be tested in this way, it will also be more flexible and promote more reuse. The lack of coupling means that the elements of our system are better isolated from each other and from change. This isolation makes it easier to understand each element of the system.
