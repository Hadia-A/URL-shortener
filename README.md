# URL-shortener
 python based URL shortener
 pip install pyshorteners

import tkinter as tk
from tkinter import messagebox
import pyshorteners
import pyperclip

def shorten_url():
    long_url = entry.get()
    if not long_url:
        messagebox.showerror("Error", "Please enter a valid URL")
        return

    try:
        shortener = pyshorteners.Shortener()
        short_url = shortener.tinyurl.short(long_url)
        result_entry.config(state=tk.NORMAL)
        result_entry.delete(0, tk.END)
        result_entry.insert(0, short_url)
        result_entry.config(state=tk.DISABLED)
        copy_button.config(state=tk.NORMAL)
    except Exception as e:
        result_entry.config(state=tk.NORMAL)
        result_entry.delete(0, tk.END)
        result_entry.insert(0, f"Error: {e}")
        result_entry.config(state=tk.DISABLED)
        copy_button.config(state=tk.DISABLED)

def copy_to_clipboard():
    short_url = result_entry.get()
    if short_url:
        pyperclip.copy(short_url)
        messagebox.showinfo("Copied", "Shortened URL copied to clipboard!")

# Initialize the main window
root = tk.Tk()
root.title("URL Shortener")
root.geometry("500x250")
root.config(bg="#f4f4f4")

# URL Entry Label
label = tk.Label(root, text="Enter the URL to shorten:", font=("Arial", 14), bg="#f4f4f4")
label.pack(pady=10)

# URL Entry Field
entry = tk.Entry(root, width=50, font=("Arial", 12), bd=2, relief=tk.SUNKEN)
entry.pack(pady=5)

# Shorten Button
shorten_button = tk.Button(root, text="Shorten URL", command=shorten_url, font=("Arial", 12), bg="#007acc", fg="white", bd=0, relief=tk.FLAT)
shorten_button.pack(pady=10)

# Result Entry Field (disabled initially)
result_entry = tk.Entry(root, width=50, font=("Arial", 12), bd=2, relief=tk.SUNKEN, state=tk.DISABLED)
result_entry.pack(pady=5)

# Copy Button (disabled initially)
copy_button = tk.Button(root, text="Copy to Clipboard", command=copy_to_clipboard, font=("Arial", 12), bg="#4CAF50", fg="white", bd=0, relief=tk.FLAT, state=tk.DISABLED)
copy_button.pack(pady=10)

# Run the GUI loop
root.mainloop()
