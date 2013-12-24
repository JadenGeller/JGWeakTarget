JGWeakTarget
============

A proxy object used to weak reference the target in a target/selector callback. To use, initialize an instance of JGWeakTarger with the desired target and selector. Then, use the weakTarget and weakSelector property when creating a target/selector callback. JGWeakTarget will maintain a weak reference to the target and relay the recieved callbacks to the selector.

Example
============

The following example creates a weak reference to `self` using JGWeakTarget. After creating an instance of JGWeakTarget, the `weakTarget` and `weakSelector` properties are used as the target and the selector for the NSTimer. This creates a normally functioning target/selector callback with the difference in that the NSTimer does not hold a strong reference to `self`. Thus, the timer will not prevent `self` from being deallocated. Notice that this also implies that, upon deallocation of the class with the weak reference, the timer must be invalidated.

```
JGWeakTarget *weakSelf = [JGWeakTarget weakTargetWithTarget:self selector:@selector(timerFired:)];
[NSTimer scheduledTimerWithTimeInterval:10 target:weakSelf.weakTarget selector:weakSelf.weakSelector userInfo:nil repeats:YES];
```

JGWeakTarget can be used with any classes that take target/selector parameters, such as CADisplayLayer and NSTimer. In addition, selectors with or without sender arguments can be used.
