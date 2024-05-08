# C#: Basics Summary

Start with the [C# programming guide](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/) from Microsoft. Fall back to the [C# reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/) when you need information about a specific topic.

After reading these documents, you should have the following basic knowledge.

## Basic knowledge

### Built in types

- Boolean: bool, true, false
- Numeric types
    - Integral types: byte, short, ushort, int, uint, long, ulong
    - Floating point numbers: float, double, understand that these are *inprecise*. See [Floating point comparison](https://floating-point-gui.de/errors/comparison/) to understand why you should never use these to represent *money*.
    - Monetary types: decimal (16 bytes), allows *exact* representation of fractional numbers
	- [String formatting](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)
	- Special types for specific purposes can be found in [System.Numerics](https://learn.microsoft.com/en-us/dotnet/api/system.numerics?view=net-8.0)
- Date and time: DateTime, TimeSpan, DateTimeOffset, DateOnly, TimeOnly
    - DateTime.Now <> DateTime.UtcNow
	- [String formatting](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-date-and-time-format-strings)
	- TODO: NodaTime
	- TODO: DateTimeKind
	- TODO: Stopwatch / GetTimestamp() / GetEllapsedTime
- char
- string
    - Reference type, so it can contain `null`.
    - Strings are immutable, concatenation/... always creates a new string
    - Encodings: ASCII, UTF-8, UTF-16, UTF-32 (TODO)
	- [Escape sequences](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/strings/#string-escape-sequences): `\t`, `\n`, `\r`, `\\`, `\'`, `\"`
	- Verbatim string literals: `@"a verbatim string ""with quotes"". It can be multi-line."`
	- Raw string literals: `"""A raw string literal "with quotes". It can be multi-line?"""`. *Use this for inline XML, JSON, ... content in your code*
	- String interpolation: `$"A string with an auto formatted {variable} or {(int)obj.Count} inline code"`. Can be combined with Raw string literals `$"""str"""` and verbatim string literals `$@"str"`. *Be wary of the performance impact when used in combination with logging libraries.* Since string interpolation will happen before the logging library might decide to skip the message based on the configured log level. For example: `logger.Debug($"A {very.HeavyFunctionCall()}");` will always call the function, but it might not end up in the log file.
	- Use `StringBuilder` when composing very big strings.
	- Access individual characters: `str[i]`
	- [Simple string operations](https://learn.microsoft.com/en-us/dotnet/api/system.string?view=net-8.0): `IndexOf`, `ToLower`, `ToUpper`, `Substring`, `Join`, `Split`, `Trim`, `Equals`, `Contains`
	- `StringComparison.Ordinal` / `StringComparison.OrdinalIgnoreCase` / `StringComparison.InvariantCulture` / `StringComparison.InvariantCultureIgnoreCase`. [More information](https://learn.microsoft.com/en-us/dotnet/api/system.stringcomparison?view=net-8.0)
- Guid
    - 16 byte globally unique identifier, e.g. `e911f42c-5468-4f3e-a5c5-46e2d70ed19d`
	- Guid.NewGuid() is pretty much guaranteed to be unique.
	- Understand that .NET uses GUID v4
	- See [Guid usage in DB's](db/Guid_do_dont.md) for more information about GUID usage in databases, potential pitfalls and the use of GUID v7.

### Control Flow

- `return`
- `if`, `else if` and `else`
- `for` and `foreach`
- `do while`, `while`
- `switch`, `case`, `default`
- `break` and `continue`
- `try`, `catch`, `finally`
    - `when` is very powerfull to add additional conditions when catching exceptions
- `throw` [Exceptions](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/exceptions)
- `using` [to correctly dispose objects](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/using)
- `yield return` and `yield break` [when working with IEnumerable<T>](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/yield)

It might be very tempting to write 1-liner control flow statements without curly braces.
However, as stated in ['the laws'](general/The_laws.md), don't try to outsmart yourself. Always use curly braces. A last minute friday afternoon commit might bite you in the ass if you are not carefull.

```
if (someVar)
	dont.DoThis();

if (someVar) {
	// do this instead
	myVar.Call();
}
```

What you shouldn't focus on as a beginner:

- `lock`: In my opinion it is no longer relevant in modern C#. See [threading](dotnet/Threading.md) for better alternatives.
- `fixed`: Used for GC memory pinning in the context of native interop.
- `checked`, `unchecked`: Used for arithmetic without overflow protection.
- `unsafe` and `type*` pointers: [Used for native interop](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/unsafe-code)


### Classes, structures and enums

- [Namespace](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/namespaces)
- [Class](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes)
- [Record](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/records)
- [Interface](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/types/interfaces)
- [Generics](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/generics/generic-type-parameters)

- TODO: structures, nested types, partial classes, attributes


### Members

- [Access Modifiers](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers): `private`, `protected`, `internal`, `public`, `protected internal`, `private protected`
- [Fields](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/fields): `private int myField;`
- [Properties](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties): `public string? Name { get; set; }`, `init`, `required`
- [Methods](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods): `public void DoSomething()`
    - TODO: in/out/ref parameters
- [Constructors](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors)
- [Events](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/events/)
- [Indexers](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/indexers/)
- [Polymorphism](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/versioning-with-the-override-and-new-keywords): `abstract`, `override`, `new`
- [Finalizers](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/finalizers)

- TODO: indexers, methods, inner types, delegates, partial methods

### Expressions

See [the full overview](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/).

- Assignment: `=` and compound assignment `a = b = c`
- Arithmetic: `+`, `++`, `-`, `--`, `*`, `/`, `%`, `+=`, `-=`, `*=`, `/=`, `%=`
- Boolean logic: `&&`, `||`, `!`
- Bitwise operations: `&`, `|`, `^`, `~` `<<`, `>>`, `>>>`, `&=`, `|=`, `^=`, `~=` `<<=`, `>>=`, `>>>=`
- Equality: `==`, `!=`. See [Equality Operators](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/equality-operators) to understand reference type equality vs value type equality.
- Comparison: `>`, `<`, `>=`, `<=`
- [Ternaty conditional](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/conditional-operator): `condition ? trueStatement : falseStatement;`
- Type casting: `(SomeType)myVar`
- Type testing: `as SomeType`, `is SomeType x`, `is not SomeType x`, `is null`, `is not null`
- [Null conditional](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-): `myVar?.SomeMethod()`
- [Null coalescing](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-coalescing-operator): `var1 ?? var2` and `var ??= new MyClass()`
- [Null Forgiving](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/null-forgiving): `myVar!.x`
- [Lambda Expression](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator): `() => {}`
- Collection expressions: TODO
- TODO: default, await, default, default(T), default!, new, typeof, nameof, sizeof, user defined operators
- TODO: patterns https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/operators/patterns

Note: `await` is described in depth in [Async/Await](Async_await.md).

### Preprocessor Directives

See the [full preprocessor directive reference](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/preprocessor-directives).

- Test a compile time condition: `#if DEBUG`, `#elif`, `#else`, `#endif`
- Enable/disable compiler warnings: `#pragma warning disable XXXX`, `#pragma warning restore XXXX`

### TODO:

- operators, overloading
- async/await / await foreach / await using
- switch expression, pattern matching, pattern subsumption, pattern exhaustiveness
- is/as, casting
- var
- lambda
- expression trees
- Exceptions
- tuple, tuple return syntax, multi assign
- dynamic, typeof, nameof
- Action, delegate
