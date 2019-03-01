# Kros.BusEventDoc

Tool for generating documentation of domain events. Inludes a simple UI to depict what specified events, commands are used in specific service.
This library is inspired by [`Swagger`](https://github.com/domaindrivendev/Swashbuckle.AspNetCore). Project is still evolving.

## Get Started

1. Instal Nuget package into your ASP.NET Core application.

```console
dotnet add package Kros.BusEventDoc
```

2. In the ConfigureServices method of Startup.cs, register the BusEventDoc generator, defining BusEventDoc document.

```csharp
using Kros.EventBusDoc.Generator.Middleware.Extensions;

services.AddEventBusDocGen(c =>
    c.EventBusDoc("v1", new Info { Version = "v1", Title = "Demo" })
);
```

3. In the Configure method, attach to the pipeline BusEventDoc generator. Generator produces json.

```csharp
app.UseEventBusDoc();
```

4. For generation and exploring definitions and types use BusEventDoc attribute annotation to specify the subjects.

```csharp
using Kros.EventBusDoc.Generator.BusentAnnotation;

[assembly: BusEvent(EventType =typeof(ISendEvent) )]
[assembly: EventBusCommandConsumer(EventType =typeof(IConsumeOne) )]
[assembly: EventBusCommandSender(EventType =typeof(ISendCommand) )]
```

5. To visual json document generated by BusEventDoc generator insert BusEventDoc UI middleware, with specific endpoint(s).

```csharp
app.UseEventBusDocUI(c => { c.EventBusDocEndPoint("v1/busent.json", "Demo"); });
```

6. If the BusEventDoc is configured we can call for output *"/busent"*.

You can see simple example [DEMO](https://github.com/Kros-sk/Kros.BusEventDoc/tree/master/demo/Kros.EventBusDoc.Demo)