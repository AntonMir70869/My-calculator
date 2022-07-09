from tkinter import *
from math import *


class CalculatorButton(Button):
    def __init__(self, master, text, command):
        super().__init__(
            master=master,
            text=text, bg="#FFF",
            font=("Times New Roman", 15),
            command=command, width=10, height=3
        )


class Main(Frame):
    def __init__(self, root):
        super(Main, self).__init__(root)
        self.build(root)
        self.Deg = True
        self.Rad = False

    def build(self, root):

        root.columnconfigure(0, weight=1, minsize=1)
        root.rowconfigure(0, weight=1, minsize=1)

        self.lbl = Entry(master=root, font=("Times New Roman", 21, "bold"), bg="#000", foreground="#FFF")
        self.lbl.insert(0, "0")

        self.lbl.grid(row=0, column=0, ipady=10, pady=10, padx=10, columnspan=7, sticky=EW)

        _btns = [
            CalculatorButton(root, 'C', self._C),
            CalculatorButton(root, 'DEL', self._DEL),
            CalculatorButton(root, 'ln', self._ln),
            CalculatorButton(root, 'log', self._log),
            CalculatorButton(root, 'sin', self._sin),
            CalculatorButton(root, 'cos', self._cos),
            CalculatorButton(root, 'tan', self._tan),
            CalculatorButton(root, '1', self.simple_vals1),
            CalculatorButton(root, '2', self.simple_vals2),
            CalculatorButton(root, '3', self.simple_vals3),
            CalculatorButton(root, '+', self.simple_vals15),
            CalculatorButton(root, '-', self.simple_vals16),
            CalculatorButton(root, 'π', self._pi),
            CalculatorButton(root, 'e', self._exp),
            CalculatorButton(root, '4', self.simple_vals4),
            CalculatorButton(root, '5', self.simple_vals5),
            CalculatorButton(root, '6', self.simple_vals6),
            CalculatorButton(root, '*', self.simple_vals13),
            CalculatorButton(root, '/', self.simple_vals14),
            CalculatorButton(root, 'x^2', self._degree),
            CalculatorButton(root, '1/x', self._rev),

            CalculatorButton(root, '7', self.simple_vals7),
            CalculatorButton(root, '8', self.simple_vals8),
            CalculatorButton(root, '9', self.simple_vals9),
            CalculatorButton(root, '^', self.simple_vals17),
            CalculatorButton(root, '=', self._equals),
            CalculatorButton(root, '√', self._sqrt),
            CalculatorButton(root, 'x!', self._fact),

            CalculatorButton(root, '(', self.simple_vals11),
            CalculatorButton(root, '0', self.simple_vals10),
            CalculatorButton(root, ')', self.simple_vals12),

            CalculatorButton(root, '.', self.simple_vals18),
            CalculatorButton(root, '%', self.percent),
            CalculatorButton(root, 'Rad', self._Rad),
            CalculatorButton(root, 'Deg', self._Deg),
        ]

        r = 1
        c = 0

        for bt in _btns:
            root.columnconfigure(c, weight=1, minsize=55)
            root.rowconfigure(c, weight=1, minsize=30)
            bt.grid(row=r, column=c, pady=5, padx=5)

            c += 1
            if c > 6:
                c = 0
                r += 1

    def _Deg(self):
        self.Deg = True
        self.Rad = False

    def _Rad(self):
        self.Deg = False
        self.Rad = True

    def _sin(self):
        if self.Rad:
            x = self.lbl.get()
            self.lbl.delete(0, END)
            self.lbl.insert(0, str(round(sin(float(x)), 7)))
            self.update()
        elif self.Deg:
            x = self.lbl.get()
            self.lbl.delete(0, END)
            self.lbl.insert(0, str(round(sin(radians(float(x))), 7)))
            self.update()

    def _cos(self):
        if self.Rad:
            x = self.lbl.get()
            self.lbl.delete(0, END)
            self.lbl.insert(0, str(round(cos(float(x)), 7)))
            self.update()
        elif self.Deg:
            x = self.lbl.get()
            self.lbl.delete(0, END)
            self.lbl.insert(0, str(round(cos(radians(float(x))), 7)))
            self.update()

    def _tan(self):
        if self.Rad:
            x = self.lbl.get()
            self.lbl.delete(0, END)
            self.lbl.insert(0, str(round(tan(float(x)), 7)))
            self.update()
        elif self.Deg:
            x = self.lbl.get()
            self.lbl.delete(0, END)
            self.lbl.insert(0, str(round(tan(radians(float(x))), 7)))
            self.update()

    def _C(self):
        self.lbl.delete(0, END)
        self.lbl.insert(0, "0")
        self.update()

    def _DEL(self):
        self.lbl.delete((int(len(self.lbl.get()))) - 1)
        self.update()

    def _degree(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str((eval(x)) * 2))
        self.update()

    def _equals(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(eval(x)))
        self.update()

    def _fact(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(factorial(int(x))))
        self.update()

    def _ln(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(log(float(x), e)))
        self.update()

    def _log(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(log10(float(x))))
        self.update()

    def _sqrt(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(sqrt(float(x))))
        self.update()

    def _pi(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(pi))
        self.update()

    def _exp(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(e))
        self.update()

    def _rev(self):
        x = self.lbl.get()
        self.lbl.delete(0, END)
        self.lbl.insert(0, str(1 / float(x)))
        self.update()

    def simple_vals1(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "1")
        self.update()

    def simple_vals2(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "2")
        self.update()

    def simple_vals3(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "3")
        self.update()

    def simple_vals4(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "4")
        self.update()

    def simple_vals5(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "5")
        self.update()

    def simple_vals6(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "6")
        self.update()

    def simple_vals7(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "7")
        self.update()

    def simple_vals8(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "8")
        self.update()

    def simple_vals9(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "9")
        self.update()

    def simple_vals10(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "0")
        self.update()

    def simple_vals11(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "(")
        self.update()

    def simple_vals12(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, ")")
        self.update()

    def simple_vals13(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "*")
        self.update()

    def simple_vals14(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "/")
        self.update()

    def simple_vals15(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "+")
        self.update()

    def simple_vals16(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "-")
        self.update()

    def simple_vals17(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, "^")
        self.update()

    def simple_vals18(self):
        if self.lbl.get() == "0":
            self.lbl.delete(0, END)
        self.lbl.insert(len(self.lbl.get()) + 1, ".")
        self.update()

    def percent(self):
        l = self.lbl.get()
        l1 = (l.translate(l.maketrans("*/+-^()", "       "))).split()
        x1 = l1[-1]
        x2 = l1[-2]
        char1 = '('
        char2 = ')'
        isRightParenExists = l.find(char2) > -1
        isLeftParenExists = l.find(char1) > -1
        self.lbl.delete(len(self.lbl.get()) - len(x1), len(self.lbl.get()))

        if isRightParenExists and isLeftParenExists:
            x2 = float(eval(str(l)[str(l).find(char1) + 1: str(l).find(char2)]))
            self.lbl.insert(len(self.lbl.get()) + 1, str(float(x2) / 100 * float(x1)))
        elif not isRightParenExists and not isLeftParenExists:
            self.lbl.insert(len(self.lbl.get()) + 1, str(float(x2) / 100 * float(x1)))
        else:
            print("error")
        self.update()

    def update(self):
        if self.lbl.get() == "":
            self.lbl.insert(0, "0")
        if self.lbl.get() == "0.0":
            self.lbl.delete(0, END)
            self.lbl.insert(0, "0")


if __name__ == '__main__':
    root = Tk()
    root["bg"] = "#000"
    root.geometry("720x630")
    root.title("Калькулятор")
    root.resizable(True, True)
    app = Main(root)
    app.grid()
    root.mainloop()
