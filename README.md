## Setup

1. Download the source code and copy into your new project repository.
2. Make sure the hidden .gitignore exists - if lost during copying remake it.
3. Edit the Podfile and rename the workspace from 'App' to the project name.
4. Upon building, address the various warnings and errors.

## Programming Guidelines

1. Manage frameworks with CocoaPods.
2. Use Alamofire for network requests.
3. Use RealmSwift for managing objects.
    * integrate objects with Alamofire response using AlamofireObjectMapper
4. Use XIBs instead of storyboards.
5. Adhere to the VIPER architecture pattern.
	* https://www.objc.io/issues/13-architecture/viper/
	* one data manager per model, in a shared space
	* all module items are interfaced for clarity
	* use the viper ruby tool to generate new modules quickly
6. Shared layers (data, network, certain interactors, extensions etc) belong in a shared framework in the app.
7. Methods and variables should be private if not accessed from outwith the class.
8. MARK: - prefixes should be used to group functions appropriately.
        * examples:
        	* MARK: - MyModule
            	* MARK: - UIViewController
            	* MARK: - UITableViewDelegate
	* extensions can be used to organise larger function groups
		* extension MyTableViewController: UITableViewDataSource
9. Use AutoLayout constraints to position views.
	* i.e. no calls to setFrame:
	* Cartography should be used for programatically adding constraints.
10. Conditions should favour constants on the left, so if null == myVar {} instead of if myVar == null {}.
    * be explicit in if statements, so if true == myBool {} in favour of if myBool {}
10. Only reference member properties with 'self.' if required (if in a block or an initialiser that has an argument of the same name).
11. Initialise variables on the same line as declaration.
12. Make use of lazy instantiation in favour of custom initialisers where possible.
13. Use NSLocalisedString if the application is to be localised at any point.
	* if multilingual support is unlikely you can use the English value as the key.
14. Don’t use IB runtime attributes to configure layer view properties (corner radius, border etc) - this should now go in the UIViewController under the VIPER architecture.
15. Global appearance setup should be favoured where possible and implemented in the Appearance module.
16. Keep project structure mimicking file structure, so make sure files are in the correct folder for the group.
18. Method names should use Cocoa guidelines and follow existing code, such as:
	* func didTapXXXButton(sender: UIButton)
		* button action selector
	* func setupContainerView()
		* styling a subview in a controller
	* func myViewController(myViewController: UIViewController, didSelectItems items: NSArray)
		* delegate method with parameter
	* func didDissmissMyViewController(myViewController: UIViewController)
		* delegate method without parameter
19. Class names should relate to the models and the type of controller, for example:
	* EventsTableViewController
	* EventDetailViewController
	* NewsCarouselCollectionViewController
	* LatestNewsTableViewDataSource
20. Variables should be constants unless mutated, so use let in place of var where possible.
20. Properties should relate to the content and type of the object, for example:
	* var messageLabel: UILabel?
	* var loadingActivityIndicatorView: UIActivityIndicatorView?
	* var exposed: Bool
21. Only one variable per line should be declared (@IBOutlet in particular).
21. Images should go in the appropriate Images.xcassets group.
	* image names should be camel case underscored:
		* examples: Button_Close_Icon, User_Profile_Photo_Placeholder
	* images should have all three sizes; @1x, @2x, @3x.
	* app icons only needs to support iOS 8 and above.
22. If developing a universal app - the following should be adhered to unless the interface is identical for both and can scale automatically without ANY platform specific code:
	* use separate XIBs for iPad and iPhone suffixed with ~iPad and ~iPhone.
	* if one is a subset of another, place the subset functionality in a prefixed subclass and use the main class for the superset, so EventsTableViewController (for iPad) and EventsTableViewController_iPhone (for iPhone).
	* if devices share mutual functionality and both have custom functionality, abstract the shared code to a parent controller; BaseEventsTableViewController with two suffixed subclasses (one for each device); EventsTableViewController_iPhone/_iPad.
23. Use // TODO: for any incomplete functionality and // ERROR: for any show-stopping issues.
24. When creating views outwith a controller and InterfaceBuilder (table headers, cells, other complex views) create a XIB and corresponding module so view layout can be done in InterfaceBuilder (helper initialisers exist in Extensions/UIView for instantiation etc).
25. Code marks should conform to the following format to ensure proper formatting in the method select menu:
	* // MARK: - Message
26. Use the synx tool (sudo gem install synx) to keep files synchronised with the project file. Run 'synx path/to/my/project.xcodeproj' to reorganise files on disk.
28. Inline comments should be used to explain unclear/complex code modules, in the format:
	* // this is a comment
29. Keep function implementations concise and ensure they have a single definable purpose.
	* this makes them more testable and the code easier to read.
30. Line break after function/class/struct declarations (soothes my OCD).

## Localisation

Use NSLocalizedString in source code and execute the following command in terminal to generate a Localizable.strings (in the English directory):

    find ./App -name \*.m | xargs genstrings -o App/Resources/Localisation/en.lproj