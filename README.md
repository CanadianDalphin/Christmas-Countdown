# Christmas-Countdown
# We made a Christmas coundown with a Raspberry Pi that displays months,days,hours,minutes, and seconds until Christmas!
from time import sleep
import threading
from Tkinter import *
import datetime

class SensorThread(threading.Thread):
    def run(self):
        try:
            while True:
                sleep(1)
        except KeyboardInterrupt:
            exit()

class Gui(object):
    def __init__(self):
        self.root = Tk()
        self.lbl = Label(self.root, text="")
        self.updateGUI()

    def run(self):
        self.lbl.pack()
        self.lbl.after(1000, self.updateGUI)
        self.root.mainloop()

    def updateGUI(self):
        dt=datetime.datetime.now()
        msg = ""
        
        msg = str(12-dt.month)+" Month"
        if 12-dt.month!=1:msg+="s"
        msg+=", "
        msg += str(24-dt.day)+" Day"
        if 24-dt.day!=1:msg+="s"
        msg+=", "
        msg += str(23-dt.hour)+" Hour"
        if 23-dt.hour!=1:msg+="s"
        msg+=", "
        msg += str(59-dt.minute)+" Minute"
        if 59-dt.minute!=1:msg+="s"
        msg+=", "
        msg += str(59-dt.second)+" Second"
        if 59-dt.second!=1:msg+="s"
        msg+=" Until Christmas!!!"
        
        self.lbl["text"] = msg
        self.root.update()
        self.lbl.after(1000, self.updateGUI)

if __name__ == "__main__":
    SensorThread().start()
    Gui().run()
