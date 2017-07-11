# decompte_temps
# programme simulant une pointeuse pour comptabiliser le temps de travail

# pour python 3.x
# -*- coding: cp1252 -*- NON

#
from time import *
from tkinter import *
#from tkFont import *

liste_instants=[]

#
def ajout_instant (la_liste) :
#def ajout_instant () :
    "ajout d'un instant dans une liste"
#    liste_instants.append(time())
#    print liste_instants
    la_liste.append(time())
#    print la_liste

def conversion_hms (duree) :
    'convertit la durée donnée en secondes en heures, minutes, secondes'
    duree = int(duree)
    secondes = duree % 60
    duree = duree // 60
    minutes = duree % 60
    duree = duree // 60
    heures = duree % 60
    if minutes<10 :
        s_minutes = '0' + str(minutes)
    else :
        s_minutes = str(minutes)
    if secondes<10 :
        s_secondes = '0' + str(secondes)
    else :
        s_secondes = str(secondes)
    result = str(heures) + ':' + s_minutes + ':' + s_secondes
    return result

def temps_travail (la_liste) :
    'calcule le temps de travail en fonction de la liste des instants'
    temps = 0
    i,longueur = 0,len(la_liste)
    while i < longueur :
        if i==longueur-1 :
            temps = temps + time() - la_liste[i]
        else :
            temps = temps + la_liste[i+1] - la_liste[i]
        i = i+2
    return temps

def texte_bouton (la_liste) :
    "définition du texte du bouton : stopper le décompte ou le commencer"
    longueur = len(la_liste)
    if longueur==0 :
        texte = "commencer le décompte du temps de travail"
    elif longueur%2==0 :
        texte = "reprendre le décompte du temps de travail"
    else :
        texte = "interrompre le décompte du temps de travail"
    return texte

#def afficher_horloge (la_liste) :
#    horloge.configure(text=conversion_hms(temps_travail(la_liste)))
def afficher_horloge () :
#    horloge.configure(text=conversion_hms(temps_travail(liste_instants)))
    i=0
    while i<30 :
            horloge.configure(text=conversion_hms(temps_travail(liste_instants)))
#            sleep(0.5)
            i=i+1
#    fenetre.after(500,afficher_horloge)

#
def appui_bouton () :
    ajout_instant(liste_instants)
    bouton.configure(text=texte_bouton(liste_instants))
    afficher_horloge()

#
fenetre = Tk()
fenetre.title("Décompte du temps de travail")

#
#type_caract=Font(size=20)
type_caract="20"
horloge = Label(fenetre,text=conversion_hms(0),font=type_caract)
#,width=18)
horloge.grid(row=1,column=1)
bout_affich_horlog = Button(fenetre,text='afficher le temps de travail'\
                            ,command=afficher_horloge)
bout_affich_horlog.grid(row=1,column=2)
#bouton = Button(fenetre,text=texte_bouton(liste_instants)\
#                ,command=ajout_instant(liste_instants))
#bouton = Button(fenetre,text=texte_bouton(liste_instants),command=ajout_instant())
bouton = Button(fenetre,text=texte_bouton(liste_instants)\
                ,command=appui_bouton)
bouton.grid(row=2,column=1,columnspan=2)
#fenetre.bind('<Button-1>',afficher_horloge)
#horloge.bind('<Button-1>',afficher_horloge(liste_instants))

#
fenetre.mainloop()

#fenetre.destroy()
#
#ma_liste=[]
#print temps_travail(ma_liste)
#ajout_instant(ma_liste)
#print ma_liste
#sleep(2)
#ajout_instant(ma_liste)
#print temps_travail(ma_liste)
#sleep(1.44)
#ajout_instant(ma_liste)
#sleep(2.68)
#print ma_liste
#print temps_travail(ma_liste)
#une_duree = 7589
#print conversion_hms (une_duree), une_duree
#print liste_instants
