# MongoDB Tutorial

MongoDB Tutorial Deutsch für Anfänger. Mit MongoDB als NoSQL Datenbank kannst du deine Daten direkt als Objekt im JSON Format persistieren und auch so wieder auslesen. Ich zeige dir was du alles brauchst und stelle dir alle wichtigen Befehle in der MongoDB Shell vor. Happy Coding!

[Tutorial auf YouTube anschauen](https://youtu.be/jpTNn4zkMKY)

[![Tutorial bei Youtube](http://img.youtube.com/vi/jpTNn4zkMKY/0.jpg)](https://youtu.be/jpTNn4zkMKY)

## Vernetze dich:

[<img align="left" alt="programmierenmitmario.de" width="22px" src="https://raw.githubusercontent.com/iconic/open-iconic/master/svg/globe.svg" />][website]
[<img align="left" alt="programmierenmitmario | YouTube" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/youtube.svg" />][youtube]
[<img align="left" alt="programmierenmitmario | Twitter" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/twitter.svg" />][twitter]
[<img align="left" alt="programmierenmitmario | Instagram" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/instagram.svg" />][instagram]
<br>
<br>

## MongoDB Cheat Sheet

### Alle Datenbanken anzeigen

<pre>
show dbs
</pre>

### Aktualle Datenbank anzeigen

<pre>
db
</pre>

### Datenbank verwenden/anlegen

<pre>
use tutorial
</pre>

### Datenbank löschen

<pre>
db.dropDatabase('tutorial')
</pre>

## Collections

### Neue Collection anlegen

<pre>
db.createCollection('products')
</pre>

### Alle Collections anzeigen

<pre>
show collections
</pre>

### Collection löschen

<pre>
db.products.drop()
</pre>

## Documents anlegen

### Ein neues Document hinzufügen

<pre>
db.products.insertOne(
  {
    name: "Banane",
    price: 0.99,
    category: 'Obst',
    views: 16
  }
)
</pre>

### Mehrere Documents hinzufügen

<pre>
db.products.insertMany(
  [
    {
      name: "Apfel",
      price: 0.60,
      category: 'Obst',
      views: 2
    },
    {
      name: "Apfel Neu",
      price: 0.80,
      category: 'Obst',
      views: 10
    },
    {
      name: "Kiwi",
      price: 1.19,
      category: 'Obst',
      views: 0,
      ratings: [
        { user: 'Paul', stars: 4},
        { user: 'Tom', stars: 5},
        { user: 'Max', stars: 3}
      ]
    }
  ]
)
</pre>

## Documents auslesen

### Alle Documents aus der Collection anzeigen

<pre>
db.products.find()
</pre>

### Ergebnisse formatiert

<pre>
db.products.find().pretty()
</pre>

### Ergebnisse filtern

<pre>
db.products.find({ name: 'Apfel' })
</pre>

### Ergebnisse sortieren

<pre>
db.products.find().sort({ name: 1 })
db.products.find().sort({ name: -1 })
</pre>

### Ergebnisse zählen

<pre>
db.products.find().count()
db.products.countDocuments()
</pre>

### Ergebnisse limitieren

<pre>
db.products.find().limit(2)
</pre>

### Verkettung mehrerer Funktionen

<pre>
db.products.find().limit(2).sort({ price: 1 })
</pre>

### ForEach Schleife

<pre>
db.products.find().forEach(function(doc) {
  print("Produkt: " + doc.name)
})
</pre>

### Ergebnisse nach Größer/Kleiner filtern

<pre>
db.products.find({ price: { $gt: 1 } })
db.products.find({ price: { $gte: 0.99 } })
db.products.find({ price: { $lt: 0.99 } })
db.products.find({ price: { $lte: 0.99 } })
</pre>

### Feld indexieren

<pre>
db.products.createIndex(
  { name: 'text' },
  { default_language: "german" }
)
</pre>

### Alle Indexes anzeigen

<pre>
db.products.getIndexes()
</pre>

### Index löschen

<pre>
db.products.dropIndex('name_text')
</pre>

### Textsuche

<pre>
db.products.find({
  $text: {
    $search: "Apfel"
  }
})
</pre>

### Nur ein Ergebnis

<pre>
db.products.findOne({ category: 'Obst' })
</pre>

### Ergebnisse gefiltert und mit bestimmten Feldern

<pre>
db.products.find({ category: 'Obst' }, {
  name: 1,
  price: 1
})
</pre>

### Alle Ergebnisse mit bestimmten Feldern

<pre>
db.products.find({}, {
  name: 1,
  price: 1
})
</pre>

### Alle Ergebnisse ohne bestimmte Felder

<pre>
db.products.find({}, {
  ratings: 0,
  date: 0
})
</pre>

## Documents updaten

### Ein Document aktualisieren

<pre>
db.products.updateOne({ name: "Banane" },
{
  $set: {
    price: 1.29
  }
})
</pre>

### Ein Document aktualisieren/hinzufügen

<pre>
db.products.updateOne({ name: 'Gurke' },
{
  $set: {
    price: 0.5 ,
    category: 'Gemüse',
    views: 0
  }
},
{
  upsert: true
})
</pre>

### Viele Documents aktualisieren

<pre>
db.products.updateMany({ category: "Obst" },
{
  $set: {
    price: 0.2
  }
})
</pre>

### Einen Wert erhöhen

<pre>
db.products.updateOne({ name: 'Gurke' },
{
  $inc: {
    views: 1
  }
})
</pre>

### Ein Feld umbenennen

<pre>
db.products.update({ name: 'Gurke' },
{
  $rename: {
    views: 'likes'
  }
})
</pre>

## Aggregates

### Daten aus Collections verarbeiten

<pre>
db.products.aggregate([
  {
    $match: {
      price: { $lt: 0.99 }
    }
  },
  {
    $group: {
      _id: "$category",
      total_views: { $sum: "$views"}
    }
  }
])
</pre>

## Documents löschen

### Ein Document löschen

<pre>
db.products.deleteOne({ name: 'Gurke' })
</pre>

### Viele Documents löschen

<pre>
db.products.deleteMany({ category: 'Obst' })
</pre>

## License

[MIT](LICENSE)

[website]: http://programmierenmitmario.de
[twitter]: https://twitter.com/programmierenm
[youtube]: https://youtube.com/programmierenmitmario
[instagram]: https://instagram.com/programmierenm
