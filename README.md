# ccsu_mobile_app.py
import tkinter as tk
from PIL import ImageTk, Image
import pandas as pd
import os

#window setup
root = tk.Tk()
root.title('CCSU Mobile App')
root.geometry("600x600")
root.resizable(0, 0)
root.configure(bg='light blue')

#logo
logo_path = '/Users/abe/Downloads/logo1.png'

if os.path.exists(logo_path):
    img = Image.open(logo_path)
    try:
        img = img.resize((100, 100), Image.Resampling.LANCZOS)
    except AttributeError:
        img = img.resize((100, 100), Image.ANTIALIAS)

    img = img.convert("RGBA")
    data_img = img.getdata()
    newData = []
    for item in data_img:
        if item[:3] == (255, 255, 255):
            newData.append((255, 255, 255, 0))
        else:
            newData.append(item)
    img.putdata(newData)
    logo = ImageTk.PhotoImage(img)
    logo_label = tk.Label(root, image=logo, bg='light blue')
    logo_label.pack(pady=10)
else:
    logo_label = tk.Label(root, text="Logo not found!", bg='light blue', fg='white', font=("Arial", 12, "bold"))
    logo_label.pack(pady=10)


#csv data
csv_path = '/Users/abe/Downloads/midterm_exam.csv'
if os.path.exists(csv_path):
    data = pd.read_csv(csv_path)
else:
    data = pd.DataFrame()

#button packing
button_frame = tk.Frame(root, bg='light blue')
button_frame.pack(pady=10)

#output
output_label = tk.Label(root, justify="center", bg="light blue", anchor="center")
output_label.pack(side="bottom", pady=20, fill="both", expand=True)

#button functions
def show_calendar():
    if 'CalendarDate' in data.columns:
        df = data[['CalendarDate']].dropna()
        output_label.config(text=df.to_string(index=False))
    else:
        output_label.config(text="Calendar data not found!")

def show_buildings():
    if 'Buildings' in data.columns:
        df = data[['Buildings']].dropna()
        output_label.config(text=df.to_string(index=False))
    else:
        output_label.config(text="Buildings data not found!")

def show_faculty():
    if 'FacultyName' in data.columns:
        df = data[['FacultyName']].dropna()
        output_label.config(text=df.to_string(index=False))
    else:
        output_label.config(text="Faculty data not found!")


#buttons
button_calendar = tk.Button(button_frame, text="Calendar", command=show_calendar, bg="light green", activebackground="light green")
button_calendar.pack(side="left", padx=10)

button_buildings = tk.Button(button_frame, text="Buildings", command=show_buildings, bg="light green", activebackground="light green")
button_buildings.pack(side="left", padx=10)

button_faculty = tk.Button(button_frame, text="Faculty", command=show_faculty, bg="light green", activebackground="light green")
button_faculty.pack(side="left", padx=10)

root.mainloop()
