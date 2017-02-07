# Lecture 11

## Last time -- constructors, copy constructors

-----------------

## Destructor

When an object is destroyed, the destructor runs.

Sequence of events when an object is destroyed.
  1. dtor body runs
  2. dtors for fields that are objects, reverse declaration order.
  3. memory reclaimed.
