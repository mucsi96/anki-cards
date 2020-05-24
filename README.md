# anki-cards
My German Anki cards

## Front Template
```html
<template id="listening">
    {{type}}
    {{audio}}
    {{example sentence audio}}
</template>

<template id="recall">
    <p>{{type}}</p>
    <p>{{picture}}</p>
    <h1>{{translation}}</h1>
    <p>{{translated example sentence}}</p>
</template>

<div id="card"></div>

<script>
    const card = document.getElementById('card');
    const listeningTemplate = document.getElementById('listening');
    const recallTemplate = document.getElementById('recall');

    if ("{{Tags}}".split(' ').includes('new')) {
        card.innerHTML = listeningTemplate.innerHTML;
    } else {
        card.innerHTML = recallTemplate.innerHTML;
    }
</script>
```

## Styling (shared between cards)
```css
.card {
    font-family: arial;
    font-size: 20px;
    text-align: center;
    color: black;
    background-color: white;
}

.card1 {
    background-color: #FFFFFF;
}

.card2 {
    background-color: #FFFFFF;
}

.der {
    color: #0074D9;
}

.die {
    color: #FF4136;
}

.das {
    color: #2ECC40;
}
```

## Back Template
```html
<template id="listening">
    <p>{{picture}}</p>
    <h1 id="word">{{word}}</h1>
    <p>{{word forms}}</p>
    <p>{{example sentence}}</p>
    <hr />
    <h1>{{translation}}</h1>
    <p>{{translated example sentence}}</p>
</template>

<template id="recall">
    <p>{{type}}</p>
    <p>{{picture}}</p>
    <h1>{{translation}}</h1>
    <p>{{translated example sentence}}</p>
    <hr>
    <h1 id="word"> {{word}}</h1>
    <p>{{word forms}}</p>
    <p>{{example sentence}}</p>
    {{audio}}
    {{example sentence audio}}
</template>

<div id="card"></div>

<script>
    const card = document.getElementById('card');
    const listeningTemplate = document.getElementById('listening');
    const recallTemplate = document.getElementById('recall');

    if ("{{Tags}}".split(' ').includes('new')) {
        card.innerHTML = listeningTemplate.innerHTML;
    } else {
        card.innerHTML = recallTemplate.innerHTML;
    }

    const word = document.getElementById('word');

    if (word) {
        if ("{{word}}".match(/der/i)) {
            word.classList.add('der');
        }
        if ("{{word}}".match(/die/i)) {
            word.classList.add('die');
        }
        if ("{{word}}".match(/das/i)) {
            word.classList.add('das');
        }
    }
</script>
```
