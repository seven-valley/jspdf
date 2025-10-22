# Créer rapidement des documents PDF avec JavaScript

<img src="./img/logo.png" width="300">

_Installer le plugin Live server sur vs code_
  
https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer

## 1 - Mise en place de jsPDF

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
</script>
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
const doc = new jsPDF({orientation: 'p',unit: 'mm', format: 'a4'});
```
|les termes| les valeurs par default|les valeurs|
|---|---|---|
|orientation|**p**|Orientation du document. Les valeurs possibles sont "**portrait**" ou "**landscape**" (ou les raccourcis "**p**" or "**l**").|
|unit| **mm**|Unité de mesure pour le coordonnées en X et Y ainsi que les dimmensions. Les valeurs possibles sont "**pt**" (points), "**mm**", "**cm**", "**m**", "**in**" ou "**px**".|
|format| **a4** | Les valeurs possibles sont  a0 - a10, b0 - b10, c0 - c10, dl, letter, government-letter, legal, junior-legal, ledger, tabloid, credit-card|

## 2 - Mise en place du texte

### Définir la taille de la police de caractère ou "font"
```js
doc.setFontSize(40);
```

### Définir la couleur du texte
En Hexadécimal
```js
doc.setTextColor('#444');
```
En RGBA
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
doc.save(`document.pdf`);
```

## 3- Code complet pour un "Hello world"
<code>demo1.html</code>

```html
<button id="btnPDF">PDF</button>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script>
document.getElementById('btnPDF').onclick =()=>{
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    doc.setFontSize(40);
    doc.setTextColor('#444');
    doc.text('Facture',158,40); 
    doc.output('dataurlnewwindow'); // data url new window
    //doc.save(`document.pdf`);
}
</script>
```

## 4 - Ajouter une forme
- Choisir une couleur pour la forme

```js
doc.setFillColor(233);
```
ou
```js
doc.setFillColor(233,233,233);
```
ou
```js
doc.setFillColor('#e9e9e9');
```
-----------------------------------
- Dessiner un rectangle
(X,Y,largeur,hauteur,remplissage) 
- remplissage : "F" = fill (rempli)
- remplissage : "S" = stroke (mettre un cadre)
- remplissage : "FD" =  (mettre un cadre et remplir)

```js
doc.rect(40,100,100,10,"F");
```
[doc](https://artskydj.github.io/jsPDF/docs/jsPDF.html#rect)

## 5 - Code complet pour un "Hello world" avec création d'une forme
<code>demo2.html</code>

```html

<button id="btnPDF">PDF</button>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

<script>
document.getElementById('btnPDF').onclick =()=>{
    console.log('ola');
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({ unit: 'mm', format: 'a4' });
    //-------------------------------
    doc.setFillColor(240,240,240);
    doc.rect(0, 0, 210, 44, 'F');
    //-------------------------------
    doc.setFontSize(40);
    doc.setTextColor('#444');
    doc.setTextColor(50);
    doc.text('Facture',158,40); 

    doc.output('dataurlnewwindow'); // différents: data url new window
    //doc.save(`document.pdf`);
}
</script>
```

## 6 - Ajouter une image
(path,X,Y,largeur,hauteur)
```js
doc.addImage('./img/ubuntu.jpg','JPG',10,8,30,30)
```
[doc](https://artskydj.github.io/jsPDF/docs/module-addImage.html)


## 7 - Code complet pour un "Hello world" avec une image
```html

<button id="btnPDF">PDF</button>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script>
document.getElementById('btnPDF').onclick =()=>{
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({ unit: 'mm', format: 'a4' });
    doc.setFillColor(240,240,240);
    doc.rect(0, 0, 210, 44, 'F');
    //-------------------------------
    doc.addImage('./img/ubuntu.jpg','JPG',10,8,30,30);
    //-------------------------------
    doc.setFontSize(40);
    doc.setTextColor('#444');
    doc.setTextColor(50);
    doc.text('Facture',158,40); 
    doc.output('dataurlnewwindow'); 
    //doc.save(`document.pdf`);
}
</script>
```
## 8 - Ajouter une Font
Ajouter la font Ubuntu
(path,nom de la font,type)
type = normal, bold , italic

```js
doc.addFont('./font/Ubuntu-Regular.ttf','Ubuntu-Regular','normal');
```
Selectionner la font à utiliser
```js
doc.setFont('Ubuntu-Regular');
```

## 9 - Code complet avec une nouvelle font
```js
document.getElementById('btnPDF').onclick =()=>{
    console.log('ola');
    const { jsPDF } = window.jspdf;
    const doc = new jsPDF();
    //-------------------------------------------
    doc.addFont('./font/Ubuntu-Regular.ttf','Ubuntu-Regular','normal');
    doc.setFont('Ubuntu-Regular');
    //-------------------------------------------
    doc.setFillColor(240,240,240);
    doc.rect(0, 0, 210, 44, 'F');
    doc.addImage('./img/ubuntu.jpg','JPG',10,8,30,30);
    doc.setFontSize(40);
    doc.setTextColor('#444');
    doc.setTextColor(50);
    doc.text('Facture',158,40); 
    doc.output('dataurlnewwindow'); 
}
```

## 10 Mise en place de auto-table
le cdn :
```html
<script src="https://cdn.jsdelivr.net/npm/jspdf-autotable"></script>
```

```js
doc.autoTable({
    const headers = [["ID", "Nom", "Email", "Âge"]];
    const data = [
        [1, "Alice Dupont", "alice@example.com", 28],
        [2, "Bob Martin", "bob@example.com", 35],
        [3, "Charlie Durand", "charlie@example.com", 42],
    ];
    startY: 30, // position du tableau
    head: headers,
    body: data,
    theme: 'striped', // styles: 'striped', 'grid', 'plain'
    styles: {
        fontSize: 12,
        cellPadding: 4
    },
    headStyles: {
        fillColor: [22, 160, 133], // vert
        textColor: 255,
        halign: 'center'
    },
    bodyStyles: {
        halign: 'left'
    }
});
```

## 11 Mise en place de auto-table pour aligner les totaux vers la droite


```js
    doc.autoTable( {
        startY: 110,
        tableWidth:24,
        margin: {
        left: 153,
        },

        body: [
        [2000],
        ],
        bodyStyles:{  halign: 'right' ,textColor:'#3c3c3c',fillColor:'#ccc'  }

    })
```

## Ressources et documentation officielle :
- https://github.com/parallax/jsPDF
- https://artskydj.github.io/jsPDF/docs/jsPDF.html
