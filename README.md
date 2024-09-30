from tkinter import messagebox
import tkinter as tk
from PIL import Image, ImageTk
from PyDictionary import PyDictionary
# GUI Application class


class DictionaryApp:
    def __init__(self,root):

        self.root = tk.Tk()
        self.root.title("Words Defined")
        self.root.geometry("500x500")

        self.gui_setup()

    def gui_setup(self):
        #labels
        self.my_title = tk.Label(self.root, text="Words Defined: An English Dictionary", font=("Times", 25 , "bold"), bg="skyblue")
        self.my_title.pack()


        # word input widget
        self.word_entry = tk.Entry(self.root, width=50, borderwidth=5)
        self.word_entry.pack(pady=20)

        # button to optimize search
        self.search_button = tk.Button(self.root, text="Search Word",command=self.second_window, padx=20, pady=20, bg="white")
        self.search_button.pack()
        # button to clear word
        self.clear_button = tk.Button(self.root, text="Clear", padx=20, pady=20, bg="white")
        self.clear_button.pack()
        # button to exit program
        self.exit_button = tk.Button(self.root, text="Exit", padx=20, pady=20, bg="white", command=self.root.destroy)
        self.exit_button.pack()



    def second_window(self):
        # second window for definition
        self.window2 = tk.Toplevel()
        self.def_window = tk.Label(self.window2, text="Definition:", font=("Times", 30, "bold"), bg="skyblue")
        self.def_window.pack()

        # result label
        self.result_label = tk.Label(self.window2, text="", wraplength=500, justify="left", anchor="w",font=("Arial", 12))
        self.result_label.pack(pady=20)


    def search_word(self):


      #uses PyDictionary to find define word
      self.dictionary = PyDictionary()
      self.word_definition = self.dictionary.meaning(self.word_entry.get())



if __name__ == "__main__":
    root = tk.Tk()
    app = DictionaryApp(root)
    root.mainloop()

