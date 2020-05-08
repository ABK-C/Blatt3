Sie finden diese Aufgabe auf github:
<https://classroom.github.com/g/GBlMdMbp>.

Vergleichen Sie die Häufigkeit der Zahlen in **datensumme.txt** mit den
Vorhersagen der Poissonverteilung. Bitte schreiben Sie Ihren Code in die
Datei: **poisson.cc**

Zählen Sie mit einem **std::vector\<int\>**, wie oft die Werte <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/63bb9849783d01d91403bc9a5fea12a2.svg?invert_in_darkmode" align=middle width=9.075367949999992pt height=22.831056599999986pt/> von 0
bis 10 in der Datei vorkommen. Binden Sie dafür die entsprechende
Include-Datei mit

    #include<vector>
    using namespace std;

ein. Erzeugen Sie ein vector-Objekt mit elf
Einträgen:`vector<int> zaehler(11);` Lesen Sie dann alle <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/ee096a83eb47b7110b5a33bfc426c09a.svg?invert_in_darkmode" align=middle width=61.57522799999998pt height=22.465723500000017pt/>
Zahlenwerte <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/de3e4ddbaf93c2db6b330ad1998cc995.svg?invert_in_darkmode" align=middle width=14.517775799999992pt height=14.15524440000002pt/> aus **datensumme.txt** und erhöhen Sie immer den
entsprechenden Eintrag im Vektor:

    zaehler[zahl] += 1;

Geben Sie am Ende alle Einträge im Vektor `zaehler` aus.

Erzeugen Sie nun eine Datei **hist.txt** mit den Ergebnissen aus a) im
Format:

    0 12
    1 23
    2 53
    ...

Stellen Sie die Werte als Histogramm da, indem Sie im Terminal
**gnuplot** starten und im Programm

    plot "./hist.txt"  smooth freq with boxes

eingeben. (Mit `quit` beenden Sie **gnuplot**.) Altnativ können Sie eine
Online-Version von gnuplot nutzen: <http://gnuplot.respawned.com/>.
Kopieren Sie Ihre Datenwerte in das obere Textfenster und geben im
darunter liegenden folgendes ein:

    set terminal svg size 400,300 enhanced fname 'arial'  fsize 10 butt solid
    set output 'out.svg'
    plot  "data.txt" using 1:2 smooth freq with boxes

Schreiben Sie eine Funktion `double poisson(double mu, int k)`, die die
Poissonwahrscheinlichkeit <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/5845a949f6a6306bf1a27da558b4a2dd.svg?invert_in_darkmode" align=middle width=113.92509974999999pt height=36.003597300000024pt/>
berechnet. Benutzen Sie als Implementation der Exponentialfunktion die
Funktion `double exp(double x)` aus **cmath** und die Funktion
`double pow(double x, double k)` für <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/ca258fdb5aa2e16d091da2d680a2bc60.svg?invert_in_darkmode" align=middle width=16.66101689999999pt height=27.91243950000002pt/>. Die Fakultät können Sie über
die Gammafunktion <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/fcb4a7f74000c59d93109a045908527f.svg?invert_in_darkmode" align=middle width=96.00441674999998pt height=24.65753399999998pt/> (`double tgamma(double x)` in
**cmath**) berechnen.\
Schreiben Sie eine neue Datei **histpoi.txt**, die in einer dritten
Spalte die Erwartung aus der Poissonverteilung <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/5c342325885f39867f8d7514b927763c.svg?invert_in_darkmode" align=middle width=78.78032579999999pt height=24.65753399999998pt/>
enthält. Verwenden Sie den Mittelwert aus Blatt 2 als <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/> der
Poissonverteilung (3,11538).\
Vergleichen Sie die Werte und die Vorhersagen mit **gnuplot**:\
`plot "./histpoi.txt" using 1:2, ''./histpoi.txt" using 1:3 smooth freq with boxes`

