# Weather Application

## Overview
This project is a weather application built using Vue.js. It allows users to search for weather information for a specific city. The application fetches data from the OpenWeatherMap API and displays the current weather conditions as well as the forecast for the upcoming days.

## Features
- Search for weather information by city name.
- Display current weather conditions including temperature, description, wind speed, humidity, sea level, and country.
- Display weather forecast for the upcoming days.
- Responsive design for different screen sizes.

## Components
1. **App.vue:**
   - Main component containing the header section with a search bar.
   - Imports the Weather component to display weather information.
   - Handles user input for city search and error messages.

2. **Weather.vue:**
   - Displays current weather information for the specified city.
   - Makes API calls to fetch weather data and displays it.
   - Includes a button to change the location.

3. **DaysWeather.vue:**
   - Displays weather forecast for the upcoming days.
   - Makes API calls to fetch forecast data and displays it.

## Installation
1. Clone the repository: `git clone https://github.com/your/repository.git`
2. Install dependencies: `npm install`
3. Run the application: `npm run serve`
4. Access the application in your browser: `http://localhost:8080`

## Usage
1. Enter a city name in the search bar.
2. Click the search button to fetch weather information.
3. View current weather conditions and forecast.

## Technologies Used
- Vue.js
- Bootstrap
- Axios (for API requests)
- Moment.js (for date formatting)

## Credits
- This project utilizes the OpenWeatherMap API for weather data.
- Icons provided by Font Awesome.
