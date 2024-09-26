from tkinter import *
from PyDictionary import PyDictionary


#widgets

#main window with program name and search box
root = Tk()
root.title("Words Defined")

#function for the second window where definition will show
def second_window():
    # second window for definition
    window2 = Toplevel()
    def_window = Label(window2, text="Definition:", font=("Times", 30, "bold"), bg="skyblue")
    def_window.pack()


def search_word():


    #uses PyDictionary to find define word
    dictionary = PyDictionary()
    word_definition = dictionary.meaning(word_entry.get())



#title of the program name in the first window
my_title = Label(root, text="Words Defined: An English Dictionary", font=("Times", 25 ),  bg="skyblue", pady=20)
my_title.pack()

#word input widget
word_entry = Entry(root, width= 50, borderwidth=5)
word_entry.pack(pady=20)

#button to optimize search
search_button = Button(root, text="Search Word",  padx = 20, pady= 20, bg="white",command=second_window)
search_button.pack()









root.mainloop()
