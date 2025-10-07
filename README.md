## API Overview

This API provides access to a wide range of movie and TV show data, including details about titles, series, episodes, ratings, and actors. It allows you to search for titles using various methods, such as by name, keyword, or IMDb ID. You can also explore upcoming releases, retrieve lists of genres, get random titles or actors, and view detailed season information for series. Additionally, the API includes utility endpoints for structured data like genres and title types, making it easy to build powerful entertainment-based applications.

## Version

**Version:** 1.0



## Available Endpoints

Below is a list of the main API endpoints and their descriptions:

### 🎬 **Titles**
- **GET `/titles`** – Retrieve a list of all titles (movies, series, etc.).
- **GET `/titles/{id}`** – Get detailed information about a specific title by its ID.
- **GET `/titles/random`** – Fetch a random title.
- **GET `/titles/{id}/aka`** – Get alternate titles (AKAs) for a specific title.
- **GET `/titles/{id}/ratings`** – Retrieve ratings for a specific title.
- **GET `/titles/series/{seriesId}`** – Get details about a series.
- **GET `/titles/series/{seriesId}/{season}`** – Retrieve details for a specific season in a series.
- **GET `/titles/seasons/{seriesId}`** – Get a list of all seasons for a series.
- **GET `/titles/episode/{id}`** – Retrieve information about a specific episode.
- **GET `/titles/x/upcoming`** – Get a list of upcoming titles.
- **GET `/titles/x/titles-by-ids`** – Fetch multiple titles by their IDs.

### 🔍 **Search**
- **GET `/titles/search/title/{title}`** – Search for titles by title name.
- **GET `/titles/search/keyword/{keyword}`** – Search titles by keyword.
- **GET `/titles/search/akas/{aka}`** – Search for titles by their alternate names.
- **GET `/titles/search/{imdbId}`** – Search by IMDb ID.

### 🧍 **Actors**
- **GET `/actors`** – Retrieve a list of actors.
- **GET `/actors/{id}`** – Get detailed information about a specific actor.
- **GET `/actors/random`** – Fetch a random actor.

### 🛠 **Utils**
- **GET `/titles/utils/genres`** – Retrieve a list of available genres.
- **GET `/titles/utils/lists`** – Retrieve predefined title lists.
- **GET `/titles/utils/titleTypes`** – Get available title types (e.g., movie, TV series, etc.).

### 📝 **Obsolete**
> These endpoints are marked as obsolete and may be removed in future versions.
- **GET `/titles/{id}/crew`** – Get crew information for a title.
- **GET `/titles/{id}/main_actors`** – Get the main actors of a title.


## Request and Response Format

The API follows a **RESTful** structure using standard HTTP methods. All responses are returned in **JSON** format.

### 📥 **Request Format**

Typical requests are sent using standard HTTP GET methods. Parameters such as `page`, `title`, or `id` can be passed as part of the URL path or as query parameters.

**Example Request:**  
```http

```http
GET /titles/search/title/Inception?page=1
```



## Authentication

All API requests require **authentication** using an **API key**. You must include this key in the request headers to access any of the endpoints.

### 🔑 How It Works

Authentication is handled through **RapidAPI**. Each request must include the following headers:

- `x-rapidapi-key`: Your unique API key provided by RapidAPI.  
- `x-rapidapi-host`: The host name of the API (`moviesdatabase.p.rapidapi.com`).

### 🧠 Example Using Axios (JavaScript)

```javascript
import axios from 'axios';

const options = {
  method: 'GET',
  url: 'https://moviesdatabase.p.rapidapi.com/titles/x/upcoming',
  headers: {
    'x-rapidapi-key': 'YOUR_API_KEY_HERE',
    'x-rapidapi-host': 'moviesdatabase.p.rapidapi.com'
  }
};

async function fetchUpcomingTitles() {
  try {
    const response = await axios.request(options);
    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
}

fetchUpcomingTitles();


## Error Handling

When interacting with the API, you may encounter different types of errors. Common error responses include:

| Status Code | Meaning                          | Description                                                                 |
|-------------|-----------------------------------|-----------------------------------------------------------------------------|
| 400         | Bad Request                      | The request is malformed or missing required parameters.                   |
| 401         | Unauthorized                     | Authentication failed — usually due to an invalid or missing API key.      |
| 403         | Forbidden                        | You don’t have permission to access the requested resource.                |
| 404         | Not Found                        | The requested resource or endpoint does not exist.                         |
| 429         | Too Many Requests (Rate Limit)   | You have exceeded the allowed number of requests within a given time.     |
| 500+        | Server Error                     | Something went wrong on the API’s side. Try again later.                   |

### 🧠 Example: Handling Errors with Axios

```javascript
import axios from 'axios';

async function fetchData() {
  try {
    const response = await axios.get('https://moviesdatabase.p.rapidapi.com/titles/random', {
      headers: {
        'x-rapidapi-key': process.env.RAPIDAPI_KEY,
        'x-rapidapi-host': 'moviesdatabase.p.rapidapi.com'
      }
    });
    console.log(response.data);
  } catch (error) {
    if (error.response) {
      console.error('Error Status:', error.response.status);
      console.error('Error Message:', error.response.data);
    } else {
      console.error('Network Error:', error.message);
    }
  }
}

fetchData();
