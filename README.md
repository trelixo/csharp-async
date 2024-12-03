
# Training Assignment: Learning C# Asynchronous Programming

This assignment will teach beginners how to use asynchronous programming in C# by building a **Movie List Console Application**. The project will involve fetching movie data from the OMDB API, processing the data asynchronously, and displaying it in the console.

---

## **Step 1: Understand Asynchronous Programming Basics**
1. **Concepts to Study:**
   - What is asynchronous programming?
   - The difference between synchronous and asynchronous code.
   - Task-based asynchronous programming in C# (`async` and `await` keywords).

2. **Resources:**
   - [Microsoft Docs: Asynchronous Programming](https://learn.microsoft.com/en-us/dotnet/csharp/async)
   - Practice small examples, such as creating a method to simulate a delay using `Task.Delay`.

---

## **Step 2: Setup the Development Environment**
1. Install **Visual Studio** or **Visual Studio Code** with the C# extension.
2. Create a new **Console Application** project in Visual Studio:
   - Name it `MovieListApp`.

---

## **Step 3: Explore the OMDB API**
1. Open the URL in a browser to understand the JSON structure returned by the API:
   ```
   https://www.omdbapi.com/?apikey=e2fae6ec&s=batman&page=1
   ```
2. Analyze the JSON response to identify fields like `Title`, `Year`, and `Poster`.

3. **Task**: Write a small C# program to make a synchronous HTTP GET request using `HttpClient` and print the raw JSON response.

---

## **Step 4: Make Asynchronous HTTP Requests**
1. Learn how to use `HttpClient` for asynchronous operations:
   - Use `HttpClient.GetAsync` and `HttpClient.ReadAsStringAsync`.
2. Convert the code from Step 3 to use asynchronous methods.

**Example:**
```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        string apiUrl = "https://www.omdbapi.com/?apikey=e2fae6ec&s=batman&page=1";
        using HttpClient client = new HttpClient();

        Console.WriteLine("Fetching movie data...");
        string response = await client.GetStringAsync(apiUrl);
        Console.WriteLine(response);
    }
}
```

---

## **Step 5: Deserialize JSON Data**
1. Learn to use `System.Text.Json` or `Newtonsoft.Json` to parse JSON into C# objects.
2. Define a class structure matching the API response:
   ```csharp
   public class Movie
   {
       public string Title { get; set; }
       public string Year { get; set; }
       public string Poster { get; set; }
   }

   public class MovieResponse
   {
       public List<Movie> Search { get; set; }
   }
   ```

3. Deserialize the JSON data into C# objects asynchronously.

**Task:**
Update the code to parse the JSON and print a list of movie titles.

---

## **Step 6: Handle API Errors Gracefully**
1. Learn how to handle exceptions using `try-catch`.
2. Add error-handling logic for scenarios like:
   - Network errors.
   - API errors (e.g., invalid API key, no results).

**Example:**
```csharp
try
{
    string response = await client.GetStringAsync(apiUrl);
    var movies = JsonSerializer.Deserialize<MovieResponse>(response);
    foreach (var movie in movies.Search)
    {
        Console.WriteLine($"{movie.Title} ({movie.Year})");
    }
}
catch (Exception ex)
{
    Console.WriteLine($"An error occurred: {ex.Message}");
}
```

---

## **Step 7: Implement Pagination**
1. Study how the API supports pagination using the `page` parameter.
2. Write an asynchronous method to fetch movies from multiple pages.

**Task:**
Fetch movies from the first two pages and display their titles.

---

## **Step 8: Build a User Interface in the Console**
1. Create a simple text-based UI to interact with the user:
   - Display the list of movies.
   - Allow the user to input a keyword to search for movies.
   - Allow the user to select a movie and view details like the poster URL.

2. **Task**: Combine all functionality into a working console application:
   - Fetch movie data asynchronously.
   - Handle user inputs and display results dynamically.

---

## **Step 9: Optimize with Cancellation Tokens**
1. Learn how to use `CancellationToken` to cancel long-running requests.
2. Update your program to support user-triggered cancellation.

---

## **Final Step: Submit Your Application**
1. Ensure your code is clean and well-documented.
2. Share your project on GitHub or submit it as a ZIP file.

---

## **Sample Code Structure**
1. **Classes**:
   - `Movie`
   - `MovieResponse`
2. **Methods**:
   - `FetchMoviesAsync(string query, int page)`
   - `DisplayMovies(List<Movie> movies)`
   - `Run()` - main entry point for user interaction.

3. **Main Program**:
   ```csharp
   static async Task Main(string[] args)
   {
       await Run();
   }
   ```

This assignment will help you build foundational knowledge in asynchronous programming while creating a functional application.
