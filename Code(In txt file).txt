import csv
import tkinter as tk
from tkinter import ttk
from tkinter import messagebox as msg
from tkinter import *
from PIL import ImageTk,Image

tax=tk.Tk()
tax.title('TAX CALCULATOR')

tax.config(bg='#ffffff')

method=tk.StringVar()
amt=tk.StringVar()
currency=tk.StringVar()
interest=tk.StringVar()
time=tk.StringVar()
period=tk.StringVar()
period_cmpnd=tk.StringVar()
inf_rate=tk.StringVar()
total_amt=tk.StringVar()
int_amt=tk.StringVar()

def SI():
    try:
        if period.get()=='years':
            si=float(amt.get())*(float(interest.get())-float(inf_rate.get()))*int(time.get())/100
            total_amt.set(str(round(float(amt.get())+si,2)) + ' ' + currency.get())
            int_amt.set(str(round(si,2)) + ' ' + currency.get())
            if (float(interest.get())-float(inf_rate.get()))<=0:
                msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
        else:
            si=float(amt.get())*(float(interest.get())-float(inf_rate.get()))*int(time.get())/(100*12)
            total_amt.set(str(round(float(amt.get())+si,2)) + ' ' + currency.get())
            int_amt.set(str(round(si,2)) + ' ' + currency.get())
            if (float(interest.get())-float(inf_rate.get()))<=0:
                msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            
    except ValueError:
        msg.showerror('OOPS!','Seems like some field is either empty or wrong type of value has been entered')
            

def CI():
    try:
        if period.get()=='years':
            if period_cmpnd.get()=='Yearly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/100))**int(time.get()))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Half-Yearly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*2)))**(2*int(time.get())))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Quarterly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*4)))**(4*int(time.get())))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Monthly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*12)))**(12*int(time.get())))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Daily':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*365)))**(365*int(time.get())))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
                
        else:
            if period_cmpnd.get()=='Yearly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/100))**(int(time.get())/12))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Half-Yearly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*2)))**(2*int(time.get())/12))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Quarterly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*4)))**(4*int(time.get())/12))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Monthly':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*12)))**(12*int(time.get())/12))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            elif period_cmpnd.get()=='Daily':
                ci=float(amt.get())*((1+((float(interest.get())-float(inf_rate.get()))/(100*365)))**(365*int(time.get())/12))
                total_amt.set(str(round(ci,2)) + ' ' + currency.get())
                int_amt.set(str(round(ci-float(amt.get()),2)) + ' ' + currency.get())
                if (float(interest.get())-float(inf_rate.get()))<=0:
                    msg.showwarning('LOSS ALERT!','Seems like the deal is not profitable!☹')
            
    except ValueError:
        msg.showerror('OOPS!','Seems like some field is either empty or wrong type of value has been entered')
        
         

def calculate():
    if method.get()=='Simple':
        SI()
    else:
        CI()

style=ttk.Style()
style.configure('TButton',font=('Gabriola',30,'bold'),foreground='#000000')

style.map('TButton',foreground=[('active','!disabled','green')],background=[('active','black')])

img=ImageTk.PhotoImage(Image.open('invest.jpg'))
panel=tk.Label(tax,image=img)
panel.grid(row=0,column=0,rowspan=1000,columnspan=1000,ipadx=300,ipady=200)
 
cur=[]

l1=ttk.Label(panel,text='TAX CALCULATOR',relief=SOLID,font=('Vineta BT',30),background='#ffffff',foreground='#000000')
l1.grid(row=0,column=0,columnspan=4,padx=130,pady=10,sticky=tk.W)

l2=ttk.Label(panel,text="Choose method of interest calculation: ",font=('MV Boli',20,'bold'),background='#ffffff',foreground='#000000')
l2.grid(row=1,column=0,pady=10,sticky=tk.W)

c1=ttk.Combobox(panel,width=18,state='readonly',textvariable=method,font=('BANKGOTHIC LT BT',15))
c1['values']=('Simple','Compound')
c1.current(0)
c1.grid(row=1,column=1,padx=10,ipady=5)


l3=ttk.Label(panel,text='Principal Amount:',font=('MV Boli',20,'bold'),background='#ffffff',foreground='#000000')
l3.grid(row=2,column=0,sticky=tk.W,pady=10)

