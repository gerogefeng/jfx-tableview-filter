#jfx-tableview-filter
In Swing I often used [swing-bits](https://github.com/eugener/oxbow) and now in JavaFX I was missing such an easy way for filtering table columns.
This library tries to fill the gap.
Currently it supports String-based filtering only as that is all I needed yet.

 Open Filter            | Filter result
:-------------------------:|:-------------------------:
![](http://i.imgur.com/w0AeGDv.png)  |  ![](http://i.imgur.com/6ozBmAf.png)

## Maven
jfx-tableview-filter is not on Maven Central. Find it on [JitPack.io](https://jitpack.io/#kaiwinter/jfx-tableview-filter/v1.1.0)
```xml
<repository>
	 <id>jitpack.io</id>
	 <url>https://jitpack.io</url>
</repository>

<dependency>
	 <groupId>com.github.kaiwinter</groupId>
	 <artifactId>jfx-tableview-filter</artifactId>
	 <version>v1.1.0</version>
</dependency>
```

## How does this work?
Call `FilterSupport.addFilter(tableColumn)` for each `TableColumn` which you want to have a filter.

## Well, how does this WORK?
The library takes the underlying `ObservableList` of the `TableView` and wraps it in a `FilteredList` which gets wrapped in a `SortedList`.
The need for the `FilteredList` should be obvious.
The `SortedList` is necessary to keep the sorting by clicking the table headers working.
You don't have to do anything for this as the library handles this wrapping when the filter gets opened for the first time.

## What's the side effects of this wrapped lists? 
The `TableView` doesn't contain a 'plain' `ObservableList` anymore.
When you call `TableView.getItems()` you get the `SortedList` instead of the `ObservableList`.  
`SortedList` doesn't support all methods as `ObservableList` so you will get an `UnsupportedOperationException` for example when you call `clear()`.
To fix this there is the helper method `FilterSupport.getItems(tableView)` which returns the original `ObservableList`.
### That's bad
Yes it is.
In the future this library might be extended by a `FilterableTableView` which ~~overwrites `getItems()`~~ nope it's `final`.

# Credits
Filter icons by [Yusuke Kamiyamane](http://p.yusukekamiyamane.com/). Licensed under a [Creative Commons Attribution 3.0 License](http://creativecommons.org/licenses/by/3.0/).
