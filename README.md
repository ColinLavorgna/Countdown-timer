# Countdown-timer
# Before trying to run code, make sure you are running it on python.11
# If start button does not return, restart the code. 
>>> import tkinter as tk
>>> from tkinter import messagebox
>>> import time
>>> import os
>>>
>>> # Dictionary to map word input to numbers
>>> word_to_number = {
...     "zero": 0, "one": 1, "two": 2, "three": 3, "four": 4,
...     "five": 5, "six": 6, "seven": 7, "eight": 8, "nine": 9,
...     "ten": 10, "eleven": 11, "twelve": 12, "thirteen": 13,
...     "fourteen": 14, "fifteen": 15, "sixteen": 16, "seventeen": 17,
...     "eighteen": 18, "nineteen": 19, "twenty": 20, "thirty": 30,
...     "forty": 40, "fifty": 50, "sixty": 60, "seventy": 70,
...     "eighty": 80, "ninety": 90
... }
>>>
>>> # Function to convert words to numbers
>>> def convert_to_number(word):
...     word = word.lower().strip()
...     if word.isdigit():
...         return int(word)  # If it's already a digit, return it as integer
...     elif word in word_to_number:
...         return word_to_number[word]  # Convert valid word to number
...     else:
...         return None  # Invalid word
...
>>> # Function to start the countdown
>>> def start_countdown():
...     try:
...         # Get the user input for days, hours, minutes, and seconds (as words or numbers)
...         days = convert_to_number(entry_days.get())
...         hours = convert_to_number(entry_hours.get())
...         minutes = convert_to_number(entry_minutes.get())
...         seconds = convert_to_number(entry_seconds.get())
...
...         # Check if any input is invalid
...         if None in (days, hours, minutes, seconds):
...             raise ValueError("Please enter valid numbers or recognized words (e.g., 'three').")
...
...         # Convert the time to total seconds
...         countdown_time = days * 86400 + hours * 3600 + minutes * 60 + seconds
...
...         if countdown_time <= 0:
...             raise ValueError("Please enter a positive time.")
...     except ValueError as e:
...         messagebox.showerror("Invalid Input", f"Invalid input: {e}")
...         return
...
...     # Disable the start button to prevent multiple starts
...     start_button.config(state="disabled")
...
...     while countdown_time >= 0:
...         d, rem = divmod(countdown_time, 86400)  # Days
...         h, rem = divmod(rem, 3600)  # Hours
...         m, s = divmod(rem, 60)  # Minutes and Seconds
...
...         # Format the remaining time in DD:HH:MM:SS
...         time_left = f"{d:02}:{h:02}:{m:02}:{s:02}"
...         time_display.config(text=time_left)
...
...         window.update()  # Update the UI
...
...         # Pause for 1 second
...         time.sleep(1)
...         countdown_time -= 1
...
>>>     # Final message when the countdown hits zero
>>>     messagebox.showinfo("Time's Up!", "The countdown has finished! Time's up!")
  File "<stdin>", line 1
    messagebox.showinfo("Time's Up!", "The countdown has finished! Time's up!")
IndentationError: unexpected indent
>>>
>>>     # Re-enable the start button
>>>     start_button.config(state="normal")
  File "<stdin>", line 1
    start_button.config(state="normal")
IndentationError: unexpected indent
>>>     time_display.config(text="00:00:00:00")  # Reset the time display
  File "<stdin>", line 1
    time_display.config(text="00:00:00:00")  # Reset the time display
IndentationError: unexpected indent
>>>
>>> # Function to save the current countdown settings to a file
>>> def save_settings():
...     try:
...         with open('countdown_settings.txt', 'w') as file:
...             file.write(f"{entry_days.get()}\n")
...             file.write(f"{entry_hours.get()}\n")
...             file.write(f"{entry_minutes.get()}\n")
...             file.write(f"{entry_seconds.get()}\n")
...         messagebox.showinfo("Saved", "Countdown settings have been saved successfully.")
...     except Exception as e:
...         messagebox.showerror("Error", f"An error occurred while saving settings: {e}")
...
>>> # Function to load countdown settings from a file
>>> def load_settings():
...     if os.path.exists('countdown_settings.txt'):
...         try:
...             with open('countdown_settings.txt', 'r') as file:
...                 days = file.readline().strip()
...                 hours = file.readline().strip()
...                 minutes = file.readline().strip()
...                 seconds = file.readline().strip()
...
  File "<stdin>", line 9

SyntaxError: expected 'except' or 'finally' block
>>>                 # Update the entry fields with loaded values
>>>                 entry_days.delete(0, tk.END)
  File "<stdin>", line 1
    entry_days.delete(0, tk.END)
