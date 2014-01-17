#Coding Experiments in LIVECODE

This document gives a brief tutorial on using the free and open-source programming language LIVECODE for programming behavioral experiments for cognitive research. The tutorial will cover some basic LIVECODE operations, programming a Stroop experiment, and scripts for preliminary data-analysis.

The community edition of LIVECODE can be downloaded for free from the LIVECODE website:

<http://www.livecode.com>

Beginners to LIVECODE should peruse the website for helpful tutorials, and should read through the manual.

##What is LIVECODE?

LIVECODE is a powerful and easy to learn language for creating applications. The language is cross-platform and can be used on macs, pcs, linux machines, and even mobile devices (ios and android). LIVECODE makes it easy to create the visual layout for your program, and to add elements (text fields, buttons, etc.) by dragging and dropping. All of the elements in a LIVECODE program can be scripted.

##Basic LIVECODE concepts

###Stacks and Cards and Elements
The starting point for creating a program is the stack. When you create a new stack, you will see a new window appear. The window can be resized to any size that you wish. When you a user loads your program, they will see the stack load up as the this window.

Stacks are composed of cards. Each stack can have many cards. Cards are like individual slides in a powerpoint or keynote presentation. New cards can be added by selecting New Card from the Object menu.

Many different kinds of elements can be added to cards by dragging and dropping. These elements are accessed through the tools pallette (Tools>Tools Pallette). Typical elements are text fields (for displaying and entering text), buttons (for receiving user input), media (for showing images, playing movies and sound clips), scrollbars, graphic objects, and so on. The size and position of these objects on each card can be changed using the mouse, much like elements inside a powerpoint.

The stack, cards, and elements can all be given unique names using the property inspector. The property inspector is accessed by double-clicking on the element of choice (but make sure you are using the pointer tool, Tools>Pointer Tool).

###Scripting
Scripts are used to implemement algorithms and to control how part of your stack work. Almost every thing in LIVECODE is scriptable. The stack itself is an entity that can be scripted. Each card is its own entity that be scripted. And all of the elements on each card are their own entities that can be scripted. It is important to realize that LIVECODE scripts work in a hierarchical fasion. The stack script is at the top of the hierarchy, the card scripts are next, and the element scripts are at the bottom. Generally, the scripts that are written at each level are specific to that level. However, writing a function at a higher level (in the stack script), allows that function to be available for use at the lower levels. The reverse is not true. Writing a function inside a button script that is on a card does not mean that function will be available to other elements on the same card or other cards. Similarly, variables that are created inside scripts for the stack, cards, or elements, are local to those entities, but they can be made global (accesible to all) if this is specified in the script.

You can access the scripting editor for the stack by Object>Stack Script. Similarly, you can access the scripting editor for the card by Object>Card Script. If you drag a text field and a button onto an empty stack, then you access the scripts for these elements by right-clicking on them and choosing edit script.

SHORTCUTS TO THE EDITOR: When you have selected the edit tool (the arrow with the crosshairs in it) you can double-click on objects and the property menu for that object will appear. Click on the play button and choose edit script. Also, if you are on a mac you can hold down option-command and click on an object to automatically open the script editor.

###Getting started with Scripting

To get a hang of the basic syntax of LIVECODE drag a text field and a button onto the card. Open the script associated with the button. You will see an editor appear with the following text:











		put "1,2,3,4,5,6,7,8,9,10" into someNumbers
		put mysum(someNumbers) into field 1
	end mouseUp

	function mysum x





The second is a list of common commands. You should know how to use each of these commands, and be able to produce examples of working code that utilizes each command. Finally, there is a list of simple to intermediate programming problems that you should be able to solve in LIVECODE. 

####LIVECODE features checklist

Learning LIVECODE
|----------|-----|


**

When programming experiments from scratch, the programmer is responsible for deciding how the data file will be formatted, and is responsible for ensuring that the data file stores all of the necessary information. There is room for flexibility here. The data could potentially be stored in many different formats to achieve the same goals of storing all of the necessary information. This tutorial outlines one tried and true method that can be used to create data files for most any multi-trial design, using long-format data files.


####Long-format data files

The basic strategy is to produce a table in a text file where each line corresponds to the data for each trial in an experiment. Each line will contain words and numbers separated by a tab (or other delimiter of your choice) that represent the order, events, conditions, and responses on each trial. It is sensible to have the first row correspond to the first trial, the second for the 2nd trial, and so one for the remaining trials. 

The following is an example of a data-file for 12 trials in a simple Stroop experiment. 