Wir wollen nun den Wert von <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/> aus den Daten mit der
[Maximum-Likelihood-Methode](https://de.wikipedia.org/wiki/Maximum-Likelihood-Methode)
abschätzen. Zudem wollen wir die Übereinstimmung mit der
Poisson-Hypothese quantifizieren. Hierzu nutzen wir die
Log-Likelihood-Funktion
([Likelihood-Quotienten-Test](https://de.wikipedia.org/wiki/Likelihood-Quotienten-Test))
und deren Beziehung zur <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/a67d576e7d59b991dd010277c7351ae0.svg?invert_in_darkmode" align=middle width=16.837900199999993pt height=26.76175259999998pt/>-Verteilung. Bitte schreiben Sie Ihren
Code in die Datei: **likelihood.cc**

Berechnen Sie zunächst die Gesamtwahrscheinlichkeit, die 234 Zahlenwerte
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/de3e4ddbaf93c2db6b330ad1998cc995.svg?invert_in_darkmode" align=middle width=14.517775799999992pt height=14.15524440000002pt/> erhalten: <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/a7118cd9ce1a28744aa9cbd13e7cc4b5.svg?invert_in_darkmode" align=middle width=154.50014579999998pt height=31.36100879999999pt/>, wenn
die Annahme der Poissonverteilung stimmt. Speichern Sie hierzu alle
Werte aus "datensumme.txt" in einem Vektor **std::vector\<int\>
daten**.\
Benutzen Sie **daten.push\_back(zahl)**, um den Wert der Variable
**zahl** zum Vektor hinzuzufügen.\
Schreiben Sie nun eine Funktion
`double prob(std::vector<int> daten, double mu)`, die die Likelihood,
also die Wahrscheinlichkeit
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/c947a8851f5423b5172592819f209215.svg?invert_in_darkmode" align=middle width=124.85689754999999pt height=36.003597300000024pt/>, die Daten
mit einem bestimmten <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/> zu erhalten, berechnet.

Zum Iterieren über die Werte in **daten** nutzen Sie:

    for(int k : daten) {
      ...
    }

Geben Sie die Wahrscheinlichkeit für <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/f9e5bca355be99e2834db8dd2ae3ed42.svg?invert_in_darkmode" align=middle width=85.70403599999999pt height=21.18721440000001pt/> (Mittelwert der
Stichprobe) aus. Es sollte <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/ff883d06bbdd96845f0668bac63e0b20.svg?invert_in_darkmode" align=middle width=112.12354229999998pt height=26.76175259999998pt/> herauskommen.

Schreiben Sie nun für <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/>-Werte zwischen 0 und 6 eine Datei
"likelihood.txt" mit den Wertepaaren <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/> und <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/5c67e215c21977c193cc27fd2e1c9392.svg?invert_in_darkmode" align=middle width=34.028301449999994pt height=24.65753399999998pt/>.
Tasten Sie <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/> mit einer Schrittweite von 0.1 ab. Stellen Sie die
Werte als Graph da, indem Sie im Terminal **gnuplot** starten und im
Programm `plot "likelihood.txt"  with line` eingeben. (Mit `quit`
beenden Sie **gnuplot**.)\
Verringern Sie die Schrittweite, um ein schöneres Bild zu erhalten. Was
sehen Sie?\
Finden Sie über das Maximum des Likelihood den besten Schätzwert für
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/>.\
(Mit `plot [xmin:xmax] "likelihood.txt"  with line` können Sie nur einen
Ausschnitt in <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/332cc365a4987aacce0ead01b8bdcc0b.svg?invert_in_darkmode" align=middle width=9.39498779999999pt height=14.15524440000002pt/> des Graphen darstellen.)

Schreiben Sie nun eine zweite Datei "nll.txt" mit den Wertepaaren <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/>
und <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/d2a4c8dba7fab920b1638ee808b147cc.svg?invert_in_darkmode" align=middle width=74.21093459999999pt height=24.65753399999998pt/>, dem negativen Log-Likelihood. Benutzen
Sie die `log`-Funktion aus **cmath**. Erzeugen Sie auch für diese Werte
einen Graph mit **gnuplot**.

Der Mittelwert der Stichprobe sollte ein guter Schätzwert für <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/>
sein. Ziehen Sie nun beim Schreiben der Datei "deltanll.txt"
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/310e44ae6e4c669a3a9eac3ef24d8e3c.svg?invert_in_darkmode" align=middle width=118.1874903pt height=24.65753399999998pt/> vom negativen Log-Likelihood
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/d2a4c8dba7fab920b1638ee808b147cc.svg?invert_in_darkmode" align=middle width=74.21093459999999pt height=24.65753399999998pt/> ab. Erzeugen Sie wiederum einen Graph mit
**gnuplot**.\
Mit `plot [xmin:xmax][ymin:ymax] "deltanll.txt"  with line` können Sie
nur einen Ausschnitt des Graphen darstellen.\
Finden Sie über das Minimum des negativen Log-Likelihood den besten
Schätzwert für <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/>. Bestimmen Sie den Fehler auf den geschätzten
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/07617f9d8fe48b4a7b3f523d6730eef0.svg?invert_in_darkmode" align=middle width=9.90492359999999pt height=14.15524440000002pt/>-Wert, indem Sie das Intervall finden, in dem
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/ca1a9c644edf17857c6f651956b9fd10.svg?invert_in_darkmode" align=middle width=65.99172524999999pt height=24.65753399999998pt/> um weniger als 1,0 größer als im Minimum ist.

Da diese Gesamtwahrscheinlichkeit immer kleiner wird, je mehr
Zahlenwerte betrachtet werden, teilt man diese Likelihood für eine
Poissonverteilung mit <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/f9e5bca355be99e2834db8dd2ae3ed42.svg?invert_in_darkmode" align=middle width=85.70403599999999pt height=21.18721440000001pt/> durch die bestmögliche
Poissonwahrscheinlichkeit, nämlich jener, wenn für jede einzelne Zahl
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/735e10d6dc3358e7402be4d93a7e85bf.svg?invert_in_darkmode" align=middle width=46.340330849999994pt height=14.15524440000002pt/> angenommen wird. Berechnen Sie den Likelihood-Quotienten:
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/9ea887b49f29fcbe054c68026d8bdc35.svg?invert_in_darkmode" align=middle width=246.83521994999998pt height=31.36100879999999pt/>
und geben Sie den Wert aus.\
Wenn die Annahme einer Poissonverteilung stimmt, sollte <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/4943210a45a87ff18a8da35abb418fb9.svg?invert_in_darkmode" align=middle width=51.598177949999986pt height=22.831056599999986pt/>
gemäß einer
[<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/a67d576e7d59b991dd010277c7351ae0.svg?invert_in_darkmode" align=middle width=16.837900199999993pt height=26.76175259999998pt/>-Verteilung](https://de.wikipedia.org/wiki/Chi-Quadrat-Verteilung)
mit <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/2fe9f8f16ec7d5a2ddef7a4621c9316a.svg?invert_in_darkmode" align=middle width=75.15227939999998pt height=21.18721440000001pt/> Freiheitsgraden verteilt sein. Für eine Zahl
an Freiheitsgraden größer 100 sollte die <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/a67d576e7d59b991dd010277c7351ae0.svg?invert_in_darkmode" align=middle width=16.837900199999993pt height=26.76175259999998pt/>-Verteilung einer
Normalverteilung mit Mittelwert <img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/0a80e9792dfd572b28b48a6eaa670d56.svg?invert_in_darkmode" align=middle width=28.674081149999992pt height=14.15524440000002pt/> und Standardabweichung
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/963b642a9f224c55585a717762056004.svg?invert_in_darkmode" align=middle width=50.59196339999999pt height=26.045612999999992pt/> entsprechen. Berechnen Sie die relative
Abweichung Ihres Likelihood-Quotienten vom Mittelwert:
<img src="https://rawgit.com/ABK-C/Blatt3/master/svgs/ccbc3b110106bd85c9fa09c300e36ade.svg?invert_in_darkmode" align=middle width=97.85380109999997pt height=29.662026899999994pt/>.
Benutzen Sie die `sqrt`-Funktion aus **cmath**.
