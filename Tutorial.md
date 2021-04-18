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
Deze personen worden getoond in de functie 'astma' en de functie 'Controle'.
Het blazen van deze personen wordt gesimuleerd met de functies 'blazen' en 'blazen2' 
Eerst moeten we onze werkplek wat proper maken, maak de functies overzichtelijker door op de pijltjes te drukken naast de titels. 
Gebruik de balk onderaan om ook de functies helemaal rechts te kunnen zien.

## Step 2
Nu moeten we deze functies activeren. Dit kunnen we doen door een 'druk op a' blok te gebruiken die de functies astma en Controle aanroepen.
```blocks
input.onButtonPressed(Button.A, function () {
    Controle()
    Astma()
})
```
## Step 3
Nu is het aan ons om de datapunten die we binnenkrijgen te versturen naar een 2de microbit.
Dit doen we door de functie 'versturen' te openen en het 'datapunt' te versturen voor de 'persoon'

```blocks
function Versturen () {
    radio.sendValue(Persoon, datapunt)
}
```
## Step  4 
Nu moet enkel een 2de microbit de gegevens die we 'binnenkrijgen' te 'laten zien' wanneer het 'lichtniveau' groter is dan 130. 
```blocks
radio.onReceivedValue(function (name, value) {
    if (input.lightLevel() > 130) {
        serial.writeValue(name, value)
    }
})
```

## Step 5
Goed gedaan, nu kunnen we onze code uittesten!

