from tkinter import messagebox
import tkinter as tk
from PyDictionary import PyDictionary
from PIL import ImageTk,Image


# GUI Application class
class DictionaryLookup:
    def __init__(self):
        self.dictionary = PyDictionary()

    def get_word_meaning(self, word):
        # Return the meaning of the word or None if no meaning found
        return self.dictionary.meaning(word)


class DictionaryApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Words Defined")
        self.root.geometry("500x500")

        self.dictionary_lookup = DictionaryLookup()  # Initialize the dictionary lookup
        self.gui_setup()


    def gui_setup(self):

        # Load the image and add it to the top of the window
        self.logo_image = Image.open("mainimage.jpg")  # Replace with your image file path
        self.logo_image = self.logo_image.resize((100, 100))  # Resize as needed
        self.logo_photo = ImageTk.PhotoImage(self.logo_image)

        self.logo_label = tk.Label(self.root, image=self.logo_photo)
        self.logo_label.pack(pady=10)  # Adjust padding as needed


        # Title Label
        self.my_title = tk.Label(self.root, text="Words Defined: An English Dictionary", font=("Times", 25, "bold"), bg="skyblue")
        self.my_title.pack()


        # Word input widget
        self.word_entry = tk.Entry(self.root, width=50, borderwidth=5)
        self.word_entry.pack(pady=20)

        # Button to search for the word
        self.search_button = tk.Button(self.root, text="Search Word", command=self.get_meaning_callback, padx=20, pady=20, bg="white")
        self.search_button.pack()

        # Button to clear word
        self.clear_button = tk.Button(self.root, text="Clear", command=self.clear_callback, padx=20, pady=20, bg="white")
        self.clear_button.pack()

        # Button to exit the program
        self.exit_button = tk.Button(self.root, text="Exit", padx=20, pady=20, bg="white", command=self.root.destroy)
        self.exit_button.pack()


    def get_meaning_callback(self):
        word = self.word_entry.get().strip()

        # Input validation: non-empty and alphabetic
        if not word:
            messagebox.showwarning("Input Error", "Please enter a word.")
            return
        if not word.isalpha():
            messagebox.showwarning("Input Error", "Only alphabetic characters are allowed.")
            return

        # Fetch the meaning
        meaning = self.dictionary_lookup.get_word_meaning(word)  # Use dictionary_lookup instance
        if meaning:
            result = f"Meaning of '{word}':\n\n"
            for pos, definitions in meaning.items():
                result += f"{pos}:\n"
                for definition in definitions:
                    result += f"- {definition}\n"
            self.display_definition(result)
        else:
            messagebox.showerror("Error", f"No definition found for '{word}'.")

    def display_definition(self, definition):
        # Open a new window to display the definition
        self.window2 = tk.Toplevel(self.root)
        self.window2.title("Definition")
        self.window2.geometry("400x300")

        # Load the image and add it to the window
        self.definition_image = Image.open("Define.jpg")  # Replace with your image file path
        self.definition_image = self.definition_image.resize((100,100))  # Resize as needed
        self.definition_photo = ImageTk.PhotoImage(self.definition_image)

        self.image_label = tk.Label(self.window2, image=self.definition_photo)
        self.image_label.pack(pady=10)  # Adjust padding as needed



        def_label = tk.Label(self.window2, text="Definition:", font=("Times", 20, "bold"), bg="skyblue")
        def_label.pack(pady=10)

        # Create a text widget to display the definition
        result_text = tk.Text(self.window2, wrap="word", height=10, width=50)
        result_text.pack(pady=20)
        result_text.insert(tk.END, definition)  # Insert the definition text
        result_text.config(state=tk.DISABLED)  # Make the text widget read-only

    def clear_callback(self):
        # Clear entry field and result label
        self.word_entry.delete(0, tk.END)

    def exit_callback(self):
        # Exit the application
        self.root.quit()



#runs the main program
if __name__ == "__main__":
    root = tk.Tk()
    dictionary = DictionaryApp(root)
    root.mainloop()
