import datetime
import tkinter as tk
from PIL import Image, ImageTk

window = tk.Tk()
window.geometry("600x700")  # Corrected geometry format for width and height
window.title("Age Calculator App")

name = tk.Label(text="Name")
name.grid(column=0, row=1)
year = tk.Label(text="Year")
year.grid(column=0, row=2)
month = tk.Label(text="Month")
month.grid(column=0, row=3)
day = tk.Label(text="Day")
day.grid(column=0, row=4)

nameEntry = tk.Entry()
nameEntry.grid(column=1, row=1)
yearEntry = tk.Entry()
yearEntry.grid(column=1, row=2)
monthEntry = tk.Entry()
monthEntry.grid(column=1, row=3)
dayEntry = tk.Entry()
dayEntry.grid(column=1, row=4)

def get_input():  # Corrected function name with snake_case convention
    name = nameEntry.get()
    try:
        # Improved error handling for invalid date input
        birth_date = datetime.date(int(yearEntry.get()), int(monthEntry.get()), int(dayEntry.get()))
        monkey = Person(name, birth_date)
        text_area = tk.Text(master=window, height=10, width=25)
        text_area.grid(column=1, row=6)
        answer = f"Hey {monkey.name}!!! You are {monkey.age()} years old!!!."
        text_area.insert(tk.END, answer)
    except ValueError:
        text_area = tk.Text(master=window, height=1, width=25, bg="red")  # Error message area
        text_area.grid(column=1, row=6)
        text_area.insert(tk.END, "Invalid date format. Please enter numbers only.")

button = tk.Button(window, text="Calculate Age", command=get_input, bg="pink")
button.grid(column=1, row=5)

class Person:
    def __init__(self, name, birthdate):
        self.name = name
        self.birthdate = birthdate

    def age(self):
        today = datetime.date.today()
        age = today.year - self.birthdate.year
        # Check for negative age due to future birthdates
        if age < 0:
            return 0  # Handle future birthdates by returning 0 age
        else:
            return age

image = Image.open('C:\\Users\\DELL\\Downloads\\WhatsApp Image 2024-08-07 at 00.48.16.jpeg')  # Assuming the image file exists
image.thumbnail((300, 300), Image.LANCZOS)
photo = ImageTk.PhotoImage(image)
label_image = tk.Label(image=photo)
label_image.grid(column=1, row=0)

window.mainloop()
# age-calculator
