# Language-Translation-Tool
A Python language translation tool using Tkinter and Google Translate.

import tkinter as tk
from tkinter import ttk, messagebox
from deep_translator import GoogleTranslator

languages = {
    "English": "en",
    "Telugu": "te",
    "Hindi": "hi",
    "Tamil": "ta",
    "Kannada": "kn",
    "Malayalam": "ml",
    "French": "fr",
    "German": "de",
    "Spanish": "es"
}


def translate_text():
    text = input_text.get("1.0", tk.END).strip()

    if not text:
        messagebox.showwarning(
            "Warning",
            "Please enter some text."
        )
        return

    source = languages[source_combo.get()]
    target = languages[target_combo.get()]

    try:
        translator = GoogleTranslator(
            source=source,
            target=target
        )

        result = translator.translate(text)

        output_text.delete("1.0", tk.END)
        output_text.insert(tk.END, result)

    except Exception as e:
        messagebox.showerror("Error", str(e))


def copy_text():
    result = output_text.get("1.0", tk.END).strip()

    if result:
        root.clipboard_clear()
        root.clipboard_append(result)
        messagebox.showinfo(
            "Copied",
            "Translation copied!"
        )


root = tk.Tk()
root.title("Language Translation Tool")
root.geometry("600x500")


title = tk.Label(
    root,
    text="Language Translation Tool",
    font=("Arial", 20, "bold")
)

title.pack(pady=15)


# Source language
tk.Label(
    root,
    text="Source Language"
).pack()

source_combo = ttk.Combobox(
    root,
    values=list(languages.keys()),
    state="readonly"
)

source_combo.set("English")
source_combo.pack(pady=5)


# Target language
tk.Label(
    root,
    text="Target Language"
).pack()

target_combo = ttk.Combobox(
    root,
    values=list(languages.keys()),
    state="readonly"
)

target_combo.set("Telugu")
target_combo.pack(pady=5)


# Input
tk.Label(
    root,
    text="Enter Text"
).pack()

input_text = tk.Text(
    root,
    height=7,
    width=60
)

input_text.pack(pady=5)


# Translate button
translate_button = tk.Button(
    root,
    text="Translate",
    command=translate_text,
    font=("Arial", 12, "bold")
)

translate_button.pack(pady=10)


# Output
tk.Label(
    root,
    text="Translated Text"
).pack()

output_text = tk.Text(
    root,
    height=7,
    width=60
)

output_text.pack(pady=5)


# Copy button
copy_button = tk.Button(
    root,
    text="Copy Translation",
    command=copy_text
)

copy_button.pack(pady=10)


root.mainloop()
