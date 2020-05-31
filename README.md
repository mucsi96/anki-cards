# anki-cards
My German Anki cards

## Addon
```python
# C:\Users\mucsi\AppData\Roaming\Anki2\addons21\hello\__init__.py
from anki.hooks import wrap
from aqt.main import AnkiQt
from anki.consts import CARD_TYPE_NEW, CARD_TYPE_LRN, CARD_TYPE_REV, CARD_TYPE_RELEARNING

def populateDue(self):
    model = self.col.models.byName("recall + listening pro")

    def isDueField(field):
        return field.get('name') == 'due'

    if model:
        mid = model.get('id')
        flds = model.get('flds')
        dueIndex = next(i for i,v in enumerate(flds) if isDueField(v))
        for nid in self.col.findNotes('mid:{}'.format(mid)):
            note = self.col.getNote(nid)
            card = note.cards()[0]
            if (card.type in (CARD_TYPE_NEW, CARD_TYPE_LRN)):
                note.fields[dueIndex] = ''
            if (card.type in (CARD_TYPE_REV, CARD_TYPE_RELEARNING)):
                note.fields[dueIndex] = '{}'.format(card.due)
            note.flush()

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
