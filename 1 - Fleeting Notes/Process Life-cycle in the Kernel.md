
**Tags**: #kernel
**Status**: #child 

---

# Memory Layout

Quale è il memory layout di un processo in memoria. Questa è allocata in memoria al kernel e contiene informazioni su tutte le aree di memoria del processo 

La relazione che è presente con una PCB, in particolare questa contiene un riferimento all'area di memoria. Questa gli serve per poter sospendere e riprendere l'esecuzione. Sa cosa deve caricare

Quindi la PCB contiene tutte le informazioni di gestione del processo

In pratica, `task_struct->mm` permette al kernel di dire alla CPU e alla MMU: “Ecco la mappa della memoria di questo processo”.
Viene anche utilizzata per l'allocazione e la deallocazione della memoria 

Quella area è fondamentale per il thread sharing
