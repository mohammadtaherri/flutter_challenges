## Scrollbar


By default scrollable widgets like `ListView` hava a **scrollbar**,when the app is run on *linux* or *macOS* or *windows*.Tehre are two ways for enable **scrollbar** in *android* , *ios* and *fuchsia* : 

1)Enabling it for the all scrollable widgets of the app:

```dart
main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      builder: (BuildContext context, Widget? navigator) {
        return ScrollConfiguration(
          behavior: ScrollConfiguration.of(context).copyWith(
            scrollbars: true, // false
          ),
          child: navigator!,
        );
      },
      home: const HomePage(),
    );
  }
}
```


2)Enabling it for the all scrollable widgets in a subtree:

```dart
class ScrollbarsToggle extends StatelessWidget {
  const ScrollbarsToggle({
    Key? key,
    this.scrollbars = true,
    required this.builder,
  }) : super(key: key);

  final bool scrollbars;
  final WidgetBuilder builder;

  @override
  Widget build(BuildContext context) {
    return ScrollConfiguration(
      behavior: ScrollConfiguration.of(context).copyWith(
        scrollbars: scrollbars,
      ),
      child: Builder(
        builder: (BuildContext context) => builder(context),
      ),
    );
  }
}
```

In a `CustomScrollView` you can also change the behavior of the Widget without changing the behavior of the all widgets in the app or a subtree.

```dart
CustomScrollView(
  scrollBehavior: ScrollConfiguration.of(context).copyWith(
    scrollbars: true // false
  ),
  slivers: [],
)
```
