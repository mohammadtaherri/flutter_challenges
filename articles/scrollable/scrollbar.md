## Scrollbars

By default, a scrollable widget (e.g. a `ListView`) has a **scrollbar** on the desktop platforms (*linux* or *macOS* or *windows*).There are some ways to enable it on the mobile platforms (*android* , *ios* and *fuchsia*).you can also use these ways to desable it on the desktop platforms :



1)If you jsut want to enable (desable) it for one or more widgets(not all widgets in your app), use following code:


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
        builder: builder,
      ),
    );
  }
}
```

Then you can wrap your widget (e.g. `ListView` or a subtree that you want to change its bahavior) in the above widget.

```dart
class MyListView extends StatelessWidget {
  const MyListView({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return ScrollbarsToggle(
      scrollbars: true, //false
      builder: (BuildContext context) {
        return ListView(
          ...
        );
      },
    );
  }
}
```



2)If you want to enable (desable) it for all widgets in your app,you should override the `builder` in the `MaterialApp` (or the `WidgetApp`):

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


3)In the `CustomScrollView` you can also change the behavior of the widget without changing the behavior of the all widgets in the app or a subtree.

```dart
CustomScrollView(
  scrollBehavior: ScrollConfiguration.of(context).copyWith(
    scrollbars: true // false
  ),
  slivers: [],
)
```
