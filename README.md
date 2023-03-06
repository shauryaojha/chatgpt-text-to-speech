import tkinter as tk
from tkinter import messagebox
import openai
import os
from gtts import gTTS

# Apply your API key
openai.api_key = input("enter your api key")

def generate_response(prompt):
    response = openai.Completion.create(
        engine="text-davinci-002",
        prompt=prompt,
        max_tokens=1024
    )
    return response['choices'][0]['text']

def generate_response_with_voice(prompt):
    response = generate_response(prompt)
    print(response)
    tts = gTTS(response)
    tts.save("response.mp3")
    os.system("start response.mp3")

def on_submit():
    prompt = entry.get()
    if prompt == "":
        messagebox.showerror("Error", "Please enter a prompt")

    else:

        generate_response_with_voice(prompt)

# Create a new Tkinter window
root = tk.Tk()
root.geometry("400x200")
root.title("ChatGPT UI")

# Create a label and an entry widget
label = tk.Label(root, text="Enter your prompt:")
label.pack()
entry = tk.Entry(root)
entry.pack()

# Create a submit button
submit = tk.Button(root, text="Submit", command=on_submit)
submit.pack()

# Start the main loop
root.mainloop()
