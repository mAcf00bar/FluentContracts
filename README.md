<img alt="Logo" width="100px" src="https://github.com/FluentContracts/FluentContracts/raw/develop/assets/icon.png"/>

# FluentContracts
![NuGet Version](https://img.shields.io/nuget/v/FluentContracts?style=for-the-badge&logo=nuget&logoColor=white&color=green)
![NuGet Downloads](https://img.shields.io/nuget/dt/FluentContracts?style=for-the-badge&logo=nuget&logoColor=white)

API for defining argument validation contracts in a fluent manner.

Inspired by [FluentAssertions](https://github.com/fluentassertions/fluentassertions)

## Builds

|     Type      | Status                                                                                                                                                                                                                                                         |
|:-------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   Dev Build   | [![Dev Linux](https://img.shields.io/github/actions/workflow/status/FluentContracts/FluentContracts/dev-linux.yml?branch=dev&style=for-the-badge&logo=linux&logoColor=white)](https://github.com/FluentContracts/FluentContracts/actions)                              |
|   Dev Build   | [![Dev Windows](https://img.shields.io/github/actions/workflow/status/FluentContracts/FluentContracts/dev-windows.yml?branch=dev&style=for-the-badge&logo=windows10&logoColor=white)](https://github.com/FluentContracts/FluentContracts/actions)                      |
|   Dev Build   | [![Dev MacOS](https://img.shields.io/github/actions/workflow/status/FluentContracts/FluentContracts/dev-macos.yml?branch=dev&style=for-the-badge&logo=Apple&logoColor=white)](https://github.com/FluentContracts/FluentContracts/actions)                              |
| Code Coverage | [![Coveralls](https://img.shields.io/coverallsCoverage/github/FluentContracts/FluentContracts?branch=dev&style=for-the-badge&logo=coveralls&logoColor=white)](https://coveralls.io/github/FluentContracts/FluentContracts)                                             |
|    Release    | [![Release](https://img.shields.io/github/actions/workflow/status/FluentContracts/FluentContracts/master-release.yml?branch=master&style=for-the-badge&logo=nuget&logoColor=white&label=NuGet%20Packages)](https://github.com/FluentContracts/FluentContracts/actions) |

## Why another validation library

I am  perfectly aware of the other libraries out there, that are doing the same stuff.

Libraries like [FluentValidation](https://github.com/FluentValidation/FluentValidation) and `Guard` from [.NET Community Toolkit](https://github.com/CommunityToolkit/dotnet) are awesome 
and have tons of functionality, support and experience. If you like those and use them already, that is fine.

I did this one, because I don't really like how the other libraries require you to write, in order to achieve the validation.
It is pretty verbose for my taste. I wanted to make something more simple and "human-readable", the same way [FluentAssertions](https://github.com/fluentassertions/fluentassertions) does it for unit testing.

## Usage

The usage of the contracts is pretty simple. You can use the extension methods everywhere you want to do a validation of some variable.

Generally when we write methods, constructors, etc., we do validation like that:
```csharp
public void AddOrder(Order myOrder)
{
    if (myOrder == null) throw new ArgumentNullException(nameof(myOrder));    
    if (myOrder.Quantity < 5) throw new OrderQuantityException("Order quantity cannot be less than 5");
    
    ...
}
```

With `FluentContracts` your code will look like this:
```csharp
public void AddOrder(Order myOrder)
{
    myOrder
        .Must()
        .NotBeNull()
        .And
        .Satisfy<OrderQuantityException>(
            o => o.Quantity >= 5, 
            "Order quantity cannot be less than 5");
    
    ...
}
```

or as simple as:

```csharp
public int Divide(int a, int b)
{
    b.Must().NotBe(0);    
    return a / b;
}
```
### User defined exceptions

You can also throw your own exception like that:
```csharp
public void AddOrder(Order myOrder)
{
    myOrder.Must().NotBeNull<OrderNullException>();
}
```

This will throw an instance of `OrderNullException` if `myOrder` is `null`.

## Help needed

This is just getting started, so I need some help. If you are interested in helping out just contact me on any of the following:

- [Blog](https://todorov.bg)
- [Twitter](https://twitter.com/totollygeek/)
- [LinkedIn](https://www.linkedin.com/in/totollygeek/)

or just send a pull request, open an issue, etc.

## Credits

Icon made by [IconMonk](https://www.flaticon.com/authors/icon-monk) from [Flaticon](https://www.flaticon.com) 
