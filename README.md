<p align="center">
  <img src="https://engeto.cz/wp-content/uploads/2019/01/engeto-square.png" width="200" height="200">
</p>

# Java 2 - 6. lekce

## Co nás čeká.. GUI

 - [Úvod](#úvod)
 
 - [GUI vs CLI](#gui-vs-cli)
 
 - [AWT vs Swing vs JavaFX](#awt-vs-swing-vs-javafx)
 
 - [Komponenty](#komponenty)
 
 - [Hledání min](#hledání-min)
 
## Úvod

 GUI (Graphical User Interface - grafické uživatelské rozhraní) představuje způsob ovládání a interakcí s počítačem (a nejen s počítačem) pomocí grafických prvků (např. tlačítka, textové inputy, meníčka, posuvníky, checkboxy..) na obrazovce. S těmito prvky uživatel interaguje pomocí myši (či jinéh polohovacího zařízení) a klávesnice. GUI vzniklo v sedmdesátých letech jako alternativa k příkazovému řádku, který byl do té doby jediným dostupným způsobem ovládání počítače. Ač první GUI bylo stvořeno společností XEROX, tak se o jeho největší rozvoj zašloužily společnosti Microsoft a Apple se svými operačními systémy. Popudem pro vytvoření GUI byla snaha zjednodušit a zintuitivnit práci s počítačem. V současnosti obě možnosti ovládání často koexitjí, ať GUI dosáhlo svého a mezi běžnými uživateli má dominantní postavení. 

## GUI vs CLI
 
 ### GUI
 
  - interakce pomocí ikon a grafických prvků
  - pamětově náročnější
  - uživatelsky přívětivější
  - pomalejší
  - klávesnice + myš
  
  ### CLI
  
  - interakce pomocí textových příkazů zadávaných do konzole
  - méně paměťově náročné
  - uživatelsky náročnější - je třeba znát či vyhledávat přesné názvy příkazů
  - rychlejší
  - klávesnice
  
## AWT vs Swing vs JavaFX

V Javě pro práci s GUI (pro jejich tvorbu) existuje několik knihoven, které nabízí předpřipravené stavební bloky a nástoje pro jeho tvorbu. (další možností je také tvorba GUI v něčem jiném a využití Javy pouze pro backend - zpracování dat, které uživatel zadá, ale toto je mimo rozsah tohoto kurzu).

### AWT

AWT, nebo-li Abstract Window Toolkit je původní knihovnou pro tvorbu grafického uživatelského rozhraní, která byla vyvíjena firmou Sun Microsystems jako součást Javy. První verze vyšla už s první verzí Javy v roce 1995 a ač byla dále vyvíjena, tak v průběhu času začaly na povrch vyplouvat problémy v návrhu - např. to, že ač si Java zakládá na přenositelnosti, tak GUI vytvořené v ATW bylo závislé na platformě. Tato knihovna neměla dlouhého trvání a už v roce 1997 bylo upuštěno od jejího dalšího vývoje a místo ní začal být vyvíjen Swing.

### Swing

Swing je knihovnou, která měla nahradit a i nahradila nevydařený AWT. Je postaven na třídách IFC od Netscape Communications Foundation v roce 1996. O rok později došlo ke spojení Netscape a Sun Microsystems a od tohoto roku (v1.2) je také přímo součástí Javy.

### JavaFX

Podobně jako Swing měl nahradit AWT, tak i JavaFX měla nahradit Swing. Jeho vývoj započal v roce 2008, ale na rozdíl od nahrazení AWT tohle nebylo zcela dokonáno. Hlavním argumentem pro JavaFX je její podpora multimediálních prvků - videa, audia, či různých animací.

## Komponenty

Řekli jsme si, že v Javě máme knihovny usnadňující tvorbu GUI. Jak?

Pro všechny představitelné prvky - existují v knihovnách předpřipravené a konfigurovatelné komponenty a z těchto komponent si skládáme jednotlivé obrazovky, které jsou reprezentované kontejnery (ty jsou taky předpřipravené a konfigurovatelné).

Tedy prvním krokem je vždy vytvoření kontejneru:

```java
JFrame kontejner = new JFrame();
```

Tímto jsme si vytvořili kontejner, do kterého si můžeme naskládat samotné komponenty, ale jak jsme si řelki, tak vše je konfigurovatelné a mnohdy je konfigurace některých hodnot nezbytná.

To si můžete sami vyzkoušet - vytvořte si nový projekt a v main metodě si vytvořte nový JFrame. Vidíte ho? Ne?

K tomu, aby ho šlo vidět, tak je nejprve potřeba nastavit to, že bude viditelný - pomocí metody setVisible.

Teď už vidět jde. Ale co ta velikost?

Tu zase nastavíme pomocí metody setSize. Co vše je potřeba nastavit před tím, než budeme moct tuto naši obrazovku použít? Viditelnost a velikost by mohla stačit.

A co jde nastavit? Vše, na co má [JFrame](https://docs.oracle.com/javase/7/docs/api/javax/swing/JFrame.html) připravené metody.

Jedna z důležitejších věcí, které jdou nastavit, je layout - tedy rozložení jednotlivých komponent v našem kontejneru a stejně jako komponenty, i layouty jsou předpřipravené a konfigurovatlené. Mezi základní patří:

 - BorderLayout - roděluje kontejner na 5 částí, do kterých můžeme komponenty umisťovat - horní, dolní, levá, pravá a střed
 - BoxLayout - skládá komponenty vždy na jeden řádek nebo do jednoho sloupce
 - FlowLayout - skládá komponenty na jeden řádek a když už se na něj nevejdou, tak pokračuje na dalším řádku (připomíná psaní textu a zároveň je defaultním rozložením našeho kontejneru JFrame)
 - GridLayout - rozdělí kontejner na matici s požadovaným počtem řádků a sloupců a do jednotlivých částí postupně skládá jednotlivé komponenty v pořadí v jakém jsou přidávány

A jednotlivé příklady najdete [zde](https://docs.oracle.com/javase/tutorial/uiswing/layout/visual.html).

Máme připravený kontejner s rozložením, tak se pojďme podívat na samotné komponenty.

```java
JButton tlacitko = new JButton();
JTextField textovePole = new JTextField();
```

Komponenty je nejprve potřeba vytvořit.

```java
tlacitko.setSize(120, 50);
tlacitko.setText("Klikni na mě");
textovePole.setEditable(false);
```

Následně nakonfigurovat. (tady je nutno dodat, že neexistuje žádný recept, či seznam 5 metod/věcí, které stačí nastavit - u každé komponenty musíte sami vědět, co chcete, aby (ne)dělala či jak chcete, aby vypada a podle toho si pak najít v dokumentaci tu správnou metodu -  jsou jich minimálně desítky, možná stovky, takže hledání se nevyhnete)

```java
kontejner.add(tlacitko);
kontejner.add(textovePole);
```

A nekonec přidat do nějakého kontejneru.

Máme obrazovku s tlačítkem a s textovým polem. A když na tlačítko klikneme, tak se.. nestane nic.

Pokud je, či jakoukoli jinou komponentu chceme "oživit", tak budeme potřebovat event listenery. Event listenery jsou rozhraní, které vřdy pro nějaký soubor událostí předepisují metody, které odpovídají situacím, které mohou nastat (stisk klávesy, najetí myší, klik, zobrazení..). Implementaci tohoto rozhraní pak předáme naší komponentě, a když nastane nějaká z námi ošetřených událostí, tak se provede kód, který jsme napsali do příslušné metody. Event listenery jsou opět předpřipravené, takže stačí vědět, jaké událsti chcete ošetřovat a pak si můžete najít ten již předpřipravený event listener.

My máme v našem kontejneru tlačítko, tak se pojďme podívat na event listener ošetřující základní události spojené s interakcí s tlačítkem - [MouseListener](https://docs.oracle.com/javase/7/docs/api/java/awt/event/MouseListener.html): 

```java
public interface MouseListener extends EventListener {

    /**
     * Invoked when the mouse button has been clicked (pressed
     * and released) on a component.
     * @param e the event to be processed
     */
    public void mouseClicked(MouseEvent e);

    /**
     * Invoked when a mouse button has been pressed on a component.
     * @param e the event to be processed
     */
    public void mousePressed(MouseEvent e);

    /**
     * Invoked when a mouse button has been released on a component.
     * @param e the event to be processed
     */
    public void mouseReleased(MouseEvent e);

    /**
     * Invoked when the mouse enters a component.
     * @param e the event to be processed
     */
    public void mouseEntered(MouseEvent e);

    /**
     * Invoked when the mouse exits a component.
     * @param e the event to be processed
     */
    public void mouseExited(MouseEvent e);
}
```

Jak vidíme, tak rozhraní pro ošetření událostí myši má šest metod - u každé je popsáno, jakou událost ošetruje - např. mouseClicked ošetřuje klik myší na té naší komponentě. Na nás je připravit implementaci tohoto rozhraní a to předat naší komponentě:

```java
tlacitko.addMouseListener(new MouseListener() {
                    @Override
                    public void mouseClicked(MouseEvent e) {
                      // sem přijde kód, který se provede, když někdo klikne na naše tlačíko
                    }

                    @Override
                    public void mousePressed(MouseEvent e) {
                      // sem přijde kód, který se provede, když někdo stiskne tlačítko myši nad naším tlačítkem
                    }

                    @Override
                    public void mouseReleased(MouseEvent e) {
                      // sem přijde kód, který se provede, když někdo pustí tlačítko myši nad naším tlačítkem
                    }

                    @Override
                    public void mouseEntered(MouseEvent e) {
                      // sem přijde kód, který se provede, když myší najedeme na naše tlačítko
                    }

                    @Override
                    public void mouseExited(MouseEvent e) {
                      // sem přijde kód, který se provede, když myší z našeho tlačítka odjedeme
                    }
                });
```

Nemusíte ošetřit všechny události - ale tím, že jde o implementaci nějakého interface, tak metody tam budete mít všechny, jen jejich tělo můžete ponechat prázdné.

Pokud bychom chtěli ošetřit pouze událst kliknutí, tak by naše metoda mouseClicked mohla vypadat takto:

```java
@Override
public void mouseClicked(MouseEvent e) {
  textovePole.setText("Ahoj světe!");
  tlacitko.setText("Už na mě neklikej.");
}
```

Takto se nám při kliknutí na naše tlačítko vypíše do textového pole požadovaný text a také se změní text na tlačítku.

Ještě zbývá dodat, že v události, kterou dostanou naše metody na ošetřování událostí jako parametr, bývají různé užitečné informace - třeba která klávesa byla stisknuta, když ošetřujeme stisk kláves, kterým tlačítkem myši jsme klikli, atd.

## Hledání min

Jako praktické cvičení si společně naprogramujeme základní verzi hledání min.

Co budeme potřebovat vyřešit?

#### Herní pole

Začneme tím, že si vytvoříme reprezentaci našeho herního pole - potřebujeme dvourozměrnou herní plochu a u každého pole nám bude zatím stačit evidovat to, jestli se na něm nachází mina, nebo ne -> true / false -> boolean.

Herní pole tedy budeme reprezentovat dvourozměrným polem booleanů.

```java
private boolean[][] minefield;
```

Pro toto minové pole budeme mít vlastní třídu, takže v konstruktoru nás čeká inicializace tohoto pole a také jeho naplnění:

```java
public PlayField(int xSize, int ySize, int numberOfMines) {
    minefield = new boolean[xSize][ySize];
    this.xSize = xSize;
    this.ySize = ySize;
    openFields = xSize * ySize - numberOfMines;
    Random random = new Random();
    for (int i = 0; i < numberOfMines;) {
        int randomX = random.nextInt(xSize);
        int randomY = random.nextInt(ySize);
        if (!minefield[randomX][randomY]) {
            minefield[randomX][randomY] = true;
            i++;
        }
    }
}
```
Jako parametry si budeme předávat rozměry herního pole a počet min a krom atributu playfield nám přibudou také atributy pro x rozměr a y rozměr a počet políček, které zbývá odhalit, aby hráč vyhrál - tedy:
```java
private int xSize;
private int ySize;
private int openFields;
```
Do polí, které zbývá zbývá odhalit, si v konstruktoru předvyplníme počet polí bez min, který se rovná velikosti herního pole (xSize * ySize) a odečteme počet min.

Po vytvoření herního pole je potřebujeme naplnit určeným počtem min (ve složitejších variacích na hledání min tento krok probíhá až potom, co uživatel klikne na první pole, protože u nich platí pravidlo, že pod prvním odhaleným polem nikdy nemůže být mina).

To naplnění provedeme v cyklu:
```java
for (int i = 0; i < numberOfMines;) {
    int randomX = random.nextInt(xSize);
    int randomY = random.nextInt(ySize);
    if (!minefield[randomX][randomY]) {
        minefield[randomX][randomY] = true;
        i++;
    }
}
```

Dokud jsme nevygenerovali požadovaný počet min, tak si vždy vygenerujeme náhodnou pozici na herním poli a ověříme, že tam mina ještě není - pokud tam není, tak ji tam přidáme a zvýšíme počet mit, které jsme už rozložili, jinak zkusíme vygenerovat nové souřadnice.

Dále budeme potřebovat 4 metody:

 - metodu na ověření, jestli na určeném herním poli je, nebo není mina

 - metodu a spočítání sousedních polí, na kterých je mina (pokud klikneme na pole, na kterém není mina, tak zobrazíme informaci o tom, na kolika sousedních polích jsou miny)

 - metodu na zjištění, jestli jsme už vyhráli

 - metodu na snížení počtu polí bez min, které nám zbývá objevit

```java
public boolean isThereMine(int x, int y) {
    return minefield[x][y];
}
```

Metoda na ověření, jestli na určeném herním poli je, nebo není mina je naprosto jednoduchá - vrátíme prostě hodnotu z určené pozice na našem herním plánu.

Podobně jednoduché jsou i metody na zjištění, jestli jsme už vyhráli a snížení počtu polí, které ještě musíme objevit:
```java
public boolean hasWon() {
    return openFields == 0;
}

public void decrementOpenFields() {
    openFields = openFields - 1;
}
```

Metoda na zjištění počtu sousedů s minou bude na první pohled vypadat složitě:
```java
public int getNeighboursWithMine(int x, int y) {
    int mineCount = 0;

    // levy horni
    if (x > 0 && y > 0 && minefield[x-1][y-1]) mineCount++;

    // horni
    if (y > 0 && minefield[x][y-1]) mineCount++;

    // pravy horni
    if (x < xSize - 1 && y > 0 && minefield[x+1][y-1]) mineCount++;

    // levy
    if (x > 0 && minefield[x-1][y]) mineCount++;

    // pravy
    if (x < xSize - 1 && minefield[x+1][y]) mineCount++;

    // levy dolni
    if (x > 0 && y < ySize - 1 && minefield[x-1][y+1]) mineCount++;

    // dolni
    if (y < ySize - 1 && minefield[x][y+1]) mineCount++;

    // pravy dolni
    if (x < xSize - 1 && y < ySize -1 && minefield[x+1][y+1]) mineCount++;

    return mineCount;
}
```
Ale jediné, co děláme, že pro každého souseda nejdřív ověříme, jestli vůbec existuje, abychom nedostali [IndexOutOfBOundsException](https://docs.oracle.com/javase/7/docs/api/java/lang/IndexOutOfBoundsException.html) pokud bychom se pokusili získat hodnotu mimo herní plán - např. herní pole v levém horním rohu už nemá žádného levého souseda.. a pokud toto herní pole existuje, tak zjistíme, jestli na něm je mina a když ano, tak inkementujeme náč čitač.

Tímto máme hotovou naši pomocnou třídu pro herní plán a zbývá nám grafické rozhraní, tak se do něj pojďme pustit.

#### Grafické rozhraní

To vygenerujeme v prozatím rovnou v main metodě a kód bude vypadat nějak takto:

```java
public static void main(String[] args) {

    int xSize = 5;
    int ySize = 5;
    int numberOfMines = 5;

    JFrame frame = new JFrame();
    frame.setVisible(true);
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    frame.setSize(xSize * 80, ySize * 80);

    GridLayout layout = new GridLayout(ySize, xSize);

    frame.setLayout(layout);

    PlayField playField = new PlayField(xSize, ySize, numberOfMines);

    for (int y = 0; y < ySize; y++) {
        for (int x = 0; x < xSize; x++) {
            JButton button = new JButton();
            button.setBackground(Color.LIGHT_GRAY);
            button.setOpaque(true);
            int finalX = x;
            int finalY = y;
            button.addMouseListener(new MouseListener() {
                @Override
                public void mouseClicked(MouseEvent e) {
                    if (SwingUtilities.isLeftMouseButton(e)) {
                        if (button.getText() != "?") {
                            if (playField.isThereMine(finalX, finalY)) {
                                button.setBackground(Color.RED);
                                button.setText("X");
                                JOptionPane.showMessageDialog(frame, "You lost, better luck next time.");
                            } else {
                                button.setBackground(Color.white);
                                button.setText(String.valueOf(playField.getNeighboursWithMine(finalX, finalY)));
                                playField.decrementOpenFields();
                                if (playField.hasWon()) {
                                    JOptionPane.showMessageDialog(frame, "Congratulations, you won!");
                                }
                            }
                            button.setEnabled(false);
                        }
                    }
                    if (SwingUtilities.isRightMouseButton(e)) {
                        if (button.getText() == "?") {
                            button.setText("");
                            button.setBackground(Color.LIGHT_GRAY);
                        } else {
                            button.setText("?");
                            button.setBackground(Color.YELLOW);
                        }
                    }
                }

                @Override
                public void mousePressed(MouseEvent e) {

                }

                @Override
                public void mouseReleased(MouseEvent e) {

                }

                @Override
                public void mouseEntered(MouseEvent e) {

                }

                @Override
                public void mouseExited(MouseEvent e) {

                }
            });
            frame.add(button);
        }
    }

}
```

Pojďme si ho projít po kouscích:

```java
int xSize = 5;
int ySize = 5;
int numberOfMines = 5;
```

Nejdříve si vytvoříme tři pomocné proměnné (tyto hodnoty bychom mohli v budoucnu získávat od uživatele, ale my zatím použijeme předdefinované hodnoty).

```java
JFrame frame = new JFrame();
frame.setVisible(true);
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setSize(xSize * 80, ySize * 80);

GridLayout layout = new GridLayout(ySize, xSize);

frame.setLayout(layout);
```

Dále si vytvoříme kontejner (JFrame) do kterého bueme umisťovat naše komponenty a nastavíme mu několik důležitých atributů
 - viditelnost (default je false, takže pokud chceme, aby naše herní plocha šla vidět, nastavíme na true)
 - co se stane při stisku tlačítka "zavřít" (defaultní chování je, že se okno pouze minimalizuje - my si nastavíme, že chceme, aby se na naše appka ukončila)
 - rozměr - v našem případě to bude rozměr herního pole vynásobený velikostí tlačítka
 - a nakonec rozložení prvků v našem kontejneru - my jsme si vybrali GridLayout, protože odpovídá právě tomu rozložení, které se snažíme dosáhnout

Vytvoříme si instanci našeho herního plánu:
```java
PlayField playField = new PlayField(xSize, ySize, numberOfMines);
```

A pustíme se do generování tlačítek - pro grafickou reprezentaci herního plánu bychom mohli zvolit mnoho postupů, ale ten nejjednodušší a nejintuitivnější je, že každé pole herního plánu bude reprezentováno jedním tlačítkem (chceme aby na ně šlo klikat, chceme zobrazovat různé barvy, popisy a chceme býn schopni prvkek, na který už bylo kliknuto, disablovat - vše, co už umí komponenta [JButton](https://docs.oracle.com/javase/7/docs/api/javax/swing/JButton.html))

```java
for (int y = 0; y < ySize; y++) {
  for (int x = 0; x < xSize; x++) {
      JButton button = new JButton();
      button.setBackground(Color.LIGHT_GRAY);
      button.setOpaque(true);
      frame.add(button);
  }
}
```

Postupně v cyklech procházíme herní plán a pro každou pozici vygenerujeme tlačítko, nastavíme mu základní barvu a přidáme ho do kontejneru.
Voila, máme hotovo.
Teda s skoro hotovo, prrotože naše tlačítka nic nedělají.
Pojďme jim tedy přidat event listenery ošetřující události, které nás zajímají.
Vzhledem k tomu, že chceme ošetřovat poze kliknutí myší, použijeme [MouseListener](https://docs.oracle.com/javase/7/docs/api/java/awt/event/MouseListener.html).

```java
button.addMouseListener(new MouseListener() {
    @Override
    public void mouseClicked(MouseEvent e) {

    }

    @Override
    public void mousePressed(MouseEvent e) {

    }

    @Override
    public void mouseReleased(MouseEvent e) {

    }

    @Override
    public void mouseEntered(MouseEvent e) {

    }

    @Override
    public void mouseExited(MouseEvent e) {

    }
});
```

Vidíme, že rozhraní MouseListener má několik předpřipravených metod pro události, které mohou nastat ve spojistosti s práci s myší - my chceme ušetřovat kliknutí myší, což znamená, že musíme přidat implementaci metody mouseClicked - což bude právě to, co se při kliku myší stane.

První věcí, které si můžeme všimnout, je to, že máme jednu metodu pro klik myší, ale my chceme ošetřovat (a hlavně rozlišovat) klik levým tlačítkem (odhalení políčka) a klik pravým tlačítkem (označení a odoznačení políčka o kterém si myslíme, že se pod ním ukrývá mina).

Abychom toho dosáhli, potřebujeme nějak rozlišit to, jaké tlačítko způsobilo tu událost mouse clicked - tato informace je schovaná v tom jednom parametru, který dostaneme - MouseEvent - ale protože rozlišování toho, kterým tlačítkem bylo kliknuto, je něco natolik běžného, nemusíme tuto informaci sami dolovat a můžeme použít dvě motedy v utitily třídy pro Swing - [SwingUtilities](https://docs.oracle.com/javase/7/docs/api/javax/swing/SwingUtilities.html) půjde o metody isLeftMouseButton a isRightMouseButton, kterým jako parametr předáme tu naši událost (MouseEvent) a ony nám řeknou, jestli šlo o pravý / levý klik.

```java
if (SwingUtilities.isRightMouseButton(e)) {
    if (button.getText() == "?") {
        button.setText("");
        button.setBackground(Color.LIGHT_GRAY);
    } else {
        button.setText("?");
        button.setBackground(Color.YELLOW);
    }
}
```

Pravý klik bude jednodušší. Ten slouží pouze k označení a odoznačení pole, o kterém si myslíme, že by pod ním mohla být mina - označené políčko má v popisku otazník, takže v podstatě jedíné, co děláme, je, že když na políčku je otazník, tak ho odstraníme a naopak. Pro přehlednost tomu políčku ještě meníme barvu pozadí - toť vše.

```java
if (SwingUtilities.isLeftMouseButton(e)) {
    if (button.getText() != "?") {
        if (playField.isThereMine(finalX, finalY)) {
            button.setBackground(Color.RED);
            button.setText("X");
            JOptionPane.showMessageDialog(frame, "You lost, better luck next time.");
        } else {
            button.setBackground(Color.white);
            button.setText(String.valueOf(playField.getNeighboursWithMine(finalX, finalY)));
            playField.decrementOpenFields();
            if (playField.hasWon()) {
                JOptionPane.showMessageDialog(frame, "Congratulations, you won!");
            }
        }
        button.setEnabled(false);
    }
}
```

Pro levé tlačítko nás čeká samotné objevování - při kliku na políčko (pokud není označené) se podíváme, jestli pod ním je a nebo není mina - když tam mina je, tak tlačítku nastavíme červenou barvu a Xko jako text. Také zobrazíme hlášku (pomocí JOptionPane.showMessageDialog) ve které uživatele informujeme o tom, že prohrál.

Pokud pod políčkem mina nebyla, tak si zjistíme, na kolika sousedních polích je mina (použijeme metodu, kterou jsme si připravili v naší pomocné třídě) a toto číslo zobrazíme na políčku, použijeme také pomocnou metodu pro snížení počtu políček, které nám zbývá prozkoumat a nakonec se dotážeme, jestli jsme už náhodou nevihrali (opět pomocí naší metody, kterou jsme si připravili) a pokud jsme vyhráli, tak zobrazíme dialog s touto informací  - stejně, jako jsme zobrazovali hlášku pro prohru.

Nakonec toto tlačítko disablujeme pomocí metody setEnabled - jednou objevené políčko už má být neklikatelné.

A tímto jsme stvořili základní implementaci hledání min.
