from tkinter import filedialog
import qrcode
import customtkinter as ctk
import tkinter as tk
from PIL import Image, ImageTk

class App(ctk.CTk):
    def __init__(self):
        ctk.set_appearance_mode("light")
        super().__init__(fg_color= "white")
        self.title("codigo QR")
        self.geometry("400x400")
        
        self.entry_string = ctk.StringVar()
        self.entry_string.trace("w",self.create_qr)

        EntryField(window = self, entry_string = self.entry_string, save_func = self.save)
        self.bind('<Return>', self.save)
        
        resize_image = qrcode.make("Hello World").resize((200,200))
        tk_resize_image = ImageTk.PhotoImage(resize_image)
        self.qr_image = QrImage(window = self)
        self.qr_image.update_image(tk_resize_image)
        self.mainloop()

    def save(self, event=""):
        if self.raw_image:
            file_path = filedialog.asksaveasfilename()

            if file_path:
                self.raw_image.save(file_path + ".jpg")

    def create_qr(self, *args):
        current_text = self.entry_string.get()
        if current_text:
            self.raw_image = qrcode.make(current_text).resize((200,200))
            self.tk_image = ImageTk.PhotoImage(self.raw_image)
            self.qr_image.update_image(self.tk_image)
        else:
            self.qr_image.clear()
            self.raw_image = None
            self.tk_image = None

class EntryField(ctk.CTkFrame):
    def __init__(self, window, entry_string, save_func):
        super().__init__(master = window, corner_radius = 20, fg_color = "blue")
        self.place(relx=0.5, rely=1, relwidth=1, relheight=0.4, anchor="center")
        self.rowconfigure(0, weight = 1, uniform = "a")
        self.rowconfigure(1, weight = 1, uniform = "a")
        self.columnconfigure(0, weight = 1, uniform = "a")
 
        self.sub_frame = ctk.CTkFrame(master = self, fg_color ="transparent" )
        self.sub_frame.columnconfigure(0, weight=1)
        self.sub_frame.columnconfigure(1, weight=4)
        self.sub_frame.columnconfigure(2, weight=2)
        self.sub_frame.columnconfigure(3, weight=1)
        self.sub_frame.grid(row=0, column=0)

        entry = ctk.CTkEntry(master = self.sub_frame, 
                             textvariable = entry_string,
                             fg_color ="#2E54E8", 
                             border_width =  0, 
                             text_color = "white" )
        entry.grid(row = 0, column = 1, sticky = "nsew")

        button = ctk.CTkButton(master=self.sub_frame, 
                               command = save_func,
                               text="save", 
                               fg_color="#2E54E8", 
                               hover_color="#4266f1")
        button.grid(row=0, column=2, sticky="nsew", padx=10)

class QrImage(tk.Canvas):
    def __init__(self, window):
        super().__init__(master = window, 
                         background = "red",
                         bd = 0,
                         highlightthickness = 0,
                         relief = "ridge")
        self.place(relx =0.5, rely=0.4, width=200, height=200, anchor="center" )
    
    def update_image(self, tk_resized_image):
        self.create_image(0, 0, anchor = "nw", image= tk_resized_image)
    def clear(self):
        self.delete("all")
    

    
app = App()


