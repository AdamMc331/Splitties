# Checked Lazy
This library provides a `checkedLazy()` method that returns a `Lazy` delegate,
as well as `uiLazy()`.

`checkedLazy()` takes as first parameter a function where you can implement an access check.

The second parameter is the lazy initializer, as in Kotlin stdlib `lazy`.

`uiLazy { … }` is a shorthand for `checkedLazy(::checkUiThread) { … }`.
It's there because UI thread checking is a common use case on Android due to
its synchronized nature and its omnipresence.

## Example

```kotlin
val noUiThreadChecker = noAccessOn(uiThread)

class YourClass {
    val greeting: String by uiLazy { "Hello Splitties!" }
    val expensiveObject by checkedLazy(noUiThreadChecker) { doHeavyInstantiation() }
}
```
