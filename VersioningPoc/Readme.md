

Install-Package Microsoft.AspNetCore.Mvc.Versioning
Install-Package Microsoft.AspNetCore.Mvc.Versioning.ApiExplorer


-- program.cs

* let’s set up the main configuration for versioning:
```C#
builder.Services.AddApiVersioning(o =>
{
    o.AssumeDefaultVersionWhenUnspecified = true;
    o.DefaultApiVersion = new Microsoft.AspNetCore.Mvc.ApiVersion(1, 0);
    o.ReportApiVersions = true;
    o.ApiVersionReader = ApiVersionReader.Combine(
        new QueryStringApiVersionReader("api-version"),
        new HeaderApiVersionReader("X-Version"),
        new MediaTypeApiVersionReader("ver"));
});
```
* Finally, because we are going to support different versioning schemes, with the ApiVersionReader property, we combine different ways of reading the API version (from a query string, request header, and media type).

```C#
builder.Services.AddVersionedApiExplorer(
    options =>
    {
        options.GroupNameFormat = "'v'VVV";
        options.SubstituteApiVersionInUrl = true;
    });
```


** Definir con que versiones va ser compatible

```C#
    [ApiVersion("1.0")]
    [ApiVersion("2.0")]
    MyController
```