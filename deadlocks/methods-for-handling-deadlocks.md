# Methods for Handling Deadlocks

There are two ways handling deadlocks, guaranteeing that deadlock will not occur

1. Prevention
2. Avoidance

Prevention is to prevent one of the four condition.  
Avoidance requires process to provide resource usage plan.

If system do not uses any of this, system investigate if deadlock really occurred, if deadlock occurred, system restore itself with some algorithms

In many system deadlock occurs rarely\(so to speak, once in a year\). That is, restoring can be much more cheaper than prevention / avoidance.

## Java Deadlock Handling

**JVM does nothing to resolve deadlock. It is programmer's job to write deadlock-free program**.

// TODO

