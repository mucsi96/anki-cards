# anki-cards
My German Anki cards

## Addon
```python
# C:\Users\mucsi\AppData\Roaming\Anki2\addons21\hello\__init__.py
from anki.hooks import wrap
from aqt import mw
from aqt.main import AnkiQt

def populateDue(self):
    mw.col.db.execute("update notes set flds = (select cards.due || char(31) || substr(notes.flds, instr(notes.flds, char(31)) + 1) from cards where cards.nid = notes.id ) where exists(select 1 from cards where cards.nid = notes.id and cards.type not in (0, 1) ) and notes.mid = 1588525990364")

AnkiQt.onSync = wrap(AnkiQt.onSync, populateDue, "before")
```

## Front Template
```html
{{^due}}
    {{type}}
    {{audio}}
    {{example sentence audio}}
{{/due}}

{{#due}}
    <p>{{type}}</p>
    <p>{{picture}}</p>
    <h1>{{translation}}</h1>
    <p>{{translated example sentence}}</p>
{{/due}}
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
{{^due}}
    <p>{{picture}}</p>
    <h1 id="word">{{word}}</h1>
    <p>{{word forms}}</p>
    <p>{{example sentence}}</p>
    <hr />
    <h1>{{translation}}</h1>
    <p>{{translated example sentence}}</p>
{{/due}}

{{#due}}
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
{{/due}}

<script>
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
