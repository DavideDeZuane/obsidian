
### References
- http://www.pluto.it/files/ildp/guide/lfh/x1243.html
- https://linux.die.net/man/5/proc
- https://it.wikipedia.org/wiki/Procfs

Abbreviazione di process file system




Nato principalmente per tracciare i processi in maniera più semplice viene integrato per trattare i processi come file.
In Linux oltre a contenere le informazioni di ogni processo sotto la cartella /proc/PID  include altre informazioni come:
- informazioni sull'hardware
- infromazioni sui moduli caricati 
- l'accesso ai parametri modificabili dinamicamente nel kernel 
- informazioni generiche di sistema 
Gioca un ruolo fondamentale nello scambio di informazioni tra userspace e kernel space. Nella versione 2.6 del kernel buona parte dei file non relativi ai processi sono stati spostati in un'altro pseudo file system sysfs montato sotto /sys

Fondamentalmente ci fornisce una finestra sul funzionamento del kernel.
Ci permette di vedere lo stato interno del kernel al momento in cui lo richiediamo.

Alcuni file consentono di modificare il comportamento del kernel a run-time e si trovano sotto la directory /proc/sys.

- **/proc/sys** → _Pannello di controllo_ del kernel.
- **/sys** → _Mappa dettagliata_ di tutto l’hardware e dei driver del sistema. (è molto più strutturato e gerarchico fornisce più informazioni sull'hardware e i parametri che si possono modificare sono più de idevice che del kerne )

Pseudo-filesystem

diverse utilità di sistema sono delle semplici chiamate a file contenuti in questa directory; per esempio, il comando "lsmod" è lo stesso di "cat /proc/modules" mentre "lspci" è equivalente a "cat /proc/pci". Modificando i file contenuti in questa directory si possono anche leggere o modificare i parametri del kernel (sysctl) mentre il sistema è in esecuzione.


Appunto per il discorso file system virtuale i

```
$ ls -la /proc
dr-xr-xr-x    3 root     root            0 Jan 19 15:00 1
dr-xr-xr-x    3 daemon   root            0 Jan 19 15:00 109
-r--r--r--    1 root     root            0 Jan 19 15:00 cpuinfo
...
-r--------    1 root     root     536809472 Jan 19 15:00 kcore
-r--------    1 root     root            0 Jan 19 14:58 kmsg
-r--r--r--    1 root     root            0 Jan 19 15:00 ksyms
-r--r--r--    1 root     root            0 Jan 19 15:00 loadavg
-r--r--r--    1 root     root            0 Jan 19 15:00 locks
-r--r--r--    1 root     root            0 Jan 19 15:00 mdstat
-r--r--r--    1 root     root            0 Jan 19 15:00 meminfo
-r--r--r--    1 root     root            0 Jan 19 15:00 misc
-r--r--r--    1 root     root            0 Jan 19 15:00 modules
-r--r--r--    1 root     root            0 Jan 19 15:00 mounts
-rw-r--r--    1 root     root          137 Jan 19 14:59 mtrr
dr-xr-xr-x    3 root     root            0 Jan 19 15:00 net
-r--r--r--    1 root     root            0 Jan 19 15:00 pci
dr-xr-xr-x    4 root     root            0 Jan 19 15:00 scsi
dr-xr-xr-x   10 root     root            0 Jan 19 15:00 sys
dr-xr-xr-x    2 root     root            0 Jan 19 15:00 sysvipc
dr-xr-xr-x    4 root     root            0 Jan 19 15:00 tty
-r--r--r--    1 root     root            0 Jan 19 15:00 uptime
-r--r--r--    1 root     root            0 Jan 19 15:00 version
```

