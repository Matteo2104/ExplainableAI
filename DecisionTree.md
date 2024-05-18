# Decision Tree

| Meteo    | Temperatura | Giocare a Tennis |
| -------- | ----------- | ---------------- |
| Sole     | Caldo       | No               |
| Sole     | Caldo       | No               |
| Nuvoloso | Caldo       | Si               |
| Pioggia  | Mite        | Si               |
| Pioggia  | Freddo      | Si               |
| Pioggia  | Freddo      | No               |
| Nuvoloso | Freddo      | Si               |
| Sole     | Mite        | No               |
| Sole     | Freddo      | Si               |
| Pioggia  | Mite        | Si               |

### Calcolo dell'entropia iniziale

$p_{pos} = \frac{6}{10}$

$p_{neg} = \frac{4}{10}$ 

$H_{init} = -(p_{pos}\log_2 p_{pos} + p_{neg}\log_2 p_{neg}) = 0.97$

L'entropia iniziale fornisce una misura del disordine dei dati: più è alta, maggiore è l'incertezza (?)

### Calcolo della riduzione dell'entropia per l'attributo "Meteo"

##### Sole

$p_{pos} = \{ \frac{n_{Si}}{n_{Sole}} \} = \frac{1}{4}$

$p_{neg} = \{ \frac{n_{No}}{n_{Sole}} \} = \frac{3}{4}$

$H_{Sole} = 0.81$

##### Nuvoloso

$p_{pos} = \{ \frac{n_{Si}}{n_{Nuvoloso}} \} = \frac{2}{2}$

$p_{neg} = \{ \frac{n_{No}}{n_{Nuvoloso}} \} = \frac{0}{0}$ ???

$H_{Nuvoloso} = 0$

##### Pioggia

$p_{pos} = \{ \frac{n_{Si}}{n_{Pioggia}} \} = \frac{3}{4}$

$p_{neg} = \{ \frac{n_{No}}{n_{Pioggia}} \} = \frac{1}{4}$

$H_{Pioggia} = 0.81$

##### Entropia ponderata

$H_{Meteo} = \frac{n_{Sole}}{n_{Tot}}H_{Sole} + \frac{n_{Nuvoloso}}{n_{Tot}}H_{Nuvoloso} + \frac{n_{Pioggia}}{n_{Tot}}H_{Pioggia} = 0.648$

##### Riduzione dell'entropia per "Meteo"

$H_{Rid_{Meteo}} = H_{init} - H_{Meteo} = 0.97 - 0.648 = 0.32$

### Calcolo della riduzione dell'entropia per l'attributo "Temperatura"

$H_{Rid_{Temperatura}} = H_{init} - H_{Temperatura} = 0.97 - 0.87 = 0.1$

### Scelta dell'attributo per la suddivisione

A questo punto si sceglie l'attributo che ha generato la **maggiore** riduzione dell'entropia, che in questo caso è "Meteo", e quindi si userà questo attributo per la suddivisione del set di dati. Si generano quindi 3 nodi

- Nodo "Sole" (3 no, 1 si) - non puro

- Nodo "Nuvoloso" (2 si) - puro 

- Nodo "Pioggia" (3 si, 1 no) - non puro

Siccome ci sono nodi non puri, ripeto il processo su tali nodi utilizzando gli attributi rimanenti (in questo caso solo "Temperatura") fino a che si ottengono tutti nodi puri, oppure fino a che non si soddisfa un certo criterio di arresto (ad esempio la profondità massima dell'albero). In questo caso, procedendo sull'attributo "Temperatura" si otterrebbe l'albero

                  Radice
             /      |       \
          Sole   Nuvoloso  Pioggia
       /    |   \   Si   /    |    \
     Caldo Mite Freddo Caldo Mite Freddo
      No    No    Si    Sì    Sì    No

(Attenzione potrebbe non essere corretto sui nodi foglia)

Quindi se ad esempio venisse fornito un nuovo campione 

| Meteo | Temperatura |
| ----- | ----------- |
| Sole  | Mite        |

Allora si classificherebbe seguendo questa procedura: si parte dal nodo radice e si segue il percorso in base agli attributi, in questo caso il percorso è Radice-> Sole -> Mite -> No. Quindi non si gioca a Tennis.