IndentationError: unexpected indent
>>>                 entry_hours.delete(0, tk.END)
  File "<stdin>", line 1
    entry_hours.delete(0, tk.END)
IndentationError: unexpected indent
>>>                 entry_minutes.delete(0, tk.END)
  File "<stdin>", line 1
    entry_minutes.delete(0, tk.END)
IndentationError: unexpected indent
>>>                 entry_seconds.delete(0, tk.END)
  File "<stdin>", line 1
    entry_seconds.delete(0, tk.END)
IndentationError: unexpected indent
>>>
>>>                 entry_days.insert(0, days)
  File "<stdin>", line 1
    entry_days.insert(0, days)
IndentationError: unexpected indent
>>>                 entry_hours.insert(0, hours)
  File "<stdin>", line 1
    entry_hours.insert(0, hours)
IndentationError: unexpected indent
>>>                 entry_minutes.insert(0, minutes)
  File "<stdin>", line 1
    entry_minutes.insert(0, minutes)
IndentationError: unexpected indent
>>>                 entry_seconds.insert(0, seconds)
  File "<stdin>", line 1
    entry_seconds.insert(0, seconds)
IndentationError: unexpected indent
>>>
>>>             messagebox.showinfo("Loaded", "Countdown settings have been loaded successfully.")
  File "<stdin>", line 1
    messagebox.showinfo("Loaded", "Countdown settings have been loaded successfully.")
IndentationError: unexpected indent
>>>         except Exception as e:
  File "<stdin>", line 1
    except Exception as e:
IndentationError: unexpected indent
>>>             messagebox.showerror("Error", f"An error occurred while loading settings: {e}")
  File "<stdin>", line 1
    messagebox.showerror("Error", f"An error occurred while loading settings: {e}")
IndentationError: unexpected indent
>>>     else:
  File "<stdin>", line 1
    else:
IndentationError: unexpected indent
>>>         messagebox.showwarning("File Not Found", "No saved countdown settings found.")
  File "<stdin>", line 1
    messagebox.showwarning("File Not Found", "No saved countdown settings found.")
IndentationError: unexpected indent
>>>
>>> # Create the main window
>>> window = tk.Tk()
>>> window.title("Countdown Timer")
''
>>>
>>> # Create the label for days input
>>> label_days = tk.Label(window, text="Enter days:")
>>> label_days.pack(pady=5)
>>>
>>> # Create the entry field for days input
>>> entry_days = tk.Entry(window, font=("Helvetica", 14))
>>> entry_days.pack(pady=5)
>>>
>>> # Create the label for hours input
>>> label_hours = tk.Label(window, text="Enter hours:")
>>> label_hours.pack(pady=5)
>>>
>>> # Create the entry field for hours input
>>> entry_hours = tk.Entry(window, font=("Helvetica", 14))
>>> entry_hours.pack(pady=5)
>>>
>>> # Create the label for minutes input
>>> label_minutes = tk.Label(window, text="Enter minutes:")
>>> label_minutes.pack(pady=5)
>>>
>>> # Create the entry field for minutes input
>>> entry_minutes = tk.Entry(window, font=("Helvetica", 14))
>>> entry_minutes.pack(pady=5)
>>>
>>> # Create the label for seconds input
>>> label_seconds = tk.Label(window, text="Enter seconds:")
>>> label_seconds.pack(pady=5)
>>>
>>> # Create the entry field for seconds input
>>> entry_seconds = tk.Entry(window, font=("Helvetica", 14))
>>> entry_seconds.pack(pady=5)
>>>
>>> # Create the start button to begin countdown
>>> start_button = tk.Button(window, text="Start Countdown", font=("Helvetica", 14), command=start_countdown)
>>> start_button.pack(pady=10)
>>>
>>> # Create buttons for saving and loading settings
>>> save_button = tk.Button(window, text="Save Settings", font=("Helvetica", 14), command=save_settings)
>>> save_button.pack(pady=5)
>>>
>>> load_button = tk.Button(window, text="Load Settings", font=("Helvetica", 14), command=load_settings)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'load_settings' is not defined. Did you mean: 'save_settings'?
>>> load_button.pack(pady=5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'load_button' is not defined. Did you mean: 'start_button'?
>>>
>>> # Create a label to display the countdown time
>>> time_display = tk.Label(window, text="00:00:00:00", font=("Helvetica", 48), fg="red")
>>> time_display.pack(pady=20)
>>>
>>> # Run the main event loop
>>> window.mainloop()
>>>