|trial|Word|Color|Congruency|OnsetTime|ResponseTime|Letter|Accuracy|
|-----|----|-----|----------|---------|------------|------|--------|
|1|red|red|congruent|12341234|12341634|r|correct|
|2|blue|red|incongruent|12341234|12341734|r|correct|
|3|red|red|congruent|12341234|12341534|r|correct|
|4|green|green|congruent|12341234|12341934|g|correct|
|5|yellow|blue|incongruent|12341234|12341334|b|correct|
|6|blue|blue|congruent|12341234|12341334|r|incorrect|
|7|blue|red|incongruent|12341234|12341434|r|correct|
|8|yellow|red|incongruent|12341234|12341234|r|correct|
|9|red|red|congruent|12341234|12341634|r|correct|
|10|green|yellow|incongruent|12341534|12341234|y|correct|
|11|red|red|congruent|12341234|12341234|r|correct|
|12|blue|red|incongruent|12341234|12341334|r|correct|

A data file like the above stores all of the necessary information to reconstruct the events of the experiment. We can see the order of trials. For each trial we can see what word was presented, and what color it was presented in. We can see when the stimulus appeared on the screen (OnsetTime), and when the response was made. We can also see the response key that was pressed on each trial, and whether or not the response was correct or incorrect. Many experiment builder programs (like PsychoPy) format their data-files in a similar manner. As well, data in this format will facilitate data-analysis later on.

One thing to note about the data is the column for congruency, which represents the names for each of the levels of the congruency variable. Usually it is a very good idea to include columns that describe the conditions of the experiment, as this makes data-analysis easier later on. Sometimes it is not strictly necessary to include the condition names because they can be inferred from other information in the table. For example, congruent conditions can be inferred by determining whether the word and color involve the same or different words. However, as a general rule, it is always a good idea to include all of the condition information in the data file, even if the conditions can be inferred at a later stage.

###The Data-file is the Design
When you are new to experimental design, you might think that something like a data file comes along only near the end of a project. First, the experiment needs to be designed, then programmed, then subjects need to be run, and only then do data file appears. However, the creation of data files is central to the very beginning of programming an experiment. Of course, the data files will be empty because you will not have run any subjects. Yet, the data file will represent and define the experimental design at its most granular level, and it can be used to tell the computer how to run each trial of the experiment. Consider the following empty data file. It is empty because it contains the information that would be presented on each trial, but it is missing all of the response information:

|trial|Word|Color|Congruency|OnsetTime|ResponseTime|Letter|Accuracy|
|-----|----|-----|----------|---------|------------|------|--------|
|1|red|red|congruent|||||
|2|blue|red|incongruent|||||
|3|red|red|congruent|||||
|4|green|green|congruent|||||
|5|yellow|blue|incongruent|||||
|6|blue|blue|congruent|||||
|7|blue|red|incongruent||||
|8|yellow|red|incongruent|||||
|9|red|red|congruent|||||
|10|green|yellow|incongruent||||
|11|red|red|congruent|||||
|12|blue|red|incongruent|||||

This data file implies that certain kinds of events would happen on each trial. On trial 1, the word red would be presented in red ink. On trial 2, the word blue would be presented in red ink, and so on. A complete data file is a record of what did happen in an experiment, and an empty data file is a record of what should happen in an experiment. In order to use this list to control the experiment, all that is needed is a script to read each line, interpret the events that are supposed to occur, and then present the events and collect response information the subject. In this way there are two major components to programming an experiment:

1. Creating the list of trials (making the empty data-file)
2. Interpreting the list to run each trial

###Creating the list of trials

Most behavioral experiments follow a similar logic. On each trial some stimulus is presented, and a response is collected. Usually, there are many kinds of stimuli, and each belong to various conditions. The list of trials for an experiment specifies which stimulus (and its conditions) occur on which trial. Depending on the purposes of the experiment, it is usually desirable to control the order with which stimuli are presented. Sometimes the order might be deliberately randomized, or deliberately sequenced. There are other decisions such as determining the frequency with which particular stimuli, or conditions occur across the trials.

Consider the problem of running a simple Stroop experiment with 4 colors, Red, Blue, Green, and Yellow. These four colors can be combined to produce 4 congruent items (blue in blue, red in red, green in green, and yellow in yellow), and 12 inocongruent items (red in blue, red in green, etc.). So far we have 2 conditions, and 16 items. Typically, Stroop experiments are conducted with an equal proportion of congruent and incongruent trials. How can this be accomplished? There are 12 incongruent items and only 4 congruent items. If we present all 12 incongruent items, then the congruent items need to be presented 3 times each (4 x 3 = 12). So, at a minimum, we need to have 24 trials (12 congruent and 12 incongruent). And, if we want to run more trials, and keep the number of congruent and incongruent trials balanced, then we would run trials in multiples of 24. Let's run 96 trials (24*4).

