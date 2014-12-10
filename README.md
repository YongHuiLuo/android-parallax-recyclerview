android-parallax-recycleview
============================
**USAGE**

(Example project - https://github.com/kanytu/example-parallaxrecycler)


 - Create your object list and pass it to the constructor of `ParallaxRecyclerAdapter`

```java
List<String> myContent = new ArrayList<String>(); // or another object list
ParallaxRecyclerAdapter myAdapter = new ParallaxRecyclerAdapter(myContent); // pass the list to the constructor
```

 - Implement `ParallaxRecyclerAdapter.RecyclerAdapterMethods`.

```java
myAdapter.implementRecyclerAdapterMethods(new ParallaxRecyclerAdapter.RecyclerAdapterMethods() {
  @Override
  public void onBindViewHolder(RecyclerView.ViewHolder viewHolder, int i) {
    // If you're using your custom handler (as you should of course) 
    // you need to cast viewHolder to it.
    ((MyCustomViewHolder) viewHolder).textView.setText(myContent.get(i)); // your bind holder routine.
  }
  
  @Override
  public RecyclerView.ViewHolder onCreateViewHolder(ViewGroup viewGroup, int i) {
    // Here is where you inflate your row and pass it to the constructor of your ViewHolder
    return new MyCustomViewHolder(LayoutInflater.from(
               viewGroup.getContext()).inflate(R.layout.myRow, viewGroup, false));
  }
  
  @Override
  public int getItemCount() {
    // return the content of your array
    return myContent.size();
  }
});
```

 - Now we set the parallax header. You need to pass the `RecyclerView` too to implement the scroll listeners.

```java
myAdapter.setParallaxHeader(LayoutInflater.from(this).inflate(
    R.layout.myParallaxView, myRecycler, false), myRecyclerView);
```

There a few other listeners you can implement:

```java
// Event triggered when you click on a item of the adapter.
void onClick(View v, int position); 

// Event triggered when the parallax is being scrolled.
void onParallaxScroll(float percentage, float offset, View parallax); 
```

**RESULT**

![ParallaxListView](https://raw.githubusercontent.com/kanytu/android-parallax-recycleview/master/screenshots/screenshot.gif)


**COOL EFFECTS YOU CAN DO WITH THIS LIBRARY**

 - Transparent toolbar effect

```java
@Override
public void onParallaxScroll(float percentage, float offset, View parallax) {
  Drawable c = mToolbar.getBackground();
  c.setAlpha(Math.round(percentage * 255));
  mToolbar.setBackground(c);
}
```

![ParallaxListView](https://raw.githubusercontent.com/kanytu/android-parallax-recycleview/master/screenshots/parallaxtoolbar.gif)


[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-android--parallax--recyclerview-brightgreen.svg?style=flat)](https://android-arsenal.com/details/3/1095)


## License
Copyright (c) 2014 Pedro Oliveira

Licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)