e1=ttk.Entry(panel,width=19,textvariable=amt,font=('BANKGOTHIC LT BT',15))
e1.grid(row=2,column=1,pady=10,padx=10,ipady=5)
e1.focus()
c2=ttk.Combobox(panel,width=10,state='readonly',textvariable=currency,font=('BANKGOTHIC LT BT',15))
with open('list_one.csv','r') as f:
    reader=csv.DictReader(f)
    for row in reader:
        cur.append(row["Code"])
c2['values']=tuple(cur)
c2.current(111)
c2.grid(row=2,column=2,pady=10,sticky=tk.W,ipady=5)

l4=ttk.Label(panel,text='Interest Rate(%): ',font=('MV Boli',20,'bold'),background='#ffffff',foreground='#000000')
l4.grid(row=3,column=0,pady=10,sticky=tk.W)

e2=ttk.Entry(panel,width=19,textvariable=interest,font=('BANKGOTHIC LT BT',15))
e2.grid(row=3,column=1,pady=10,padx=10,ipady=5)

l5=ttk.Label(panel,text='% per year',font=('Monotype Corsiva',15,'bold'),background='#ffffff')
l5.grid(row=3,column=2,pady=10,sticky=tk.W)

l6=ttk.Label(panel,text='Time Period: ',font=('MV Boli',20,'bold'),background='#ffffff',foreground='#000000')
l6.grid(row=4,column=0,pady=10,sticky=tk.W)

e3=ttk.Entry(panel,width=19,textvariable=time,font=('BANKGOTHIC LT BT',15))
e3.grid(row=4,column=1,pady=10,padx=10,ipady=5)

c3=ttk.Combobox(panel,width=11,state='readonly',textvariable=period,font=('BANKGOTHIC LT BT',15))
c3['values']=('years','months')
c3.current(0)
c3.grid(row=4,column=2,pady=10,sticky=tk.W,ipady=5)

l7=ttk.Label(panel,text='*Compound Period: ',font=('MV Boli',20,'bold'),background='#ffffff',foreground='#000000')
l7.grid(row=5,column=0,pady=10,sticky=tk.W)

c4=ttk.Combobox(panel,width=18,state='readonly',textvariable=period_cmpnd,font=('BANKGOTHIC LT BT',15))
c4['values']=('Yearly','Half-Yearly','Quarterly','Monthly','Daily')
c4.current(0)
c4.grid(row=5,column=1,pady=10,padx=10,ipady=5)

l8=ttk.Label(panel,text='*If compoundly interested',font=('Agency FB',15,'bold'),background='#ffffff')
l8.grid(row=5,column=2,pady=10,sticky=tk.W)

l9=ttk.Label(panel,text='Inflation rate: ',font=('MV Boli',20,'bold'),background='#ffffff',foreground='#000000')
l9.grid(row=6,column=0,pady=10,sticky=tk.W)

e4=ttk.Entry(panel,width=19,textvariable=inf_rate,font=('BANKGOTHIC LT BT',15))
inf_rate.set('1')
e4.grid(row=6,column=1,pady=10,padx=10,ipady=5)

l10=ttk.Label(panel,text='(Taken 1% by default)',font=('Monotype Corsiva',15,'bold'),background='#ffffff')
l10.grid(row=6,column=2,pady=10,sticky=tk.W)

l11=ttk.Label(panel,text='Total Amount = ',font=('MV Boli',20,'bold'),relief=SUNKEN,background='#ffffff',foreground='#000000',borderwidth=6)
l11.grid(row=7,column=0,pady=10,sticky=tk.W)

e5=ttk.Entry(panel,width=19,textvariable=total_amt,font=('Berlin Sans FB',20,'italic','bold'))
e5.grid(row=7,column=1,pady=10,padx=10,ipady=5)

l12=ttk.Label(panel,text='Interest Amount = ',font=('MV Boli',20,'bold'),relief=SUNKEN,background='#ffffff',foreground='#000000',borderwidth=6)
l12.grid(row=8,column=0,pady=10,sticky=tk.W)

e6=ttk.Entry(panel,width=19,textvariable=int_amt,font=('Berlin Sans FB',20,'italic','bold'))
e6.grid(row=8,column=1,pady=10,padx=10,ipady=5)

b1=ttk.Button(panel,text='CALCULATE',command=calculate,style='TButton')
b1.grid(row=9,column=0,pady=10,sticky=tk.E+tk.N,ipady=5)

tax.mainloop()
