---
cssclasses: 
tags:
  - unity
  - guides
  - ongoing
  - "#scriptableObjects"
date: 2024-05-13T18:58:00
---
---
# Event System

Un sistema di eventi basato sugli Scriptable Objects è un modo potente per gestire e distribuire eventi all'interno di un'applicazione Unity. Ecco una sintesi su come funziona:

---

 ### **Scriptable Objects**: 
 In Unity, gli Scriptable Objects sono oggetti speciali che possono contenere dati, ma non sono associati a specifiche istanze di gioco. Questi oggetti persistono tra le scene e le sessioni di gioco, rendendoli ideali per la memorizzazione di dati globali e per la comunicazione tra i vari sistemi dell'applicazione.
 
---

### **Definizione degli eventi**: 

Crei uno Scriptable Object per rappresentare un tipo di evento specifico. Questo oggetto conterrà le informazioni sull'evento che si vuole comunicare, come un ID univoco e eventuali dati aggiuntivi.

---
```
using UnityEngine;

\[CreateAssetMenu(fileName = "NuovoEvento", menuName = "Eventi/NuovoEvento", order = 1)]
public class Evento : ScriptableObject
\{
	public string idEvento;
	public int datiAggiuntivi;
	// Puoi aggiungere altri dati aggiuntivi necessari per l'evento
\}
```
---

### **Sottoscrizione agli eventi**: 
Gli oggetti che desiderano essere avvisati di quando un evento si verifica si sottoscrivono agli Scriptable Objects corrispondenti. Questa sottoscrizione può avvenire tramite riferimenti diretti agli Scriptable Objects o attraverso un sistema di gestione degli eventi.

---

### **Generazione dell'evento**: 
Quando un evento si verifica nel gioco, ad esempio il completamento di una determinata azione, viene creato un'istanza dell'oggetto evento corrispondente. Questo oggetto viene quindi passato agli Scriptable Objects che rappresentano quelli che si sono sottoscritti all'evento.

---

### **Gestione degli eventi**: 
Gli Scriptable Objects ricevono l'evento e possono eseguire le azioni appropriate in risposta. Ad esempio, un evento "Nemico Sconfitto" potrebbe attivare una funzione in uno ScriptableObject che gestisce il punteggio del giocatore, aumentando il punteggio di conseguenza.

---

### **Deregistrazione dagli eventi**: 
Gli oggetti che non sono più interessati agli eventi possono deregistrarsi dagli Scriptable Objects corrispondenti. Questo previene eventuali effetti collaterali indesiderati dovuti alla ricezione di eventi non più rilevanti.

---

### TL/DR: 
In sintesi, questo sistema fornisce un modo flessibile e decentralizzato per gestire gli eventi nel gioco, consentendo una maggiore modularità e facilitando la comunicazione tra i vari sistemi senza la necessità di dipendenze dirette.

---
# References
