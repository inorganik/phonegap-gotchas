## iOS 7 - webview is overlapped by status bar

##### PROBLEM

>In iOS 7, the app's webivew is overlapped by the status bar.

##### SOLUTION

This is actually the intended behavior of iOS 7. It’s part of the new look, which makes the status bar seem more integrated in the UI.  The problem is, you likely want to be able to run your app on iOS 6 and iOS 7, and need to account for that extra 20px one way or another. Here’s one fix:

At the top of MainViewController.h, insert the following property:

```objc
@interface MainViewController : CDVViewController
@property (nonatomic, assign) BOOL firstAppearance;
@end
```
In MainViewController.m, make the following changes:
```objc
@implementation MainViewController
@synthesize firstAppearance;
```
Edit initWithNibName method:
```objc
- (id)initWithNibName:(NSString*)nibNameOrNil bundle:(NSBundle*)nibBundleOrNil {
    self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
    if (self) {
        self.firstAppearance = YES;
    }
    return self;
}
```
Inside viewWillAppear method:
```objc
- (void)viewWillAppear:(BOOL)animated {
    if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 7) {
        if (self.firstAppearance) {
            self.firstAppearance = NO;
            CGRect viewBounds = [self.webView bounds];
            viewBounds.origin.y = 20;
            viewBounds.size.height = viewBounds.size.height - 20;
            self.webView.frame = viewBounds;
        }
    }
    [super viewWillAppear:animated];
}
```
Edit viewDidLoad Method:
```objc
- (void)viewDidLoad {
    if ([self respondsToSelector:@selector(setNeedsStatusBarAppearanceUpdate)]) {
        [self setNeedsStatusBarAppearanceUpdate];
    }
    [super viewDidLoad];
}
```
Add method:
```objc
-(UIStatusBarStyle)preferredStatusBarStyle {
    // UIStatusBarStyleDefault
    // UIStatusBarStyleLightContent
    // UIStatusBarStyleBlackTranslucent - deprecated ios 7
    // UIStatusBarStyleBlackOpaque - deprecated ios 7
    return UIStatusBarStyleLightContent;
}
```
Now, edit your MainViewController.xib file and make its background color whatever you want the background of the status bar to be. Using `UIStatusBarStyleLightContent` makes the status bar text white, and `UIStatusBarDefault` makes it black. Those are they only two options that are not deprecated in iOS 7.
