# Verbat--First-name-of-candidate---last-name-of-candidate-
GifInteraction App
GifInteraction App is based on ZLSwipeableView.

Preview

CocoaPods Used
You can install ZLSwipeableViewSwift through CocoaPods adding the following to your Podfile:

pod 'ZLSwipeableViewSwift'
use_frameworks!

Then import it using:
import ZLSwipeableViewSwift

Instantiation
ZLSwipeableView can be added to storyboard or instantiated programmatically:
var swipeableView = ZLSwipeableView(frame: CGRect(x: 0, y: 0, width: 300, height: 500))
view.addSubview(swipeableView)

Adding Views
ZLSwipeableView supports both adding views to the front and to the back.
public var numberOfActiveView = UInt(4)
public var nextView: (() -> UIView?)?
public var previousView: (() -> UIView?)?

Adding views to the back
nextView, a closure that returns an UIView, works with loadViews and numberOfActiveView. It acts as the data source. After defining it, ZLSwipeableView will call loadViews which will invoke nextView numberOfActiveView times and insert them in the back. loadViews will also be called each time a view is swiped.
public func loadViews()
// Usage:
swipeableView.numberOfActiveView = 3
swipeableView.nextView = {
return UIView()
}
swipeableView.loadViews() // optional, automatically call after nextView is set

Adding views to the front
previousView works with rewind, which inserts a view in the front and positions it at the center with animation. Note that rewind calls previousView only when history is empty, otherwise it returns the most recently swiped view. Please try out the Previous View example for more information.
public func rewind()
// Usage:
swipeableView.previousView = {
return UIView()
}
swipeableView.rewind()

Interface Builder
If you need to work with Interface Builder, the demo app includes examples of both creating views programmatically and loading views from Xib files that use Auto Layout.

Removing Views

Swiping programmatically
The user can swipe views in the allowed directions. This can also happen programmatically.
You can swipe the top view programmatically in one of the predefined directions or with point and direction in the view's coordinate.
public func swipeTopView(inDirection direction: Direction)
// Usage:
swipeableView.swipeTopView(inDirection: .Left)
swipeableView.swipeTopView(inDirection: .Up)
swipeableView.swipeTopView(inDirection: .Right)
swipeableView.swipeTopView(inDirection: .Down)

public func swipeTopView(fromPoint location: CGPoint, inDirection directionVector: CGVector)
// Usage:
swipeableView.swipeTopView(fromPoint: CGPoint(x: 100, y: 30), inDirection: CGVector(dx: 100, dy: -800))

Rewinding:
ZLSwipeableView keeps a history of swiped views. They can be retrieved by calling rewind.
public var history = [UIView]()
public var numberOfHistoryItem = UInt(10)

public func rewind()

Removing all views:
To discard all views and reload programmatically (discarded views cannot by rewinded):
swipeableView.discardViews()
swipeableView.loadViews()


Delegate:
Here is a list of callbacks you can listen to:
swipeableView.didStart = {view, location in
print("Did start swiping view at location: \(location)")
}
swipeableView.swiping = {view, location, translation in
print("Swiping at view location: \(location) translation: \(translation)")
}
swipeableView.didEnd = {view, location in
print("Did end swiping view at location: \(location)")
}
swipeableView.didSwipe = {view, direction, vector in
print("Did swipe view in direction: \(direction), vector: \(vector)")
}
swipeableView.didCancel = {view in
print("Did cancel swiping view")
}

Requirements:
iOS 7 or higher.

