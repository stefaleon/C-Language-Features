## Language Features

### C# features used in web application development
### from [Pro ASP.NET Core MVC](https://www.apress.com/gp/book/9781484203972) by Adam Freeman

Freeman A. (2017) Essential C# Features. In: Pro ASP.NET Core MVC 2. Apress, Berkeley, CA

![](LanguageFeatures.png?raw=true)


&nbsp;
## 00 Preparing the Example Project

* Create an empty project using the ASP.NET Core Web Application (.NET Core) template.
* Enable the MVC framework by adding `services.AddMvc();` and `app.UseMvcWithDefaultRoute();` in *Startup.cs*.
* Add the *Models* folder and the *Product.cs* class.
* Add the *Controllers* folder and the *HomeController.cs* controller.
* Add the *Views/Home* folder and the *Index.cshtml* view.


&nbsp;
## 01 Using the Null Conditional Operator

```
string name = p?.Name;
decimal? price = p?.Price;
```
* The null conditional operator is a single question mark (the ? character). If p is null, then name will be set to
null as well. If p is not null, then name will be set to the value of the Product.Name property. The Price property is
subject to the same test. Notice that the variable you assign to when using the null conditional operator must be
able to be assigned null, which is why the price variable is declared as a nullable decimal (decimal?).
* The null conditional operator can be chained to navigate through a hierarchy of objects.

```
string relatedName = p?.Related?.Name;
```

* It can be useful to combine the null conditional operator (a single question mark) with the null coalescing
operator (two question marks) to set a fallback value to present null values being used in the application.

```
string name = p?.Name ?? "<No Name>";
decimal? price = p?.Price ?? 0;
string relatedName = p?.Related?.Name ?? "<None>";
```



&nbsp;
## 02 Using Automatically Implemented Properties

* C# supports automatically implemented properties and this feature allows to define properties without having to implement the get and set bodies.

`public string Name { get; set; }`

* The latest version of C# supports **initializers** for automatically implemented properties, which allows an initial value to be set without having
to use the constructor.

`public string Category { get; set; } = "Watersports";`


* You can create a **read-only** property by using an initializer and omitting the set keyword from an auto-implemented property that has an initializer.

`public bool InStock { get; } = true;`

The InStock property is initialized to true and cannot be changed; however, the value can be assigned to in the type’s constructor

```
public Product(bool stock = true) {
  InStock = stock;
}
```



&nbsp;
## 03 Using String Interpolation

* Unlike the string.Format method, string interpolation uses the variable names directly.

`results.Add($"Name: {name}, Price: {price}, Related: {relatedName}");`

Interpolated strings are prefixed with the $ character and contain holes, which are references to values
contained within the { and } characters. When the string is evaluated, the holes are filled in with the current
values of the variables or constants that are specified.  



&nbsp;
## 04 Using Object and Collection Initializers

* Instead of calling the Product constructor and then using the newly created object to set each of the properties, use an object initializer.

```
    Product kayak = new Product
    {
        Name = "Kayak",
        Category = "Water Craft",
        Price = 275M
    };
```

* Similarly, a **collection initializer** allows the creation of a collection and its contents to be specified in a single step.

```
  return View("Index", new string[] { "Bob", "Joe", "Alice" });
```

The array elements are specified between the { and } characters, which allows for a more concise definition of the collection and makes it possible to define a collection inline within a method call.

* The latest versions of C# support a more natural approach to initializing **indexed collections** that is consistent with the way that values are retrieved or modified once the collection has been initialized.

```
Dictionary<string, Product> products = new Dictionary<string, Product> {
["Kayak"] = new Product { Name = "Kayak", Price = 275M },
["Lifejacket"] = new Product { Name = "Lifejacket", Price = 48.95M }
};
```


&nbsp;
## 05 Pattern Matching

* Pattern matching can be used to test that an object is of a specific type or has specific characteristics. This is another form is syntactic sugar, and it can dramatically simplify complex blocks of conditional statements.

`if (data[i] is decimal d) {`

This expression will evaluate as true if the value stored in data[i] is a decimal. The value of data[i] will be assigned to the variable d, which allows it to be used in subsequent statements without needing to perform any type conversions.

* Pattern matching can also be used in switch statements, which support the when keyword for restricting when a value is matched by a case statement.

`case int intValue when intValue > 50:`

This case statement matches int values and assigns them to a variable called intValue, but only when the value is greater than 50.
