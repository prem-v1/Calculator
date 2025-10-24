# Calculator
# Simple calculator software code. It can add, sub, multiply, divide & other maths...

    import tkinter as tk
    from tkinter import messagebox

# MAIN CALCULATOR LOGIC

    def button_click(item):

# Handles button presses (numbers and operators)
    global expression
    current_text = input_text.get()
    
    if item == '=':
        try:

# Convert symbols to Python-compatible ones
            temp_expression = (
      current_text.replace('×', '*')
                .replace('÷', '/')
                .replace('%', '/100*')
                .replace('−', '-'))
            
            result = str(eval(temp_expression))
            input_text.set(result)
            expression = result
            
# Zero division error
        except ZeroDivisionError:
            input_text.set("Error")
            expression = ""
        except Exception:
            input_text.set("Error")
            expression = ""
            
# All clear button
    elif item == 'C':
        expression = ""
        input_text.set("")
        
# Single clear button
    elif item == '⌫':
        expression = current_text[:-1]
        input_text.set(expression)

    else:
        expression += str(item)
        input_text.set(expression)


# GUI SETUP
    expression = ""
    root = tk.Tk()
    root.title("Calculator")
    root.configure(bg='black')
    root.geometry("360x560")
    root.resizable(False, False)

    input_text = tk.StringVar()

    display_font = ('Segoe UI', 30, 'bold')
    input_field = tk.Entry(
    root, font=display_font, textvariable=input_text, bd=0,
    bg="black", fg="#00cc66", insertwidth=4, justify='right',
    relief=tk.FLAT, highlightthickness=0
    )
    input_field.grid(row=0, column=0, columnspan=4, padx=10, pady=(460, 20), ipady=0, sticky="ew")
    tk.Frame(root, height=2, bg='#3a3a3a').grid(row=1, column=0, columnspan=10, padx=10, sticky="ew")

# BUTTON COLOR SETUP
    BUTTONS = [
    ('⌫', 2, 0, '#ff6666', 'white', 18),   
    ('C', 2, 1, '#3a3a3a', 'white', 18),   
    ('.', 2, 2, '#3a3a3a', 'white', 22),
    ('÷', 2, 3, '#6a6e73', 'white', 22),

    ('7', 3, 0, '#3a3a3a', 'white', 22),
    ('8', 3, 1, '#3a3a3a', 'white', 22),
    ('9', 3, 2, '#3a3a3a', 'white', 22),
    ('×', 3, 3, '#6a6e73', 'white', 22),

    ('4', 4, 0, '#3a3a3a', 'white', 22),
    ('5', 4, 1, '#3a3a3a', 'white', 22),
    ('6', 4, 2, '#3a3a3a', 'white', 22),
    ('−', 4, 3, '#6a6e73', 'white', 22),

    ('1', 5, 0, '#3a3a3a', 'white', 22),
    ('2', 5, 1, '#3a3a3a', 'white', 22),
    ('3', 5, 2, '#3a3a3a', 'white', 22),
    ('+', 5, 3, '#6a6e73', 'white', 22),

    ('0', 6, 1, '#3a3a3a', 'white', 22),
    ('=', 6, 3, '#00cc66', 'white', 22),
    ]

# SEPARATOR LINE

    tk.Frame(root, height=2, bg='#3a3a3a').grid(row=1, column=0, columnspan=4, padx=20, sticky="ew")

    for (text, row, col, bg_color, fg_color, font_size) in BUTTONS:
    def create_round_button(master, text, size, color, command, text_color):
        canvas = tk.Canvas(master, width=size, height=size, bd=0, highlightthickness=0, bg='black')
        canvas.create_oval(0, 0, size, size, fill=color, outline=color)
        canvas.create_text(size/2, size/2, text=text, fill=text_color, font=('Segoe UI', font_size, 'bold'))
        canvas.bind("<Button-1>", lambda event, t=text: command(t))
        return canvas

    button_size = 140 
    btn_canvas = create_round_button(root, text=text, size=button_size, color=bg_color, command=button_click, text_color=fg_color)
    btn_canvas.grid(row=row, column=col, padx=3, pady=3)
    root.grid_rowconfigure(0, weight=1)
    for i in range(1, 10): 
    root.grid_rowconfigure(i, weight=1)
    for i in range(4):
    root.grid_columnconfigure(i, weight=1)
    root.mainloop()
