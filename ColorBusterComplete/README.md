# Color Buster Game

## General Info
Author: Lillian Arguelles
Class: CSIS 3460 - Object Oriented Design
Time Frame: Spring 2016


## Details

Initially the professor gave us a project with files but the game itself did not work. We were told to: get it working, and add features that made it our own. Listed below are the changes I implemented for the project.

* **Resources Added**
	* Added Images:	Black.jpg

* **Changes to Default Classes**
	* Main.java
	* No Changes Made
* **Model Classes**
	* Tile.java
		* No Changes Made
	* Board.java
		* Added private int threshold
		* Board Constructor
			* added threshold in parameter
			* set global class variable threshold to value passed in with parameter
		* isMoveAvailable
			* changes the if condition (matches.size() >= 3) to be >= threshold
* **View Classes**
	* ButtonView.java
		* Added a JButton - hintButton
		* Added ActionListener levelListener, ActionListener hintButtonListener into the parameters of the 		ButtonView Constructor
		* Added for level combo box to work: levelSelector.addActionListener(levelListener);
		* Added hint button implementation:
			* hintButton = new JButton();
			* hintButton.setText("Hint");
			* hintButton.addActionListener(hintButtonListener);
			* add(hintButton);
	* ScoreView.java
		* Added:
			* private static int threshold
			* private static int bonus
			* private static int pointsReg
			* private static int pointsBonus
			* private int saveScore
		* Constructor - left alone
		* commented out updateScore - original function
		* created functions:
			* setupScoreView
				* passes in threshold, bonus, pointsReg and pointsBonus as parameters
				* sets global variables to associated parameters (i.e. threshold to threshold, etc)
			* updateScore - new version
				* parameter of int tiles is passed in
				* local variable s is set to calculate score
				* new score is added to original score and set to label
			* calculateScore
				* parameter of int tiles is passed in
				* calculates scores based on
					* if number of tiles exceeds # of tiles needed for bonus (bonus)
					* if yes additional tiles have additional points
					* gets regular point score and adds regular with bonus
					* returns the new additional score
			* clear score
				* because of new score calculation method needs this to clear score when new game
			* setter functions (used when changing level)
				* setThreshold
				* setNumBonus
				* setPtsBonus
				* setPtsRegular
	* GameView.java
		* Global Class Variables
			* Added:
				* private int threshold
				* ActionListener levelListener
				* ActionListener hintListener
		* Constructor:
			* Added to parameters:
				* threshold, levelListener and hintListener
			* Added:
				* updateScoreLevel(threshold) - calls function
				* Added levelListener and hintListener to ButtonView Parameters
				* Added threshold to BoardView parameters
	* BoardView.java
		* Added:
			* private int threshold;
			* private Image originalImg;
			* private Image hintImg;
			* private String hintString = "Resources/images/Black.jpg";
			* Timer timer;
			* private int tr;
			* private int tc;
		* Constructor
			* Added int threshold to parameter
		* processTouchedTile
			* created HashSet matches
			* created call for locateNeighbors
			* created call for removeMatchingTiles
			* created call for collapsecollumns
			* adjusted return statement to return # of matching tiles
		* setThreshold
			* created for adjusting level when needed
		* processHint
			* created for implementation of hint button
		* createHintImage
			* created for implementation of hint button
		* blink
			* created for implementation of hint button
	* TileView.java		
		* blinkImg
			* created for implementation of hint button
		* getImg
			* created for implementation of hint button
* **Controller**
	* GameController.java
		* Added:
			* private int variable threshold
			* private final int variable DEFAULT - set to 3
		* in GameController constructor
			* set threshold to be equal to default
			* in the GameView call for new game view
				* changed “Title” to “Color Buster”
				* added: new LevelListener()
				* added: threshold
				* added: new HintListener()
		* in TileTouchedListener Class
			* added: gameView.processTouchedTile(tv);
			* commented out: System.out.println(“Not implemented yet”);
		* in NewGameListener Class
			* commented out: System.out.println(“Not implemented yet”);
			* added: gameView.newGame(threshold);
		* Added:
			* LevelListener Class
				* Changes the level based on the user adjusting the number in combo box
				* Updates level in game view
			* HintListener Class
				* Implements Hint Button
				* Calls Game View to process hint
	* levelManager.java
		* Note: its really a ‘manager’ but used for more of a keeping track of level differences
		* created by me for level changes
		* global class variables
			* private static int threshold;
			* private static int bonus;
			* private static int pointsReg;
			* private static int pointsBonus;
			* private static int level;
		* constructor
			* takes in threshold to set level by
			* Note: there is also a commented out function call to set by level.
				* a better and clearer implementation of levelManager would be to have it set by Level rather than threshold
		* getter functions for global class variables
			* used for when changing level and needing to get number by outside classes
		* setByLevel
			* Note: not currently being used; will be used if it is set by level rather than threshold
		* setByThreshold
			* sets variables based on threshold
			* chart below explains breakdown (also found in top of Java File)

## Extension Ideas
Ideas to add in to project if have time later:
* Score Manager
	* Using hint = negative points
		* 1 Hint = Free
		* 2+ Hint = -5 Points per Hint
		* 5+ Hint = -10 Points per Hint
	* Add High Score
* Level Manager
	* rows, columns, number of colors used per level

