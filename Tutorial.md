# Tutorial

```template
function Controle () {
    Persoon = "Controle"
    longcapaciteit_L = 6
    diameter_bronchioli_mm = 1
    Blazen()
    basic.pause(500)
}

function Astma () {
    Persoon = "Asthma"
    longcapaciteit_L = 6
    diameter_bronchioli_mm = 1.2
    Blazen()
    basic.pause(500)
}

function Blazen2 () {
    basic.pause(100 / diameter_bronchioli_mm)
    Versturen()
}

function Versturen () {
    
}

function Blazen () {
    datapunt = 0
    Blazen2()
    for (let index = 0; index <= 7; index++) {
        datapunt = datapunt + longcapaciteit_L * diameter_bronchioli_mm / (index + 1)
        Blazen2()
    }
    for (let index = 0; index < longcapaciteit_L / 2; index++) {
        datapunt += longcapaciteit_L * diameter_bronchioli_mm / 40
        Blazen2()
    }
    for (let index = 0; index < longcapaciteit_L / 2; index++) {
        datapunt += longcapaciteit_L * diameter_bronchioli_mm / -40
        Blazen2()
    }
    while (datapunt > 1.5) {
        datapunt = datapunt - datapunt / 10
        Versturen()
        basic.pause(100)
    }
}

```

# My Tutorial

## Step 1
Tijdens deze tutorial gaan we de data van 2 personen analyseren, iemand met asthma en iemand zonder astma.
Deze personen worden getoond in de functies ``||functions:astma||`` en ``||functions:Controle||``.
Het blazen van deze personen wordt gesimuleerd met de functies ``||functions:blazen||`` en ``||functions:blazen2||`` 
Eerst moeten we onze werkplek wat overzichtelijker maken, maak de functies kleiner door op de pijltjes te drukken naast de titels.
Gebruik de balk onderaan om de functies helemaal rechts ook te kunnen zien.

## Step 2
Nu moeten we deze functies activeren. Dit kunnen we doen door een ``||input:druk op a||`` blok te gebruiken die de functies ``||functions:astma||`` en ``||functions:Controle||`` aanroepen.
```blocks
input.onButtonPressed(Button.A, function () {
    Controle()
    Astma()
})
```
## Step 3
Nu is het aan ons om de datapunten die we binnenkrijgen te versturen naar een 2de microbit.
Dit doen we door de functie ``||functions:versturen||`` te openen en het ``||variables:datapunt||`` te ``||radio:versturen||`` voor de ``||variables:persoon||``

```blocks
function Versturen () {
    radio.sendValue(Persoon, datapunt)
}
```
## Step  4 
Nu moet enkel een 2de microbit de gegevens die we ``||radio:binnenkrijgen||`` te ``||serial:laten zien||`` wanneer het ``||input:lichtniveau||`` ``||logic:groter is dan||``  130. 
```blocks
radio.onReceivedValue(function (name, value) {
    if (input.lightLevel() > 130) {
        serial.writeValue(name, value)
    }
})
```

## Step 5
Goed gedaan, nu kunnen we onze code uittesten!
Wanneer je de ``||functions:astma||`` functie opent kun je de ``||variables:longcapaciteit||`` en de ``||variables:diameter van de bronchioli||`` aanpassen.
probeer de het longvolume eens naar 4 of 8 te brengen en de diameter naar 0.8 of 1.2mm, wat verandert er? 
