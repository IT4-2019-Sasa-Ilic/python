#1.a)
from datetime import datetime
from dateutil.relativedelta import relativedelta

class Student:
    def __init__(self, ime, prezime,br_indeksa,datum_rodjenja=None):
        self.ime = ime
        self.prezime = prezime
        self.br_indeksa = br_indeksa
        self.datum_rodjenja = datum_rodjenja if datum_rodjenja is not None else datetime.now().date() - relativedelta(years=18)
 #1.b)
    def __str__(self):
        return '{} {} ({}) - {}'.format(self.ime,self.prezime,self.br_indeksa,self.datum_rodjenja)
        
student1= Student('Sasa','Ilic','IT4')
print(student1.datum_rodjenja)
student1.datum_rodjenja = datetime.now().date()
print(student1)

#2.a)
num = int(input("Unesite broj "))

def zadatak_2(n):
    a=[]
    for x in range(1,num+1):
        if num%x==0:
            a.append(x)
    print(a)
    
zadatak_2(num)

#2.b
def prosti_brojevi(n):
    lista = []
    for num in range(2, n+1):
        if all(num % i != 0 for i in range(2, num)):
            lista.append(num)
    print(lista)

num = int(input("Unesite broj "))
prosti_brojevi(num)

#3.a)
import numpy as np
def mult_table(num):
    t = np.arange(1, num+1)
    b = np.arange(1, num+1)
    array = np.array(np.outer(t, b))
    m,n = array.shape
    nule = np.zeros(shape=(n), dtype=int)
    a=np.insert(array, 0, nule,axis=0)
    nule = np.insert(nule,0,0)
    a1 = np.insert(a, 0,nule,axis=1)
    t= np.insert(t,0,0)
    a1=np.insert(a1, 0,t,axis=0)
    a1= np.insert(a1, 0,np.insert(b,[0,0],0),axis=1)
    aa=str(a1)
    lista = list(aa)
    lista[4] = ' '
    str1 = ''.join(lista)
    print(str1)
    
for i in range(0,10):
    num = input('unesite ceo broj ')
    try:
        num = int(num)
        mult_table(num)
    except ValueError as ve:
        print('Morate uneti ceo broj')
        continue
    break
    
    #3.b)
import numpy as np
def mult_table(m,n):
    t = np.arange(m, n+1)
    b = np.arange(m, n+1)
    array = np.array(np.outer(t, b))
    a=np.insert(array, 0, t,axis=0)
    b2 = np.insert(b,0,1)
    a1= np.insert(a, 0,b2,axis=1)
    aa=str(a1)
    lista = list(aa)
    lista[3] = ' '
    str1 = ''.join(lista)
    print(str1)

for i in range(0,10):
    m = input('unesite prvi ceo broj ')
    n = input('unesite drugi ceo broj ')
    try:
        n = int(n)
        m= int(m)
        mult_table(m,n)
        break
    except ValueError as ve:
        print('Morate uneti ceo broj')
        continue
        
#4.a)
import matplotlib.pyplot as plt
import numpy

def generator(n,asc):
    i=1
    if(asc==True):
        while True:
            yield n*i
            i=i*n
    else:
        while True:
            yield n*i
            i=i/n
hajmo = generator(4,True)
print(next(hajmo))
print(next(hajmo))
print(next(hajmo))

#4.b)
def fun(x):
    lista = []
    hajmo = generator(2,True)
    for i in range(0,x):
        lista.append(next(hajmo))
    lista2 = numpy.arange(1,x+1)
    plt.plot(lista2,lista)
    plt.show()
    
fun(10)

#5.a)
import random
import time
import datetime
lista_dict = []
for i in range(500):
    new_dict = {}
    values = ['Koncert','Putovanje','Ispit','Sastanak']
    new_dict['Dogadjaj'] = random.choice(values)
    d = random.randint(1, int(time.time()))
    new_dict['Datum'] = datetime.date.fromtimestamp(d).strftime('%Y-%m-%d')
    lista_dict.append(new_dict)

#5.b)
import os
import csv
header = ['Dogadjaji','Datum']
if not os.path.exists('Dogadjaji'):
    os.makedirs('Dogadjaji')
for i in range(0,len(lista_dict)):
    year,month,day=lista_dict[i]['Datum'].split('-')
    if not os.path.exists('Dogadjaji'+'/' + month):
        os.makedirs('Dogadjaji'+'/' + month)
    naziv = '/'.join(['Dogadjaji' , month,day + '.csv'])
    if not os.path.exists(naziv):
        with open(naziv,'w') as f:
            writer = csv.writer(f)
            writer.writerow(header)
for i in range(0,len(lista_dict)):
    year,month,day=lista_dict[i]['Datum'].split('-')
    naziv = '/'.join(['Dogadjaji' , month,day + '.csv'])
    lista = [lista_dict[i]['Dogadjaj'],lista_dict[i]['Datum']]
    with open(naziv,'w') as f:
        writer = csv.writer(f)
        writer.writerow(lista)

Jos nesto sto moze biti korisno....
#5.a) primeri - generisanje random 1000 znakova i njihov upis u random fajlove
import uuid
import string
import random
import os
if not os.path.exists('data'):
    os.makedirs('data')
broj_fajlova = random.randint(2, 10)
for i in range(0,broj_fajlova):
    naziv = '/'.join(['data',str(uuid.uuid4())+'.txt'])   
    text = string.ascii_lowercase + string.digits
    result_str = ''.join(random.choice(text) for i in range(1000))
    with open(naziv,'w') as f:
        f.write(result_str)

#5.b) - prebrojavanje koji karakter se najcesce ponavlja u fajlu
import os
fajlovi = os.listdir('data')
lista1 = []
lista2 = []
lista3 = []
for f in fajlovi:
    new_dict= {}
    file = open('data/' + f)
    lista3.append(f)
    stri= file.read();
    for x in stri:
        if x in new_dict.keys():
            new_dict[x] = new_dict.get(x,0)+1
        else:
            new_dict[x]=1
    lista1.append(max(new_dict,key=new_dict.get))
    lista2.append(max(new_dict.values()))
    file.close()
    
print(lista1)
print(lista2)
print(lista3)
print(max(lista2))
print(lista2.index(max(lista2)))
print('Najvise se ponavlja {}, {} puta u fajlu {}'.format(lista1[lista2.index(max(lista2))],max(lista2),lista3[lista2.index(max(lista2))]))

Raspakivanje recnika....

primer= {"a": 1, "b": {"1": 1, "2": 2}}
new_dict = {} 
print(primer)
for item in primer.items():
    kljuc,vrednost=item
    if(type(vrednost)==dict):
        for key,value in vrednost.items():
            new_dict[kljuc + '-' + key] = value
        
    else:
        new_dict[kljuc] = vrednost
        
print(new_dict)

Raspakivanje recnika naprednije

def raspakuj(recnik,dodatni_arg):
    new_dict = {}
    if(dodatni_arg==True):
        for item in recnik.items():
            k,v = item
            if(type(v)==dict):
                for key,value in v.items():  
                    if(type(value)==dict):
                        for ke,valu in value.items():
                            new_dict[k + '-' + key + '-' + ke] = valu
                    else:
                        new_dict[k + '-' + key] = value
            else:
                new_dict[k] = v
    else:
        for item in recnik.items():
            k,v = item
            if(type(v)==dict):
                for key,value in v.items():
                    if key not in new_dict.keys():
                        
                
        
    print(new_dict)
