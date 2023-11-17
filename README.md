# weather-project
import requests
import tkinter as tk
import ttkbootstrap as ttk

# api


# function to prompt user and display on app
def get_weather():
# api key and url + user input
    api_key = "507bd791486bae1554aba821a54fbaa8"
    api_url = "https://api.openweathermap.org/data/2.5/weather"
    city = city_input.get()



# url str formating


    response = requests.get(
        url=api_url,
        params={
            "q": city,
            "appid": api_key,

        }
    )
    try:
        weather_data = response.json()
        weather = weather_data["weather"][0]["description"]
        temperature = (weather_data["main"]["temp"] - 273.15) * 1.8 + 32
        roundedTemp = round(temperature)
        output_str.set("It is "+str(roundedTemp)+" with "+ weather+"!")
    except:
        output_str.set("Enter a valid location.")

# window
window = ttk.Window(themename = "journal")
window.title("Weather")
window.geometry("500x250")

# title
title_label = ttk.Label(
    master=window,
    text="Enter Your City!",
    font="Calibri 20 bold")
title_label.pack()

# input
city_input_frame = ttk.Frame(master=window)
inputStr = tk.StringVar
city_input = ttk.Entry(
    master=city_input_frame,
    textvariable=inputStr)

button = ttk.Button(
    master=city_input_frame,
    text="Enter",
    command= get_weather)

city_input.pack(side="left", padx = 10)
button.pack(side= "left")
city_input_frame.pack(pady = 10)

# output
output_str = tk.StringVar()
output_label = ttk.Label(
    master = window,
    text = "Output",
    font="Calibri 20 bold",
    textvariable= output_str)
output_label.pack(pady= 5)




window.mainloop()
