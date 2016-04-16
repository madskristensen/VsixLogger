# Vsix Logger

[![Build status](https://ci.appveyor.com/api/projects/status/as39v33vy4c5v2t0?svg=true)](https://ci.appveyor.com/project/madskristensen/vsixlogger)

Adds logging and telemetry support to Visual Studio extensions.

Available as [VsixLogger on NuGet](https://www.nuget.org/packages/VsixLogger/)

---------------------------------------------------

## Features

- Easy to setup and use
- Logs any string message to Output Window
- Logs any exception to Output Window
- Logs any exception to Application Insights
- Tracks custom events through Application Insights

## Initialize the logger
From the Visual Studio extension's package file's `Initialize()`
method, call `Logger.Initialize()` to set everything up. This
is the only thing needed to be able to start using the logger.

### Logger
Here's is how to initialize the logger.

```c#
protected override void Initialize()
{
  base.Initialize();
  Logger.Initialize(this, "Vsix name");
}
```

### Logger + Telemetry
Here's is an example on how to initialize the logger as well
as the Application Insights telemetry.

```c#
protected override void Initialize()
{
  base.Initialize();
  Logger.Initialize(this, "Vsix name", "Version", "177c7fed-9dec-4947-b29d-5d3ff53a50e3");
}
```

## API

### Logger
Use the `Logger.Log` method to log exceptions or strings to
the Output Window. If the `Telemetry` client has been
initialized then exceptions are logged to Application Insights
as well.

#### Exceptions
```C#
try {
  // code
}
catch (Exception ex){
  Logger.Log(ex);
}
```

#### Any string

```C#
  Logger.Log("Some string");
```

### Telemetry
The `Telemetry` class allows you to track both exceptions
and custom events with Application Insights.

#### Exceptions
It's recommended to use `Logger.Log(Exception)` to log
exceptions.

```C#
try {
  // code
}
catch (Exception ex){
  Telemetry.TrackException(ex);
}
```

#### Events

```C#
  Telemetry.TrackEvent("event name", properties = null, metrics = null);
```

## Contribute
Bug reports and pull requests are more than welcome.

## License
[Apache 2.0](LICENSE)