So, how to make a trial list with 96 trials that conforms to the above demands? One simple strategy would be to write the list as a table, just like the one above by hand. Once the first 24 items are all written down, then they could be copy and pasted below to make the list 96 trials long. Sometimes this simple approaches are the fastest and easiest. Let's explore how to create the list using scripts in LIVECODE.

The following scripts are assumed to be placed in a button, and the results are placed into a text field

	on mouseUp
	put empty into field 1
	
	put "red blue green yellow" into StroopWords
	put "red blue green yellow" into StroopColors
	
	repeat for each word n in StroopWords
		repeat for each word j in StroopColors
			if n is j then
				put "congruent" into conditionLabel
			else
				put "incongruent" into conditionLabel
			end if
			put n & tab & j & tab & conditionLabel & return after field 1
		end repeat
	end repeat	
	

	end mouseUp
	
The text field should now contain lines with the following 16 lines, each representing 4 of the possible congruent items, and 12 of the possible incongruent items.

	red	red	congruent


	put empty into field 1
	
	put "red blue green yellow" into StroopWords
	put "red blue green yellow" into StroopColors
	
	repeat for each word n in StroopWords
		repeat for each word j in StroopColors
			if n is j then
				put "congruent" into conditionLabel
				put n & tab & j & tab & conditionLabel & return after field 1
				put n & tab & j & tab & conditionLabel & return after field 1
				put n & tab & j & tab & conditionLabel & return after field 1
			else
				put "incongruent" into conditionLabel
				put n & tab & j & tab & conditionLabel & return after field 1
			end if
		end repeat
	end repeat	
	

	end mouseUp

Here is the result, as you can see all 24 trials are present.

	red	red	congruent

	
	put empty into field 1
	
	put "red blue green yellow" into StroopWords
	put "red blue green yellow" into StroopColors
	
	repeat 4 times
		repeat for each word n in StroopWords
			repeat for each word j in StroopColors
				if n is j then
					put "congruent" into conditionLabel
					put n & tab & j & tab & conditionLabel & return after field 1
					put n & tab & j & tab & conditionLabel & return after field 1
					put n & tab & j & tab & conditionLabel & return after field 1
				else
					put "incongruent" into conditionLabel
					put n & tab & j & tab & conditionLabel & return after field 1
				end if
			end repeat
		end repeat	
	end repeat
	

	end mouseUp
	
At this point, you should have a list of 96 trials that satisfy the constraints of the design from above. A next step is to randomize the order of these trials so that participants are unable to predict the order of items and responses. Lines in a text file can easily be randomized using the sort function. For example:

	sort lines of field 1 by random(the number of lines in field 1)
	
The above line will randomize the order of the lines in field 1. Assuming that field 1 contains the 96 Stroop trials, this list will now be randomized. Each line refers to each trial. If you want to be more specific, and add trial numbers, consider the following code:


	
	put "red blue green yellow" into StroopWords
	put "red blue green yellow" into StroopColors
	
	repeat 4 times
		repeat for each word n in StroopWords
			repeat for each word j in StroopColors
				if n is j then
					put "congruent" into conditionLabel
					put n & tab & j & tab & conditionLabel & return after field 1
					put n & tab & j & tab & conditionLabel & return after field 1
					put n & tab & j & tab & conditionLabel & return after field 1
				else
					put "incongruent" into conditionLabel
					put n & tab & j & tab & conditionLabel & return after field 1
				end if
			end repeat
		end repeat	
	end repeat
	
	sort lines of field 1 by random(the number of lines in field 1)
	
	put field 1 into tempVar
	repeat for each line k in tempVar
		add 1 to lineCounter
		put lineCounter & tab & k & return after outputWithTrialNumbers
	end repeat
	put outputWithTrialNumbers into field 1
	end mouseUp
	
Here is the result from the first 24 lines of the output from this script:

	1	blue	green	incongruent



2. An empty text field named StroopStimDisplay placed in the center of the card (this will display the Stroop item)
3. An empty text field named dataVar (to store the data on each trial)
4. A button named begin placed in the bottom center of card (to initiate the experiment)

