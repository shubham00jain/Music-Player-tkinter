from tkinter import *
from pygame import mixer
from tkinter import filedialog
from tkinter import ttk
import time
import os
from ttkthemes import themed_tk as tk
from mutagen.mp3 import MP3
import threading

playlist= list()

def OpenFile():
    global namepath
    namepath=filedialog.askopenfilename()
    Add(namepath)
    print(name)

def Add(filename):
    filename=os.path.basename(filename)
    index=0
    l1.insert(index,filename)
    playlist.insert(index,namepath)
    index+=1

def Delete():
    song=l1.curselection()
    song=int(t[0])
    l1.delete(song)
    playlist.pop(song)
    
def NewFile():
    print("New File")
def About():
    tkinter.messagebox.showinfo('My Window','Created By AK')

def Exit():
    root.destroy()
def Volume(event):
    value=v.get()
    mixer.music.set_volume(value/100)


def Play():
    t=l1.curselection()[0]
    name=l1.get(t)
    audio=MP3(name)
    mixer.music.load(name)
    mixer.music.play()
    l1.configure(text="song played")
	
def Pause():
    global paused
    if(paused==1):
        mixer.music.pause()
        label.configure(text="paused")
        paused=0
    elif(paused==0):
        mixer.music.unpause()
        label.configure(text="played again")
        paused=1
        
def Stop():
    mixer.music.stop()
    label.configure(text="stopped")
def Mute():
    global muted
    if(muted==1):
        s.set(0)
        muted=0
        s.configure(text="muted")
    else:
        s.set(70)
        muted=1
        s.configure(text="unmuted")
def Rewind():
    pass
mixer.init()

def Start():
    length=0
    while True:
        minute,sec=divmod(length,60)
        minute=round(minute)
        sec=round(sec)
        label['text']="{:02}:{:02}".format(minute,sec)
        time.sleep(1)
        length+=1
root=tk.ThemedTk()
root.set_theme('scidgrey')
#t=song.get()
root.iconbitmap('melody.ico')
root.title('Music Player')

#menu bar

menu=Menu(root)
root.config(menu=menu)
filemenu=Menu(menu,tearoff=0)
menu.add_cascade(label='File',menu=filemenu)
filemenu.add_command(label='New File',command=NewFile)
filemenu.add_command(label='Open',command=OpenFile)
filemenu.add_separator()
filemenu.add_command(label='Exit',command=Exit)
helpmenu=Menu(menu,tearoff=0)
menu.add_cascade(label='Help',menu=helpmenu)
helpmenu.add_command(label='About',command=About)

#statusbar at bottom
statusbar=Label(root,text='Welcome to My Music Player', font='arial 10 italic',anchor=W)
statusbar.pack(side=BOTTOM,fill=BOTH)

frame1=Frame(root)
frame1.pack(padx=10,pady=10,side=LEFT,fill=BOTH,expand=YES)
topframe1=Frame(frame1)
topframe1.pack(fill=BOTH,expand=YES)
l1=Listbox(topframe1)
l1.pack(fill=BOTH,expand=YES,padx=5,pady=5)
bottomframe1=Frame(frame1)
bottomframe1.pack(padx=10,pady=10,fill=BOTH,expand=YES)
b1=Button(bottomframe1,text='+Add',command=Add)
b1.pack(side=LEFT,fill=BOTH,expand=YES)
b2=Button(bottomframe1,text='-Del',command=Delete)
b2.pack(side=LEFT,fill=BOTH,expand=YES)

frame2=Frame(root)
frame2.pack(side=RIGHT,fill=BOTH,expand=YES)

topframe2=Frame(frame2)
topframe2.pack(fill=BOTH,expand=YES)
l2=Label(topframe2,text='Total length= {}'.format(time),font="arial 10")
l2.pack(padx=10,pady=10,fill=BOTH, expand=YES)
l3=Label(topframe2,text='Current time={}'.format(time),font="arial 10")
l3.pack(padx=10,pady=10,fill=BOTH, expand=YES)

middleframe2=Frame(frame2)
middleframe2.pack(fill=BOTH,expand=YES)
img1=PhotoImage(file='play.png')
ttk.Button(middleframe2,image=img1,command=Play).pack(side=LEFT,fill='x',expand=YES)
img2=PhotoImage(file='pause.png')
ttk.Button(middleframe2,image=img2,command=Pause).pack(side=LEFT,fill='x',expand=YES)
img3=PhotoImage(file='stop.png')
ttk.Button(middleframe2,image=img3,command=Stop).pack(fill="x",expand=YES)

bottomframe2=Frame(frame2)
bottomframe2.pack(fill=BOTH,expand=YES)
img4=PhotoImage(file='rewind.png')
ttk.Button(bottomframe2,image=img4,command=Rewind).pack(side=LEFT,fill=BOTH,expand=YES)
img5=PhotoImage(file='mute.png')
ttk.Button(bottomframe2,image=img5,command=Mute).pack(side=LEFT,fill=BOTH,expand=YES)
v=IntVar()
s=Scale(bottomframe2,orient=HORIZONTAL,from_=0,to=100,variable=v,command=Volume)
s.pack(side=BOTTOM)
s.set(70)

root.mainloop()
