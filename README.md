## Language Features

### C# features used in web application development
### from [Pro ASP.NET Core MVC](https://www.apress.com/gp/book/9781484203972)

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
