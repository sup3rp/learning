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

Something something:
* npm
  ```sh
  npm install npm@latest -g
  ```

### Solve using the DI approach
Something something

## Conclusion
Something something