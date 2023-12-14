# Eye reminder/Dry eyes
#The provided Python code is a simple desktop application designed to remind users to take breaks for eye care. It utilizes the plyer module for notifications, time for managing time intervals, and tkinter for the graphical user interface (GUI). The application prompts the user to input reminder times for blinking and eye drops in minutes, ensuring positive integer values. It then continuously runs a loop, triggering desktop notifications at specified intervals for both blink reminders and eye drop reminders. The GUI, created with Tkinter, includes input fields for reminder times, labels for guidance, and a button to set and activate the reminders. The code also customizes the window's dimensions, position, background color (pale green), and font (Arial, size 12).
#Reason: The eye was not created to be constantly focusing on close objects. If your occupation requires that you stare at a computer screen all day long or if you do a lot of reading, stop from time to time to do a few eye exercise.
# -*- coding: utf-8 -*-
"""
Created on Wed Dec 13 17:45:24 2023

@author: FARGOL
"""

from plyer import notification
import time
import tkinter as tk

def set_reminder():
    try:
        blink_time = int(blink_entry.get())
        drop_time = int(drop_entry.get())

        if blink_time <= 0 or drop_time <= 0:
            raise ValueError("Reminder times should be positive integers.")

        while True:
            time.sleep(blink_time * 60)  # Convert minutes to seconds
            show_notification("Blink Reminder", "Remember to blink for eye health!")

            time.sleep(drop_time * 60)  # Convert minutes to seconds
            show_notification("Eye Drop Reminder", "Time for eye drops!")

    except ValueError as e:
        print(f"Error: {e}")

def show_notification(title, message):
    notification.notify(
        title=title,
        message=message,
        app_icon=r"C:\Users\ff\Pictures\pic\a6fb9c6328d0b4d3dfe81492c905f3d5_w200.ico",  # Replace with the path to your icon file
    )

# GUI setup
root = tk.Tk()
root.title("Eye Reminders")

# Set window dimensions and position
root.geometry("400x300+300+200")

# Customize window background color
root.configure(bg="pale green")

# Customize font
custom_font = ("Arial", 12)

blink_label = tk.Label(root, text="Enter blink reminder time (minutes):", font=custom_font)
blink_label.pack()

blink_entry = tk.Entry(root, font=custom_font)
blink_entry.pack()

drop_label = tk.Label(root, text="Enter eye drop reminder time (minutes):", font=custom_font)
drop_label.pack()

drop_entry = tk.Entry(root, font=custom_font)
drop_entry.pack()

button = tk.Button(root, text="Set Reminders", command=set_reminder, font=custom_font, bg="#4CAF50", fg="white")
button.pack()

root.mainloop()
