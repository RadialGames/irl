# IRL:
#### A game development library you can use IRL

When making games, I don't use all-in-one game packages or frameworks - I just use a collection of helper functions to make my life a bit easier, sorta similar to FlashPunk. This set of tools has been evolving over the last two years and I think it would do better opened to the world!

This library is intended to be used with Haxe3 & OpenFL, and some classes have dependencies (such as the Actuate library), but not all of them.  I try to keep them as unspecific and lightweight as possible.  Just use the classes you want, and ignore the rest; they won't compile into your project.

## Caveat!

I'm not a genius and I have no formal programmer training. To me, it's more important to hack things to "just work" quickly without much of an eye to performance or good design patterns. One of the reasons I'm sharing this library is to hopefully help fix that and make a better world for all of us. Let's work together! Let's make this beautiful and great! Maybe I'll learn to do things /right/ for a change!

## Installation

The easiest way to install this library is to use the `haxelib` tool from your command line:
	
	haxelib install irl
	
Alternatively, you can install direct from Git if you want the bleeding-edge version:
	
	haxelib git irl https://github.com/CapnAndy/irl.git
	
You then have to tell your project to use the haxe library, by adding the following to your `application.xml` file:

	<haxelib name="irl" />
	
(You can also just download this git repo and slam the `irl` folder into your project source directory, it should work the same there.)

Once installed, just start using some functions! No library initialization is required. Example:
	
	import irl.Rndm;
	
Then in your code:
	
	trace( Rndm.bool() );
	
## Usage

Each class /should/ be documented, so the code-completion in your editor should answer any of your burning questions. Here's a quick reference guide:

### Analytics

The `Analytics` class is intended to work in conjunction with `haxelib haxe-ga`, and is a static wrapper class that just makes submitting google analytics information a bit easier.

	// The path and domain are optional arguments
	Analytics.init("MyAnalyticsID", "radialgames.com", "/WordWings/");
	
	// Once initialized, you can just call a quick reference to record an Analytics pageview:
	Analytics.pageView("gameStarted");
	
### Assert

The `Assert` class is designed to replicate assertation behaviour that is available in other languages; it basically does an evaluation check and throws an error on failure. Great for debugging.

	Assert.isTrue(stage != null, "Oh crap, stage doesn't exist");
	
The assertion uses macros to disable itself when not a debug build, and can also be added to other classes via the `using` keyword.

### BitmapText

This class creates a bitmap image out of a standard TextField object, allowing you to use Filters on GPU-rendered devices.

	addChild( new BitmapText("Hello!", new TextFormat()) );
	
### BitmapTextAnimated

This class extends `BitmapText` but makes the text appear as if it was being typed out.

	var myText = new BitmapText("This types out slowly!", new TextFormat() );
	// Delay before start, and milliseconds per character, respectively:	
	myText.startAnimation(0, 150);
	
### Button

This class simply adds a signal dispatcher to `WSprite` that triggers when pressed.

	var myButton = new Button();
	myButton.addChild(myBitmap);
	
	// clickHandler will be called upon button press
	myButton.pressed.add(clickHandler);
	
### FPSCounter

A basic `FPSCounter` that displays the number of FPS passed, with optional averaging, and target framerate.

	FPSCounter.init(stage, 30); // Smooths FPS over 30 frames.
	
### GenericProperties

This is essentially a pre-typed `Map<String, Dynamic>` shortcut -- useful for storing whatever data you want with string references.

	var gProp = new GenericProperties();
	gProp.set("MyVariable", 1234);
	gProp.get("MyVariable"); // 1234
	
### GreyBox

The `GreyBox` extends `WSprite` and just draws itself a nice grey box. Perfect for prototyping.

	addChild( new GreyBox(100, 100) );
	
(You can also customize the line thickness and colours with optional instantiation variables)

### GreyCircle

Same as `GreyBox` but draws a circle instead. Useful if you want to spice up your greyboxing.

	addChild( new GreyCircle(100) );

### Input

This class handles some basic input functionality and reports back using Signals. Requires you install the `msignal` library first.

	Input.init(stage);
	
	// This triggers a custom function on mouse press:
	Input.mousePressed.add(myMouseListener);
	
	// This returns the current mouse state:
	Input.mousePressed;
	
### Rndm

The `Rndm` class is a selection of randomization tools that should work easily and nicely, across all Haxe-supported platforms.  Allows for specific seeding and resetting to previous seeds, and includes shortcuts to common utilities.

	// Set a random seed:
	Rndm.seed = 1234;
	
	// Common random figures, with min and optional max:
	Rndm.float(0.2, 1.4);
	Rndm.integer(5, 20);
	
	// Option arguments for common functions:
	Rndm.bool(); 	// (50%)
	Rndm.bool(0.8); // (80%)
	
	// These two return the same values:
	Rndm.staticDice(diceSides, numDice);
	trace( Rndm.lastStaticDiceRoll );
	
If no seed is specified (or you set the seed to 0), it will generate one randomly based off the timestamp the next time it needs one.

In case you need a one-off deterministic result from the class, you can specific one-time-use seed like so:
	
	Rndm.useForNextSeedOnly = 12345.67890;
	Rndm.integer(0, 100); // Always returns the same result based on the above seed
	Rndm.integer(0, 100); // Reverts to standard random seed generation

### SaveData

This class makes saving game data a little bit easier by wrapping the `SharedObject` class with simple `get` and `set` comands.

	SaveData.init("WordWings", "/RadialSaveData/");
	
	SaveData.set("score", 1234);
	SaveData.get("score"); // 1234

### Utils

A general utilitarian class that handles several common operations, such as rotating a point, sorting an array, or even just adding commas to large numbers.

(will document more details here later)

### WSprite

A wrapper for the `Sprite` class that contains a lot of helper functions such as `.top` and `.bottom` for determining pixel positions, screenshake functions, and drawing of bounding boxes.

(will document more details here later)
	
## Games using this library:
	
 - Monster Loves You!, available on Steam/iOS/Android
 - All games by Radial Games! http://www.radialgames.com ! (buy today!)

## ToDo

 - Add back in the AdobeAIR Specific libraries for SteamWorks, GameCenter, and GoogleGames.
 - Document all the things.
 - Settle on a proper acronym definition to title the project.

http://www.radialgames.com