# Créer rapidement des documents PDF avec JavaScript

<img src="./img/logo.png" width="300">

## Mise en place de jsPDF

### :one: Importer le CDN de jsPDF
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
```

### :two: Créer un bouton pour générer le PDF
```html
<button id="btnPDF">PDF</button>

<script>
document.getElementById('btnPDF').onclick =()=>{
    // code ici
}
<script>
```

### :three: Importer jsPDF
```js
document.getElementById('btnPDF').onclick =()=>{
    // on importe jsPDF pour pouvoir l'utiliser
    const { jsPDF } = window.jspdf;
}
```

### :four: Création de l'objet jsPDF
```js
document.getElementById('btnPDF').onclick =()=>{
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
}
```
### :five: Changer les valeurs par défault dans le constructeur
```js
const doc = new jsPDF( orientation: 'p',unit: 'mm', format: 'a4');
```
|les termes| les valeurs par default|les valeurs|
|---|---|---|
|orientation|**p**|Orientation du document. Les valeurs possibles sont "**portrait**" ou "**landscape**" (ou les raccourcis "**p**" or "**l**").|
|unit| **mm**|Unité de mesure pour le coordonnées en X et Y ainsi que les dimmensions. Les valeurs possibles sont "**pt**" (points), "**mm**", "**cm**", "**m**", "**in**" ou "**px**".|
|format| **a4** | Les valeurs possibles sont  a0 - a10, b0 - b10, c0 - c10, dl, letter, government-letter, legal, junior-legal, ledger, tabloid, credit-card|

## Mise en place du texte

### Définir la taille de la police de caractère ou "font"
```js
doc.setFontSize(40);
```
### Définir la couleur du texte
en Hexadécimal
```js
doc.setTextColor('#444');
```
en RGBA
```js
doc.setTextColor(68,68,68);
```
ou bien une seule valeur si elle se répète
```js
doc.setTextColor(68);
```
### Afficher du texte
```js
doc.text('Hello PDF',158,40);
```

## Afficher le PDF
Afficher une preview :
```js
doc.output('dataurlnewwindow'); //  data url new window
```
Télécharger :
```js
doc.save(`document.pdf`)
```

## Code complet 

## Ressources et documentation officielle :

- https://github.com/parallax/jsPDF
- https://artskydj.github.io/jsPDF/docs/jsPDF.html
