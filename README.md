SDFPages
========

SDFPages is a simple replacement for NSPageController from Apple. NSPageController is complicated and you don't get much control of your animations. Thus SDFPages was born.

It works by simply taking a bunch of view controllers, getting the views and adding them into a scroll view. You can stack the views vertically or horizontally and navigate forward or backward as you see fit.

SDFPages is a very basic plugin and will never be overly feature rich, howeverif you do want something please just leave an issue and I'll look at putting it in.

# Usage

### Setup

1. Create an array of pages you want, make sure they each inherit from **SDFPageViewController**

```
  NSMutableArray *pages = [NSMutableArray new];
  
  SDFPageViewController *page1VC = [[SDFPageViewController alloc] initWithNibName:@"Page1View" bundle:nil];
  [pages addObject:page1VC];
  
  SDFPageViewController *page2VC = [[SDFPageViewController alloc] initWithNibName:@"Page2View" bundle:nil];
  [pages addObject:page2VC];
  
  SDFPageViewController *page3VC = [[SDFPageViewController alloc] initWithNibName:@"Page3View" bundle:nil];
  [pages addObject:page3VC];
``` 

NOTE: It's easiest to create the view controllers in code like above as sometimes when connecting up via NIBs they aren't loaded correctly and errors occur when setup is called.
  
2. Create a new pages controller and assign the pages, now is the time to customise the controller as needed

```
  //  self.pagesController is a property on this class
  self.pagesController = [SDFPagesController new];
  // In this example the code is added to a **NSWindowController**
  self.pagesController.contentView = self.window.contentView;
  self.pagesController.pages = pages;
```

3. Call **setup** somewhere in your code at a time when you know the views will be loaded, i.e. NOT during **init**.

```
  [self.pagesController setup];
```

### Navigation

Each **SDFPageViewController** has an **IBOutlet** for **nextPage** and **previousPage**.

### Customisation

The following are able to be set before **setup** is called:

- **Flow**: horizontal / vertical stacked views
- **Direction**: which direction will the views be stacked, if **forward** and **horizontal** the views will be stacked from left to right with the left most view being the first page view and the last page view being on the right. The scrolling direction when next page is hit will go left to right. Otherwise if **backward** and **horizontal** the views will be stacked right to left with the first page on the right and the last page on the left. The scrolling will go right to left when next page is hit. The same concepts apply for **vertical** with **forward** being top down and **backward** being bottom up.
- **Animation duration**: control the time in seconds the next / previous page animation will take.


