import requests

# Replace with your OpenWeatherMap API key
API_KEY = 'your_api_key_here'

def get_weather(city):
    url = f'http://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric'
    response = requests.get(url)
    
    if response.status_code == 200:
        weather_data = response.json()
        return weather_data
    else:
        return None

def display_weather(weather_data):
    if weather_data:
        print(f"Weather in {weather_data['name']}, {weather_data['sys']['country']}:")
        print(f"Temperature: {weather_data['main']['temp']}°C")
        print(f"Humidity: {weather_data['main']['humidity']}%")
        print(f"Wind Speed: {weather_data['wind']['speed']} m/s")
        print(f"Description: {weather_data['weather'][0]['description']}")
    else:
        print("City not found or API request failed.")

def main():
    city = input("Enter the name of the city: ")
    weather_data = get_weather(city)
    display_weather(weather_data)

if __name__ == "__main__":
    main()
