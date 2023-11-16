<!-- PROJECT LOGO -->
<br />
<div align="center">
  

  <h3 align="center">🏭 Factory Pattern using Dependency Injection (DI) in order to resolve dependencies. 🏭</h3>
  
  <p>Followed instructions from https://medium.com/null-exception/factory-pattern-using-built-in-dependency-injection-of-asp-net-core-f91bd3b58665
</p>
</div>




<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#the-factory-pattern">The Factory Pattern</a></li>
    <li>
      <a href="#traditional-vs-di-approach">Traditional vs DI approach</a>
      <ul>
        <li><a href="#the-original-problem">The original problem</a></li>
        <li><a href="#solve-using-the-traditional-approach">Solve using the traditional approach</a></li>
        <li><a href="#solve-using-the-di-approach">Solve using the DI approach</a></li>
      </ul>
    </li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ol>
</details>

<!-- THE FACTORY PATTERN -->
## The Factory Pattern
<p align="center">A factory pattern belongs to the creational patterns from Gang of 4. It is a creational design pattern that solves the problem of creating object without exposing the creation logic to the client. </p>

<!-- TRADITIONAL APPROACH -->
## Traditional vs DI approach
Something something
### The original problem
<p>Taking a real world example from the source article, let's say we have service contract for a stream service which exposes a <i>ShowMovies</i> method.</p>

 ```csharp
  public interface IStreamService
  {
      string[] ShowMovies();
  }
  ```

<p>We also have two services, Netflix and Amazon, that implement the contract above.</p>

 ```csharp
  public class NetflixStreamService: IStreamService
  {
      public string[] ShowMovies()
      {
          return new string[]
          {
              "Movie 1",
              "Movie 2",
              "Movie 3"
          };
      }
  }

  public class AmazonStreamService: IStreamService
  {
      public string[] ShowMovies()
      {
          return new string[]
          {
              "Movie A",
              "Movie B",
              "Movie C"
          };
      }
  }

  ```

<p>We now want to refactor the code, so that the client calling this service does not need to know the specifics of how this service is instantiated, that's where the Factory Pattern comes in handy.</p>

### Solve using the traditional approach
<p>In order to implement the Factory Pattern we create a new class called <i>StreamFactory</i> that implements a <i>GetStreamService</i> which returns the appropriate service according to the string <i>userSelection</i> that is passed in the method.</p>

```csharp
  public class StreamFactory
  {
      public IStreamService GetStreamService(string userSelection)
      {
          if(userSelection == "netflix")
          {
              return new NetflixStreamService();
          }
          else
          {
              return new AmazonStreamService();
          }
      }
  }
  ```

<p>In the client code (in this case, the Controller) we just need to call the <i>StreamFactory</i> class and the method <i>GetStreamService</i> and pass the <i>userSelection</i> string.</p>

  ```csharp
  public class StreamController : Controller
  {
      private readonly StreamFactory streamFactory;

      public StreamController(StreamFactory streamFactory)
      {
          this.streamFactory = streamFactory;
      }
      [HttpGet("movies/{userSelection}")]
      public IEnumerable<string> GetMovies(string userSelection)
      {
          return streamFactory.GetStreamService(userSelection).ShowMovies();
      }
  }
  ```

<p>Finally, we have to add the <i>StreamFactory</i> to the <i>Startup</i> class so that DI instantiates the class for us, alternatively we could create <i>StreamFactory</i> as a static class.</p>

  ```csharp
 public void ConfigureServices(IServiceCollection services)
  {
      services.AddMvc();

      services.AddScoped<StreamFactory>();

  }
  ```



### Solve using the DI approach

We can go beyond and turn this code even more usable by using DI to solve any depedencies that both services that can come from the constructors. Let's update the <i>StreamFactory</i> class.

  ```csharp
public class StreamFactory
{
    private readonly IServiceProvider serviceProvider;

    public StreamFactory(IServiceProvider serviceProvider)
    {
        this.serviceProvider = serviceProvider;
    }
    
    public IStreamService GetStreamService(string userSelection)
    {
        if(userSelection =="Netflix")
            return (IStreamService)serviceProvider.GetService(typeof(NetflixStreamService));
        
        return (IStreamService)serviceProvider.GetService(typeof(AmazonStreamService));
    }
    
}
```

<p>Here we delegate the responsability to the <i>IServiceProvider</i> of getting the appropriate instance of the <i>IStreamService</i> with all the dependencies taken care, but in order for this to happen we need to register both services in the <i>Startup.cs</i> class.</p>

```charp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();

    services.AddScoped<StreamFactory>();
    
    services.AddScoped<NetflixStreamService>()
                .AddScoped<IStreamService, NetflixStreamService>(s => s.GetService<NetflixStreamService>());
                
    services.AddScoped<AmazonStreamService>()
                .AddScoped<IStreamService, AmazonStreamService>(s => s.GetService<AmazonStreamService>());
}
```

<p>As of now, all future changes to the dependencies of the <i>NetflixStreamService</i> and <i>AmazonStreamService</i> classes (i.e. changes in the constructor) are automatically taken care by the DI at runtime. <b>Note:</b> All dependencies must be configured with DI as well.</p>

## Conclusion
The Factory Pattern is a good pattern if we don't want to expose the client to the details of how to instantiate certain classes. We might go even further and make it more reusable by making the DI take care of all dependencies that come from the classes that the Factory is responsible for instantiating.