####Presenting a stimulus
 The following code will be placed in the button Begin. The logic of the code is as follows. Each press of the button should initiate the next trial. The button will increment a counter (that counts 1 to 96 for each trial). The value of the counter will serve as an index into the appropriate line from the trials list (1 for line 1, 2 for line 2 etc.). The 2nd word in each line will be presented as the word on each trial, and the 3rd word will be used to set the font color of the word.
 
	 on mouseUp
	 global TrialCount
	 add 1 to TrialCount
	 put line TrialCount of field trials into trialTemp
	 if TrialCount <97 then
	 	put word 2 of trialTemp into wordVar
	 	put word 3 of trialTemp into colorVar
	 	put wordVar into field StroopStimDisplay
	 	set the foregroundcolor of field StroopStimDisplay to colorVar
	 	show field StroopStimDisplay
	 	put the milliseconds into onsetTime
	 	put trialTemp & tab & onsetTime & tab after field dataVar
	 else
	 	put "Finished" into field StroopStimDisplay
	 	show field StroopStimDisplay
	 end if
	 end mouseUp
	 
Now, everytime the button is clicked, a new Stroop item should appear in the field StroopStimDisplay. As well, the trial information for each trial should be stored into the field dataVar.

####Collecting a response

After each trial is presented on screen, the participant should be able to enter a response to identify the ink color of the presented stimulus. Response collection will be handled by the card script. The goal of response collection could be to 

1. Save the identity of the response key that was pressed
2. Save the time when the response occured
3. Trigger the next trial automatically so the button doesn't need to be pressed manually to start the next trial

The following code goes in the card script:

	on keydown whichkey
		put the milliseconds into RT
		put RT & tab & whichkey & return after field dataVar
		hide field StroopStimDisplay
		send mouseUp to button begin in 1 second
	end keydown

With the code in the button and the card in place, the basic elements of interpreting the trial list to present an item and collect and record a response are in place. The code will run for 96 trials, and then a message saying "finished" will appear in the field StroopStimDisplay.

###Look and feel

The above code shows the basic logic that goes into coding a multi-trial Stroop experiment. There are many additions that could be made to make the experiment look better and run more smoothly. The size of the font in the field StroopStimDisplay can be made larger (using the property inspector). The look of the text field can be changed. A basic text field usually starts with a visible border. This can be turned off so that the word appears on its own without a border. The data field can be hidden. The trials field can be hidden. 

For most experiments, including the demo Stroop experiment in the repository, it is usally desirable to have several cards in your stack. The first card can act as an opening screen, perhaps with a title for the experiment, and a text field for entering subject numbers or counterbalancing codes. There might be a button that is pressed to begin the experiment and take the subject to a second card that displays instructions. This button can also be used to insert the code that creates the trial list. At this point, it would also be important to initialize aspects of the experiment. For example, the button could have code that empties the contents of data field, sets the global counter to zero, and hides or shows important elements on diffent cards. The card containing the instructions could also have a button that sends the subject to a third card containing the code from above that implements the Stroop experiment. Finally, when the trials are over, the participant could automatically be sent to a final card that displays a message like "Thank you for your participation, please find the experimenter".

Many experiment builder programs like e-prime or PsychoPy present trials on a completely blank computer screen. This can be accomplished in LIVECODE by hiding things the like menubar. Check out what the following commands do:

	hide menubar
	show menubar
	set the decorations of this stack to default
	set the decorations of this stack to empty
	set the backdrop to black
	set the backdrop to none
	
In combination with setting the background colors of the card and fields, it is possible to create a completely blank screen for presenting stimuli, if so desired.

###Preventing unwanted actions

The example code shown so far does implement a basic Stroop experiment, however the code allows for some unwanted behavior. We expect that subjects would not press buttons until a stimulus is presented on the screen, and then only press one button (say r to identify a red stimulus) and not many buttons. Unfortunately, even the best subjects will press buttons in error and at inopportune moments. The current version of the code is vulnerable to this kind of button pressing. For example, try pressing the "r" button three times in rapid succession. You should see three trials automatically be presented in rapid succession on the screen. To prevent this kind of behavior, we need to build in logical switches or toggles into the code that allow responses to be collected only during certain times. Fortunately, this is very easy. Consider a variable called toggleResponse. If the contents of the variable is 0 then we do not allow response collection, but if the contents is 1, then we do allow it. Consider, the following code implementing the toggle.

####button begin script
	 on mouseUp
	 global TrialCount
	 global toggleResponse -- new toggle declared as a global variable
	 put 0 into toggleResponse -- set to 0, this could be set elsewhere and early perhaps when the stack is opened
	 add 1 to TrialCount
	 put line TrialCount of field trials into trialTemp
	 if TrialCount <97 then
	 	put word 2 of trialTemp into wordVar
	 	put word 3 of trialTemp into colorVar
	 	put wordVar into field StroopStimDisplay
	 	set the foregroundcolor of field StroopStimDisplay to colorVar
	 	show field StroopStimDisplay
	 	put 1 into toggleResponse -- turn on response Collection
	 	put the milliseconds into onsetTime
	 	put trialTemp & tab & onsetTime & tab after field dataVar
	 else
	 	put "Finished" into field StroopStimDisplay
	 	show field StroopStimDisplay
	 end if
	 end mouseUp
	 
