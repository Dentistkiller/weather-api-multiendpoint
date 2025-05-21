🌐 Weather & Utility API Frontend (ASP.NET Core MVC)
This frontend is a simple ASP.NET Core MVC web application that consumes your Node.js backend API hosted on Render. It allows users to check the weather, reverse text, and interact with various utility endpoints.

🛠️ Prerequisites
Visual Studio 2022 or later

An existing running backend API (deployed on Render)

OpenWeatherMap API key (already set in backend/ on render)

🧰 Steps to Create the Frontend in Visual Studio
1. Create a New ASP.NET Core MVC Project
Open Visual Studio.

Click Create a new project.

Choose ASP.NET Core Web App (Model-View-Controller).

Name your project (e.g., WeatherFrontend), choose a location, then click Next.

Select .NET 8 (Long-term support) or higher.

Check enable container support

Click Create.

2. Create the Data Models
Add a new folder named Models.

Create amodel class to represent the API responses (for weather data).

3. Add a Service Class to Call the API
Create a folder named Services.

Create a class that uses HttpClient to communicate with your Node.js backend endpoints.

Implement methods to:

Fetch weather data.

Reverse text.

Call any other available endpoints.

4. Create a Controller
Add a new controller named WeatherController.

Inject or instantiate the service class.

Create action methods to handle:

Fetching weather info.

Reversing text.

Rendering the appropriate views.

5. Create Views
Inside the Views folder, create a subfolder named Weather.

Create the following views:

Index.cshtml for the homepage with forms.

WeatherResult.cshtml to display weather info.

ReverseResult.cshtml to display reversed text.

6. Set the Default Route
Open Program.cs or Startup.cs.

Set the default route to point to Weather/Index.

7. Run the Application
Press F5 or click Start Debugging.

The homepage should allow you to:

Enter a city name and get weather data.

Enter text to reverse.

🔄 Backend API Endpoints Used
This frontend interacts with the following API endpoints:

GET /weather/{city} – Get weather data for a specific city

POST /reverse – Reverse a given string
