In C++, the `override` keyword is used to explicitly indicate to the compiler that a member function in a derived class is intended to override a virtual function in the base class. This helps in catching errors at compile-time and makes the code more readable.

Consider a scenario where you have a base class with a virtual function, and you want to provide a specific implementation of that function in a derived class. Using `override` ensures that the function in the derived class is indeed intended to override a virtual function in the base class. If there is a mistake in the function signature or if there is no corresponding virtual function in the base class, the compiler will generate an error.

Here's an example:

```cpp
class Base {
public:
    virtual void foo() const {
        // Some implementation in the base class
    }
};

class Derived : public Base {
public:
    void foo() const override {
        // Specific implementation in the derived class
    }
};
```

In this example:

- The `Base` class has a virtual function `foo()`.
- The `Derived` class inherits from the `Base` class and provides its implementation of `foo()`.

The `override` keyword after the function declaration in the `Derived` class indicates that `foo()` in `Derived` is meant to override `foo()` in `Base`. If there's an error in the function signature or if there is no matching virtual function in the base class, the compiler will generate an error, alerting you to the issue.

Here's a common mistake that the `override` keyword can help catch:

```cpp
class Derived : public Base {
public:
    void foo(int x) const override {
        // Error: The signature doesn't match the base class
    }
};
```

In this case, the compiler will generate an error because `foo(int x)` in `Derived` does not match the signature of the virtual function in the `Base` class. Using `override` helps avoid accidental errors of this kind.