####Card script
	 
	 on keydown whichkey
		global toggleResponse -- declare toggle as a global variable
		put the milliseconds into RT
		if toggleResponse is 1 then -- only do if toggle is on
			put 0 into toggleResponse --turn toggle off to stop multiple keystrokes
			put RT & tab & whichkey & return after field dataVar
			hide field StroopStimDisplay
			send mouseUp to button begin in 1 second
		end if
	end keydown

The toggling logic implemented above will only allow response collection to occur after a Stroop stimulus has been presented. It also only collects one response before turning off, so it prevents multiple key presses from triggering multiple trials in rapid succession. It is worth noting that this kind of toggle is not always desired. Sometimes it is desirable to collect premature responses that occur before the presentation of a stimulus. In this case a different toggle logic would need to be implemented. This shows a great example of the challenges of programming experiments from scratch (having to deal with these issues), as well as the power of programming from scratch (it is possible to do what you want, but you have to figure out how to do it).

###Saving the data

At the end of the experiment the field containing the data should have 96 lines. 

One option for saving the data-file would be to 

1. Make the data field visible
2. Copy and paste the data into a text file
3. Save the text-file to a folder on your computer

Another option is to use LIVECODE to create a file and save the contents to that file. Here is a general strategy for saving text to files in LIVECODE.

1. Create a folder for your experiment, then save your experiment stack into this folder.
2. Inside your experiment folder you should now see the LIVECODE stack. Create a new folder inside the current folder called `data`.
3. Your experiment folder should now contain the LIVECODE stack, and a folder called `data`
4. Create a new button on your card, give it a name like `savedata` (or incorporate this code into your script in another way)

The code for the button script should read as follows (note: this code assumes that your data is in a field called `dataVar`):

	on mouseUp
		put the filename of this stack into fname
		set the itemDelimiter to to "\"
		delete the last item of fname
		put "\data\" after fname
		put field dataVar into url("file:" & fname & "data.txt")
	end mouseUp

If your data field has text inside it, then clicking this button should create a new field called `data.txt` inside the data folder that you created on your hard-drive. This kind of code can be changed to add more functionality. For example, instead of using "data" as the filename, a subject number could be used. Note that in the demo version there is a field on the first card for entering a subject number, the contents of this field could be used to define the filename for the data file.


#Data-analysis

If you have created the Stroop experiment and run yourself in it, then you should have created a datafile with 96 lines that looks something like the shortened version below:

	1	blue	blue	congruent	1389995871068 1389995871785 b
	2	blue	blue	congruent	1389995872788 1389995873384 b
	3	yellow	yellow	congruent	1389995874388 1389995875191 y
	4	red	blue	incongruent	1389995876195	1389995877182 b
	5	red	blue	incongruent	1389995878186	1389995878886 b
	6	yellow	yellow	congruent	1389995879889 1389995880629 y
	7	yellow	yellow	congruent	1389995881632 1389995882259 y
	8	blue	blue	congruent	1389995883262 1389995883811 b
	9	green	red	incongruent	1389995884815	1389995885514 r
	10	green	blue	incongruent	1389995886517 1389995887321 b
	11	blue	blue	congruent	1389995888325 1389995888801 b
	12	green	green	congruent	1389995889804 1389995890536 g
	13	blue	yellow	incongruent	1389995891540 1389995892263 y
	14	red	red	congruent	1389995893266	1389995893830 r
	15	yellow	yellow	congruent	1389995894833 1389995895365 y
	
The next step might be to get the mean reaction times for congruent vs incongruent trials. This involves finding all of the reaction times for each trial, then separating them into congruent and incongruent types, and finally computing the average for each type.

Here is a straightforward approach using a repeat loop. This assumes you have opened a new stack for accomplishing the analysis. Field 1 could contain the data, and field 2 could be reserved for the output of the analysis.

	repeat for each line n in field 1
		put word 6 of n - word 5 of n into RT -- computes reaction time
		if word 4 of is congruent then
			put RT & "," after CongruentVar
		else
			put RT & "," after IncongruentVar
		end if
	end repeat
	put "Congruent" & tab & "Incongruent" & return after field 2
	put average(CongruentVar) & tab & average(IncongruentVar) after field 2
	
##Batch-analysis

The next section deals with the problem of analysing multiple data-files. This section will be updated shortly.




