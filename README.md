﻿## :newspaper:About

​	:star: 这是一个请求跟踪Id，用于跟踪请求链路，整条链路用一个Guid作为Id关联起来；CorrelationId会将请求Id写入请求头、响应头；



## :golf:Use

:flags:.Net Core 3.1

```c#
using Zzz.CorrelationId.Extension;

public class Startup
{
	public void ConfigureServices(IServiceCollection services)
	{
		...
		
		//默认使用 X-RequestId且自动生成Id
		//services.AddCorrelationId();
         services.AddCorrelationId("CorrelationId");
         
         ...
  	}
    
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        ...
           
    	app.UseCorrelationId();    
            
    	...
    }
}
```



:flags:.Net 5/6/7

```C#
using Zzz.CorrelationId.Extension;

var builder = WebApplication.CreateBuilder(args);

...

builder.Services.AddHttpContextAccessor();

//builder.Services.AddCorrelationId();
builder.Services.AddCorrelationId("CorrelationId");

...

app.UseCorrelationId();

...
```



:flags:Test

```C#
public class WeatherForecastController : ControllerBase
{
	private readonly ILogger<WeatherForecastController> _logger;
	private readonly CorrelationInfo _correlation;

	public WeatherForecastController(ILogger<WeatherForecastController> logger, 
								CorrelationInfo correlation)
   	{
		_logger = logger;
		_correlation = correlation;
  	}
    
    public async Task Test()
	{
        //全局APP获取
        var requestFromAPP = APP.GetCorrelationId();

        //DI获取
        var requestFromDI = _correlation.Get();
	}

}

```









