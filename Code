from tkinter import *
from tkinter import ttk, messagebox
from googletrans import Translator, LANGUAGES
from gtts import gTTS
import os
import pygame

def change(text="type", src="English", dest="Hindi"):
    text1 = text
    src1 = src
    dest1 = dest
    trans = Translator()
    try:
        # Try to get the translation
        trans1 = trans.translate(text, src=src1, dest=dest1)
    except Exception as e:
        # Handle any errors during translation (e.g., network issues, API issues)
        print(f"Error during translation: {e}")
        trans1 = text
    return trans1.text

def text_to_speech(textget, language='en', output_file='output.mp3'):
    # Create a gTTS object
    try:
        tts = gTTS(textget, lang=language, slow=False)
        # Save the speech as an MP3 file
        tts.save(output_file)
    except PermissionError as pe:
        print(f"PermissionError: {pe}")
        print("Check file permissions and try again.")
    except Exception as e:
        print(f"Error during text-to-speech conversion: {e}")

def play_audio(output_file):
    import pygame
    import os

def play_audio(output_file):
    pygame.init()
    pygame.mixer.init()
    pygame.mixer.music.load('output.mp3')
    pygame.mixer.music.play()
    while pygame.mixer.music.get_busy():
        pygame.time.Clock().tick(10)
    pygame.mixer.quit()
    os.remove('output.mp3')

# ...

def data():
    # ...
    textget = change(msg, s, d)
    tts = gTTS(textget, lang=d, slow=False)
    tts.save('output.mp3')
    play_audio('output.mp3')
    ask_to_use_again()

import pygame
pygame.mixer.init()
def stop_audio():
    try:
        pygame.mixer.music.stop()
    except ImportError:
        print("Please install pygame to enable audio playback.")

def ask_to_use_again():
    # Show a message box asking if the user wants to use the companion again
    response = messagebox.askyesno("Use Your Companion Again", "Do you want to use your companion again?")
    if response:
        # If "Yes", clear the destination text and reset the source text box
        dest_txt.delete(1.0, END)
        Sor_txt.delete(1.0, END)
        # Stop any ongoing audio playback
        stop_audio()
        # Optionally, delete or overwrite the audio file
        if os.path.exists('output.mp3'):
            os.remove('output.mp3')
    else:
        # If "No", close the application
        root.destroy()

def data():
    s = comb_sor.get()
    d = comb_des.get()
    msg = Sor_txt.get(1.0, END).strip()
    textget = change(msg, s, d)
    dest_txt.delete(1.0, END)
    dest_txt.insert(END, textget)
    text_to_speech(textget, output_file='output.mp3')
    play_audio(output_file='output.mp3')
    ask_to_use_again()

root = Tk()
root.title("Translator")
root.geometry("600x800")
root.config(bg='#f0f8ff')  # Light AliceBlue background

# Title Label
lab_txt = Label(root, text="Translator", font=("Helvetica", 36, "bold"), bg='#f0f8ff', fg='#4682b4')
lab_txt.pack(pady=20)

# Main Frame
frame = Frame(root, bg='#f0f8ff')
frame.pack(padx=20, pady=10, fill=BOTH, expand=True)

# Source Text
lab_src = Label(frame, text="Source Text", font=("Helvetica", 18, "bold"), bg='#f0f8ff', fg='#333333')
lab_src.grid(row=0, column=0, columnspan=2, pady=10, sticky=W)
Sor_txt = Text(frame, font=("Helvetica", 14), wrap=WORD, height=6, width=50)
Sor_txt.grid(row=1, column=0, columnspan=2, pady=5, padx=5)

# Source Language ComboBox
comb_sor = ttk.Combobox(frame, values=list(LANGUAGES.values()), font=("Helvetica", 14))
comb_sor.grid(row=2, column=0, pady=10, padx=5, sticky=W)
comb_sor.set("English")

# Destination Language ComboBox
comb_des = ttk.Combobox(frame, values=list(LANGUAGES.values()), font=("Helvetica", 14))
comb_des.grid(row=2, column=1, pady=10, padx=5, sticky=E)
comb_des.set("Hindi")

# Destination Text
lab_dest = Label(frame, text="Destination Text", font=("Helvetica", 18, "bold"), bg='#f0f8ff', fg='#333333')
lab_dest.grid(row=3, column=0, columnspan=2, pady=10, sticky=W)
dest_txt = Text(frame, font=("Helvetica", 14), wrap=WORD, height=6, width=50)
dest_txt.grid(row=4, column=0, columnspan=2, pady=5, padx=5)

# Translate and Speak Button
button_translate_speak = Button(frame, text="Translate and Speak", font=("Helvetica", 16, "bold"), relief=RAISED, command=data, bg='#4682b4', fg='white')
button_translate_speak.grid(row=5, column=0, columnspan=2, pady=20)

root.mainloop()
