## 🌐 Weather & Utility API Frontend (ASP.NET Core MVC)

This frontend is a simple ASP.NET Core MVC web application that consumes a Node.js backend API hosted on Render. It allows users to:

* ☔️ Check weather for any city
* 🔄 Reverse a string
* ➕ Add two numbers
* ⏰ Get the current server time
* 🎲 Generate a random number

---

### 🛠️ Prerequisites

* Visual Studio 2022 or later
* Running backend API (deployed on Render)
* OpenWeatherMap API key configured in the backend

---

### 🧰 Steps to Create the Frontend in Visual Studio

#### 1. Create a New ASP.NET Core MVC Project

* Open Visual Studio.
* Click **Create a new project**.
* Choose **ASP.NET Core Web App (Model-View-Controller)**.
* Name the project (e.g., `WeatherFrontend`) and choose a location.
* Select **.NET 8 (LTS)** or higher.
* Check **Enable container support**.
* Click **Create**.

#### 2. Create the Data Models

* Add a folder named `Models`.
* Create a `WeatherModel` class to represent weather data.

#### 3. Add a Service Class to Call the API

* Add a folder named `Services`.
* Create a class `ApiService.cs` to call your backend endpoints using `HttpClient`.
* Implement methods for:

  * `GetWeatherAsync(string city)`
  * `ReverseTextAsync(string text)`
  * `AddNumbersAsync(int a, int b)`
  * `GetCurrentTimeAsync()`
  * `GetRandomNumberAsync()`
* An example of what these will look like using GetRandomNumberAsync() 
```c#
        public async Task<int?> GetRandomNumberAsync()
        {
            var response = await _http.GetAsync("/random");
            if (response.IsSuccessStatusCode)
            {
                var json = await response.Content.ReadAsStringAsync();
                using var doc = JsonDocument.Parse(json);
                return doc.RootElement.GetProperty("random").GetInt32();
            }
            return null;
        }
```
  

#### 4. Create a Controller

* Add a new controller named `WeatherController.cs`.
* Instantiate the `ApiService`.
* Add action methods:

  * `Index()`
  * `GetWeather(string city)`
  * `Reverse(string input)`
  * `Add(int a, int b)`
  * `Time()`
  * `Random()`
* An example of what these will look like using Random() and Index()
```c#
    public class WeatherController : Controller
    {
        private readonly ApiService _apiService;

        public WeatherController()
        {
            _apiService = new ApiService();
        }

        public IActionResult Index() => View();
        [HttpGet]
        public async Task<IActionResult> Random()
        {
            var random = await _apiService.GetRandomNumberAsync();
            ViewBag.RandomNumber = random;
            return View("RandomResult");
        }
   }
```

#### 5. Create Views

* Inside the `Views` folder, add a `Weather` subfolder.
* Add the following views:

  * `Index.cshtml` – Homepage with forms for all features, include input fields here and buttons to execute the api request and once the request is sent the following will occur:
  * `WeatherResult.cshtml` – Display weather info
  * `ReverseResult.cshtml` – Display reversed string
  * `AddResult.cshtml` – Show sum result
  * `TimeResult.cshtml` – Show current time
  * `RandomResult.cshtml` – Show random number

#### 6. Set the Default Route

* In `Program.cs`, change the default route to `Weather/Index` so it opens up on this page:

```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Weather}/{action=Index}/{id?}");
```

#### 7. Run the Application

You should now see a page with forms for:

* Weather lookup
* Text reversal
* Adding numbers
* Getting current time
* Getting a random number

---

### 🔄 Backend API Endpoints Used

| Method | Endpoint          | Purpose                     |
| ------ | ----------------- | --------------------------- |
| GET    | `/weather/{city}` | Get weather data            |
| POST   | `/reverse`        | Reverse input string        |
| GET    | `/add?a=1&b=2`    | Add two numbers             |
| GET    | `/time`           | Get current server time     |
| GET    | `/random`         | Get a random number (0-999) |


