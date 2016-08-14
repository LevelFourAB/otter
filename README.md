# Otter

Otter is a library to support collaborative realtime editing using
[Operational Transformation](https://en.wikipedia.org/wiki/Operational_transformation).
It is available for several platforms and is designed to be integrated with your
existing system.

## Features

* Realtime editing of strings, maps and lists
* Support for multiple users concurrently editing the same content
* High-level API for working with realtime content
* Extendable with custom data types
* Annotation/marking support for strings

## Planned Features

* Undo/redo support
* Helpers for easier sync implementation

## Library implementations

* [otter-java](https://github.com/LevelFourAB/otter-java) - Java 8 implementation for both servers and clients
* [otter-js](https://github.com/LevelFourAB/otter-js) - JS implementation for Node and the browser

## Browser example

```javascript
var model = new otter.Model(new otter.engine.Editor(serverSync));
model.open()
    .then(function() {
        var title = model.get('title', function() {
            // This is run if title is not in the model
            return model.newString();
        });
        otter.model.bind.text(title, document.getElementById('text-input'));

        var users = model.get('users', function() {
            return model.newList();
        });

        users.on('insert', function(e) {
            // This will be called when something is added to the list
            console.log(e);
        });

        users.add({
            id: 'xFk12',
            name: 'Test'
        });
    });
```
