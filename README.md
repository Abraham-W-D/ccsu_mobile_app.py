CCSU Mobile App (Python & Tkinter)

This project is a desktop-based simulation of a mobile application interface built using Python’s tkinter library. The application loads a CCSU logo image, reads data from a CSV file, and allows users to view selected information—such as the academic calendar, campus buildings, and faculty names—through interactive buttons.

Overview:
The application demonstrates how to integrate graphical elements, external images, and CSV data into a Python GUI. When launched, the interface displays a logo at the top, three buttons for navigating different datasets, and an output area where the selected information is shown.

Features:
-Graphical interface built with tkinter
-Ability to load and display a transparent CCSU logo
-CSV data reading using pandas

Buttons that display:
-Calendar dates
-Campus building names
-Faculty names
-Automatic handling of missing files or missing columns

How the Program Works:

Image Handling:
The app attempts to load a logo from the provided file path. If found, it resizes the image and removes white backgrounds to allow for seamless blending with the GUI’s light-blue background. If the file is missing, a fallback text label is shown.

CSV Data:
The application loads data from midterm_exam.csv. Each button displays one column from the CSV if it exists.

Button Functions:
-show_calendar(): Displays all calendar dates from the CSV
-show_buildings(): Displays all campus buildings
-show_faculty(): Displays all faculty names

Each function checks whether the required column exists and updates the output label accordingly.

