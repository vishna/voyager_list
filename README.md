[![pub package](https://img.shields.io/pub/v/voyager_list.svg)](https://pub.dartlang.org/packages/voyager_list) [![Codemagic build status](https://api.codemagic.io/apps/5d99c4749b09d3000b08f35d/5d99c4749b09d3000b08f35c/status_badge.svg)](https://codemagic.io/apps/5d99c4749b09d3000b08f35d/5d99c4749b09d3000b08f35c/latest_build) [![codecov](https://codecov.io/gh/vishna/voyager_list/branch/master/graph/badge.svg)](https://codecov.io/gh/vishna/voyager_list)

# voyager_list

Allows mapping a list of arbitrary objects to a list view.

![voyager-keynote 001](https://user-images.githubusercontent.com/121164/66267843-cacfba00-e836-11e9-87ed-1b7e5426b205.png)

# Usage

Say you have 3 different classes...

```dart
class Shoe {
    final id;
    final name;
    Shoe(this.id, this.name);
}

class Bulb {
    final id;
    final name;
    Bulb(this.id, this.name);
}

class Duck {
    final id;
    final name;
    Duck(this.id, this.name);
}
```

...a mixed list of items of these types:

```dart
final items = [
    Shoe("mk", "Mike"),
    Bulb("bl", "Phillip"),
    Duck("rb", "Rubber")
]
```

and respective widgets:

```dart
class ShoeWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Shoe shoe = Provider.of<VoyagerArgument>(context).value;
    return Text("Shoe: ${shoe.name}");
  }
}

class DuckWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Duck duck = Provider.of<VoyagerArgument>(context).value;
    return Text("Duck: ${duck.name}");
  }
}

class BulbWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Bulb bulb = Provider.of<VoyagerArgument>(context).value;
    return Text("Bulb: ${bulb.name}");
  }
}
```

You can simply map your object list to a list view:

```dart
String idMapper(dynamic item) => item.id;
String objectMapper(dynamic item) =>
      "/object/${item.runtimeType}";
VoyagerListView(items, idMapper, objectMapper);
```

provided your navigation map specifies following mapping:

```yaml
'/object/:className':
  type: object_item
  widget: "%{className}Widget"
```