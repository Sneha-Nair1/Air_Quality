# Air_Quality
import requests

API_KEY = 'e2c40c0ac1f95e386b6389e6965ff327'

city = input('Enter city name: ')

# Get weather data
weather_url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}'
weather_data = requests.get(weather_url).json()

temp = weather_data['main']['temp']
desc = weather_data['weather'][0]['description']

print(f'Temperature: {temp} K')
print(f'Description: {desc}')

# Get coordinates for air quality
lat = weather_data['coord']['lat']
lon = weather_data['coord']['lon']

# Get air quality data
air_quality_url = f'http://api.openweathermap.org/data/2.5/air_pollution?lat={lat}&lon={lon}&appid={API_KEY}'
air_quality_data = requests.get(air_quality_url).json()

aqi = air_quality_data['list'][0]['main']['aqi']
print(f'Air Quality Index: {aqi}')

if 'pm10' in air_quality_data['list'][0]['components']:
    pm10 = air_quality_data['list'][0]['components']['pm10']
    print(f'PM 10: {pm10} μg/m3')

# Print other pollutants similarly
