# Weather Forecasting App

Welcome to the Weather Forecasting App! This application, developed using Python and an external API, provides detailed weather forecasts, including temperature, humidity, pressure, wind speed, weather index, latitude, longitude, and time. Additionally, it offers daily and nightly weather information for the entire week.

## Features

- **Current Weather Data**: Get real-time weather information.
- **Weekly Forecast**: View weather predictions for the next seven days.
- **Day and Night Weather**: Separate forecasts for day and night conditions.
- **Comprehensive Details**: Information includes temperature, humidity, pressure, wind speed, weather index, latitude, longitude, and time.

## Requirements

To run this project, you'll need to have Python installed on your machine. Additionally, you will need to install the following Python libraries:

- `requests`
- `datetime`
- `tkinter`
- `geopy`
- `timezonefinder`
- `pytz`
- `Pillow`

You can install these libraries using pip:

```bash
pip install requests datetime tkinter geopy timezonefinder pytz Pillow
```

## Getting Started

1. **Clone the repository**:

```bash
git clone https://github.com/GoKu21g/weather-forecasting-app.git
cd weather-forecasting-app
```

2. **Obtain API Key**: Sign up at a weather data provider (e.g., OpenWeatherMap) to get an API key.

3. **Configuration**: Create a configuration file or set up environment variables to store your API key.

4. **Run the Application**:

```bash
python weather_app.py
```

## Usage

Once the application is running, you can use it to get weather forecasts by entering the desired location. The application will fetch and display the current weather and the forecast for the next week.

## Code Overview

### `weather_app.py`

This is the main script of the application. It handles:

- Fetching weather data from the API
- Parsing and displaying the data
- Providing options to view current weather or weekly forecast

### `config.py`

This file contains the configuration settings, such as the API key and the base URL for the weather API.

## GUI Overview

The app utilizes `tkinter` for the graphical user interface. The following widgets are included:

- **Search Box**: Enter the city name to get weather information.
- **Labels**: Display temperature, humidity, pressure, wind speed, description, and time.
- **Frames**: Show daily weather information including day and night temperatures and icons.

```python
import tkinter as tk
from tkinter import *
from geopy.geocoders import Nominatim
from tkinter import ttk, messagebox
from timezonefinder import TimezoneFinder
from datetime import *
import requests
import pytz
from PIL import Image, ImageTk

root = tk.Tk()
root.title("WeatherApp")
root.geometry("890x470+300+300")
root.configure(bg="#57adff")
root.resizable(False, False)

def getWeather():
    city = textfield.get()
    geolocator = Nominatim(user_agent="geoapiExercises")
    location = geolocator.geocode(city)
    obj = TimezoneFinder()
    result = obj.timezone_at(lng=location.longitude, lat=location.latitude)
    timezone.config(text=result)
    long_lat.config(text=f"{round(location.latitude,4)}°N,{round(location.longitude),4}°E")
    home = pytz.timezone(result)
    local_time = datetime.now(home)
    current_time = local_time.strftime("%I:%M %p")
    clock.config(text=current_time)
    api = "https://api.openweathermap.org/data/2.5/onecall?lat=" + str(location.latitude) + "&lon=" + str(location.longitude) + "&units=metric&exclude=hourly&appid=YOUR_API_KEY"
    json_data = requests.get(api).json()
    temp = json_data['current']['temp']
    humidity = json_data['current']['humidity']
    pressure = json_data['current']['pressure']
    wind = json_data['current']['wind_speed']
    description = json_data['current']['weather'][0]['description']
    t.config(text=(temp,"°C"))
    h.config(text=(humidity,"%"))
    p.config(text=(pressure,"hPa"))
    w.config(text=(wind,"m/s"))
    d.config(text=(description))

    # Code for displaying daily weather cells and other details

root.mainloop()
```

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your improvements.

## Contact

For any questions or suggestions, please open an issue on GitHub or contact me at [GoKu21g](https://github.com/GoKu21g).

---

Thank you for using the Weather Forecasting App! We hope it provides you with accurate and helpful weather information.
