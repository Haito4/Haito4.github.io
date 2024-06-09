---
weight: 200
title: "Project Log"
description: ""
icon: "list_alt"
date: 2023-11-24 12:00:00
date: "2024-05-10T09:23:34+10:00"
lastmod: "2024-05-10T09:23:34+10:00"
draft: false
toc: true
scrollSpy: true
---

# Part 1
## 24/10/23

{{< img src="img/log/image1.png" alt="image1" resize="600">}}



Downloaded and unzipped juce framework folder.

----

## 5/11/23
Begun researching the process of creating a pitch shifting algorithm.

Took notes regarding important aspects of hop size, window functions, waveform similarity, and the SOLA algorithm.

----

## 6/11/23
Continued researching the process of a phase vocoder. Began installing c++ requirements in visual studio.

----

## 11/11/23
Cloned latest JUCE develop code, installed xcode 13.2.

Then built the projuicer application with xcode.

{{< img src="img/log/image2.png" alt="image2" resize="600">}}

Built an empty standalone plugin application.

{{< img src="img/log/image3.png" alt="image3" resize="600">}}

Created local git repository for the project folder with fork application then pushed source code to github repository for an online backup.

{{< img src="img/log/image4.png" alt="image4" resize="600">}}

Created a readme file online in the github repository then pulled the change to the local folder.

{{< img src="img/log/image5.png" alt="image5" resize="600">}}

{{< img src="img/log/image6.png" alt="image6" resize="600">}}

Readme file was added, so it worked.

----

## 14/11/23: Starting Practice Project
Started following a tutorial on making an EQ plugin to learn the framework. 

Following the framework structure, I created a parameter layout to be given to the application.

![image7](img/log/image7.png)

To start with, it is blank, so in PluginProcessor.cpp I defined the layout of each parameter within the main parameter layout.

The first 6 parameters use a normalisable range, which allows you to select any value in a specified range.

![image8](img/log/image8.png)

![image9](img/log/image9.png)

The last two parameters use a choice within an array, instead of a value in a range.

Defined stringArray to provide the options, then put it into the AudioParameterChoice definition of LowCut Slope and HighCut Slope.

Since I have not created any GUI yet, if I ran it now nothing would show except for the blank hello world template that is preloaded.

![image10](img/log/image10.png)

Rather than using SimpleEQAudioProcessorEditor (which will eventually run the GUI), I replaced it with GenericAudioProcessorEditor. This should show all available parameters rather than the GUI (which currently doesn’t exist).

When I tried to build and run to see if the parameters would show, the text output showed “JUCE assertion failure”. This prevented the application from running despite the fact that the build succeeded.

![image11](img/log/image11.png)

The output said the source is in juce_AudioProcessor.cpp at line 442.

![image12](img/log/image12.png)

A forum comment recommended to remove the line containing jassertfalse to fix the problem. I removed it, but then everything underneath became an error, while saying “expression expected”. This also stopped the build from running completely.

Then I looked closer and saw that jassertfalse is within an instance of std:call_once().

I figured that if I could just remove it from the expression’s output, but keep the structure, it would work without creating more errors beneath from breaking the structure of the framework.

So, I created a copy of the original line in comment form, then purely removed the jassertfalse.

![image13](img/log/image13.png)

After compiling and running this time, it finally worked.

![image14](img/log/image14.png)

All the parameters that were defined before now show up in their appropriate representation, at their default value that was set.

![image15](img/log/image15.png)


The range parameters are slidable and the choice parameters show the four choices that were defined in the string array.

![image16](img/log/image16.png)


Added changes as commit to the github repository.

![image17](img/log/image17.png)

----

## 29/11/23
Worked on social and ethical considerations for the solution. These include accessibility and privacy.

----

## 30/11/23
Expanded on data types and data structures in documentation.

----

## 5/12/23
Worked on pseudocode algorithm documentation for the noise gate.

Expanded on relevance to the user’s hardware environment.

Built standard noise gate plugin as VST3 and tested with audio file in an audio plugin host.

The threshold and alpha settings were adjustable, and functionally worked.

![image18](img/log/image18.png)

----

## 12/12/23
Completed data flow and context diagrams.

Expanded on boundaries of the problem, data types and structures.

Began a new iteration of noise gate pseudocode.

----

## 13/12/23
Revised and finished noise gate pseudocode. Added relevant context for variables.

Finished selection of programming language section.

Made flowchart for the noise gate algorithm.

Finished structure chart.

Finished system flowchart.

Finished data dictionary.

----

## 14/12/23
Finished all scenes in the storyboard and arranged them into a single image. Finished the pseudocode for IR, overdrive, amplifier, and reverb algorithms.

----

# Part 2

## 2/01/24
- Added juce dsp library
- Bound sliders to dsp parameters
- Fixed negative quality slider which was causing a 12dB crack. Did this by changing the minimum value for Q from -24.f to 0.1f
- Also adjusted skewfactor for frequency related parameters

----

## 6/01/24
- Connected parameters to a butterworth filter to allow a low cut frequency interaction
- Adjust how the chain settings are defined for lowcut and highcut slope

----

## 9/01/24
- Refactored code into void functions to avoid repetition of code for each of the two audio channels.
- Finalised EQ DSP, now all parameters control their own DSP function.

----

## 14/01/24
- Created custom GUI sliders to control each parameter.

----

## 18/01/24: Starting The Actual Project
Created Artisian DSP plugin project.
Worked on creating a structure that allows for different GUI scenes to contain different contents while also being selectable via user interactable buttons.
### **Scene 1**

![](img/log2/feb/18-01-24.png)

### **Scene 2**

![](img/log2/feb/2024-01-18.png)

The scripts are structured so that each scene has its own c++ file.

![](img/log2/feb/2024-01-18n2.png)

MultiSceneComponent is the manager of the scene1 and scene2 component scripts, which changes the visibility of each scene as the other is selected.
This function is then called from the PluginEditor, which actually draws it to the plugin's GUI.

![](img/log2/feb/2024-01-18n3.png)

I will have to add more scenes for each processor in the final version, but for now, this test works with no errors, making it a good spot for an emergency rollback should everything break.

----

## 19/01/24: All Scenes
Today I created the rest of the scenes to be used in the final version for each effect.
Each scene has text in the centre displaying the name of the effect.

![](img/log2/feb/2024-01-19.png)

In the scene manager script, there is a lot of repetition, as each scene does the same thing - showing itself while hiding the others.

![](img/log2/feb/2024-01-19n2.png)

![](img/log2/feb/2024-01-19n3.png)

Later I will find a way to optimise this to minimise the repeated code, but for now it works.

I also updated the names for each script. Rather than Scene1Component, Scene2Component, etc, each component has the name of its function before the number. This is just to make navigating and calling upon each function easier.

![](img/log2/feb/2024-01-19n4.png)

----

## 22/01/24
Began working on the overdrive. Started by adding the knobs to the scene. Need to fix.

update: tried to fix it but it is still brokey.
getting juce assert error
JUCE Message Thread (1): EXC_BREAKPOINT (code=EXC_I386_BPT, subcode=0x0)

This is probably due to the getState function or the parameters.

----

## 23/01/24
Added these changes to a new branch called method b and checked out back to the previous version. Basically, I'm starting the overdrive thing again.

![](img/log2/feb/2024-01-23n1.png)

Update:
Well it works now for some reason. Test knob is there.

![](img/log2/feb/2024-01-23n2.png)

This is all it is. I feel stupid for trying to salvage old code with outdated functions.

![](img/log2/feb/2024-01-23n3.png)

Created the other two knobs for the overdrive. I will fine tune the position and size later, but for now they work and show up on the overdrive scene in almost the centre.

![](img/log2/feb/2024-01-23n4copy.png)

Position of knobs is x of last + 90 at 270 y.

![](img/log2/feb/2024-01-23n6.png)

Made a parameter layout that i tried to link to the knobs with no luck. Deleted all of that as it was creating error after error.
Here is what I will keep.

![](img/log2/feb/2024-01-23n7.png)

----

## 14/02/24
I've been trying to make an always-visible input gain rotary knob. After dealing with a lot of errors, I created a new project to test if it would work on a blank slate. It did. I compared the new project with my project and found that in PluginProcessor.h I was including PluginEditor.h. I removed that and it just worked.

![](img/log2/feb/2024-02-14.png)

I will need to change the size and link it to the parameter, but for now I am glad that it works again.

----

## 16/04/24: Input Gain Slider
Finished the implementation of the input gain slider. It has a range of -15.0f to 15.0f. It returns a float value that is converted to decibels and then multiplied by the current sample from the buffer to either increase or attenuate the volume of the incoming signal.

![](img/log2/feb/2024-02-16n1.png)

![](img/log2/feb/2024-02-16n2.png)

![](img/log2/feb/2024-02-16n3.png)

![](img/log2/feb/2024-02-16n4.png)

when the slider value changes, it also checks if the slider is at the minimum value, and if so it makes the variable affecting the sample data a much smaller number, effectively muting it.

----

## 19/02/24
Began creating a function to resize the application window while maintaining aspect ratio. 

![](img/log2/feb/2024-02-19n1.png)

Right now, I've implemented a combo (dropdown) box in the bottom right corner. When pressed , the user receives three options - small, medium and large, which will be used to determine the size of the application window when I finish its logic.

![](img/log2/feb/2024-02-19n2.png)

----

## 20/02/24: Resizing With A ScaleFactor
Finished the logic for the three stages of window resizing.
This function is called whenever the combobox (called resizenator) is adjusted. Based on the selected option, the width, height and uiScaleFactor variables are adjusted.

![](img/log2/feb/2024-02-20n1.png)

![](img/log2/feb/2024-02-20n2.png)

After updateResolution is called, the canvas size is readjusted using the newly updated width and height variables.

![](img/log2/feb/2024-02-20n3.png)

    (The initialisation of the combobox and its options)

To actually adjust the elements within alongside the canvas, I multiplied all the coordinates and size values for each element by the scalefactor. By default it will be 1, and work off of the standard resolution of 720 x 540, and then adjust the values according to the new size option.

![](img/log2/feb/2024-02-20n4.png)

At the moment, though, I've only applied it to the input/output knobs and the resizing selector itself. I will need to send the variable to the multiScene script also for the scene selectors at the top to resize. The resolutions could also use some adjusting, ideally I will need to find a way to scale them off of the user's monitor resolution.

### **Small Size**

![](img/log2/feb/2024-02-20n5.png)

### **Medium Size (Default)**

![](img/log2/feb/2024-02-20n6.png)

### **Large Size**

![](img/log2/feb/2024-02-20n7.png)

----

## 27/02/24: Wrapper-Based Resizing
My scaling method works perfectly fine when resizing the window. However, I could not pass the uiScaleFactor variable to the multiSceneComponent and its child buttons since it is in a seperate script. It is either impossible or I'm just stupid

```
Note (21/05/24): I was stupid
But this new method is better anyway
```

After searching, I came across a better method. Rather than use a scale factor variable that is applied to every single child component of the editor, a wrapper can be made, assuming the role of the editor (drawing the displayable application window). 

Also, all of the displayable area of the window, including all of the components can be added as a single component to the wrapper.

Because the wrapper contains a single full-sized component all the time, it can be scaled on its own according to the wrapper.

Here it is, after implementation, and it works smoothly.

![](img/log2/feb/2024-02-27.gif)

----

## 28/02/24: Input Meter
Added functionality to save and recall the plugin's size when closed and reopened.
Also added a bottom bar and repurposed the size selection combobox for preset selection.

![](img/log2/feb/2024-02-28n1.png)

I added an input meter on the left side to represent the program's incoming audio.

![](img/log2/feb/2024-02-28n2.png)

In action:
![](img/log2/feb/2024-02-28n3.gif)

----

## 1/03/24: Source Organisation
Improved the organisation by moving the component definitions to their header files, then deleting their source files.

![](img/log2/march/2024-03-01n1.png)

![](img/log2/march/2024-03-01n2.png)

The directory is heaps more manageable now.

![](img/log2/march/2024-03-01n3.png)

----

## 6/03/24
Created ui elements in an illustrator canvas so I can export them as svg's for use as icons.

----

## 8/03/24: Output Gain
Added output gain adjustment using the output gain knob. Still trying to figure out the best way to structure effect processing.

![](img/log2/march/2024-03-08.png)

----

## 10/03/24
I tried to set up the AudioProcessorGraph, but it just wouldn't work. This means I will just be using variables to write the algorithms within the processBlock. 
As a test, I defined a boolean called in PluginProcessor.h called usingGate to represent the gate's state, starting off as false.

![](img/log2/march/2024-03-10n1.png)

Then in my gate component header, I defined the button type, text, and its actual function - to just return the opposite of whatever usingGate is when pressed (using ! to get the opposite bool value).

![](img/log2/march/2024-03-10n2.png)

    This screenshot is the working version.

To get the usingGate variable from PluginProcessor.h to this script, I needed to get the Gate1Component constructor to accept a reference to ArtisianDSPAudioProcessor.
But in the MultiSceneComponent script, where gate1component is called, it was not receiving the processor reference, so I had to add that:

![](img/log2/march/2024-03-10n3.png)

But, to actually do that the MultiSceneComponent constructor needed to receive it too.

![](img/log2/march/2024-03-10n4.png)

But, this header was also getting the processor reference from nowhere. 
That meant I needed to pass the processor to the MultiSceneComponent when it was called, this time in the PluginEditor script.

![](img/log2/march/2024-03-10n5.png)

Thankfully, because the PluginEditor already works for some reason, this is where the hoops end.

So, by going from PluginProcessor.h  ---> PluginEditor.h ---> PluginEditor.cpp ---> MultiSceneComponent.h ---> MultiSceneComponent.cpp ---> Gate1Component.h, I can access usingGate by prefixing it with "audioProcessor."

And by doing that, I could finally change the variable.

![](img/log2/march/2024-03-10n6.gif)

----

## 12/03/24: APVTS
Today I implemented an Audio Value TreeState for the processor. It's basically a list that can contains all of the program's processors, and stores their values within a file. Using this will make preset management much simpler when when I need to do that.

In the processor, I add parameters within the createParameters function with params.add (parameter id, parameter name, min value, max value, default value), and then params is returned into the apvts in its declaration the constructor.

![](img/log2/march/2024-03-12n1.png)

The current parameters in there are for the noise gate.

To start, I wanted to create a knob that could control the threshold, so in my gate script I created a slider (thresholdSlider) and set its values to match the parameter.
Then I defined a slider attachment called thresholdAttachment, which let me attachment the threshold parameter to the threshold slider.

![](img/log2/march/2024-03-12n2.png)

![](img/log2/march/2024-03-12n3.png)

Then, to test, back in the processor, I wrote code to output whatever the current value of the threshold parameter is to the console, in this function. Whenever any parameter value is changed, the function gets called again.

![](img/log2/march/2024-03-12n4.png)

![](img/log2/march/2024-03-12n5.gif)

And it works, so I now have a reliable way to bind the sliders and buttons from the component scripts to the values in the apvts, which I can then chuck into the processor's algorithms.

I also wrote a baseline kind of noise gate algorithm using the threshold value.

![](img/log2/march/2024-03-12n6.png)

It works alright and the threshold slider reacts how it should when audio is above and below, but if the audio is sitting very close to the threshold, it will start crackling. This is probably because the change in audio level is made instantly, rather than over a timeframe. When I implement attack and release times, it'll probably help.

----

## 19/03/24: I am terribly sad
Trying to implement the attack and release time, but my xcode doesn't seem to like exponential functions, which I kind of need. I tried fixing it, but now I broke everything. Now it won't launch.

![](img/log2/march/2024-03-19.png)

----

## 21/03/24
So that error went on to cause a lot of pain, but I've kind of found a solution. The error seemed to stem from a code signing issue, where my apple developer id certificate or whatever stopped working, preventing me from being able to finish the build.

I tried lots of different methods on the JUCE forums which did not work. A lot of them did suggest to build with cmake, rather than JUCE's built in exporter Projucer.

I found this tool on github called FRUT, which seemed to replace the role of projuicer, using cmake.

![](img/log2/march/2024-03-21n1.png)

So then I installed cmake, then its command line tools, then cloned FRUT into a local folder, and then I followed the installation guide and blindly copy pasted all of this stuff into the terminal

![](img/log2/march/2024-03-21n2.png)

Then I just like used the cmake GUI cause its easier

![](img/log2/march/2024-03-21n3.png)

Here I generated all of the files that xcode will need to build with cmake.

Then I opened the xcode project file and building didn't work.

![](img/log2/march/2024-03-21n4.png)

So I commented it out so I can forget about it and only have to worry later

![](img/log2/march/2024-03-21n5.png)

Then it like full actual ran perfectly fine like before

![](img/log2/march/2024-03-21n6.png)

i am happy


free smiley ru gif

----

## 23/03/24 Attack and Release is Working

Yippee

![](img/log2/march/2024-05-13.png)

----

## 26/03/24: Notion

Today I started to migrate the documentation to a notion site.

----

## 12/04/24
I started trying to make sense of cmake and add some images to my project to use as buttons.
It didn't work.
I'll figure it out later.

----

## 20/04/24: Back to projuicer, Mono Input & Optimisation
Noise gate broke even though I changed nothing. Why man

Update : I fixed the cmake problem in that I don't have to use it anymore. I cloned my repository to a new folder then rebuilt it with the projuicer file and it seems to work for now. It's named ArtisianDSP2 now so that it doesn't interfere with the previous version still on my computer.

I updated the plugin to only have mono input, which helps to minimise cpu usage and audio artifacts that I was getting before.

![](img/log2/april/2024-04-20n1.png)

I simplified the noise gate algorithm to use scalar variables, rather than vector ones, since there is no need for dual values with only one channel. Everything is much much smoother sounding now, because now there's only one gate catching every, rather than two that are slightly out of sync.

![](img/log2/april/2024-04-20n2.png)

![](img/log2/april/2024-04-20n3.png)

I still haven't implemented hold time, which I might consider doing later, but at the moment it works pretty well, so I don't think there's any need for it.

Also at the end I copy the processed audio to the other output channel, so that it's not just left empty.

![](img/log2/april/2024-04-20n4.png)

### **Noise Gate Testing**
Here's an example of it working. When the signal is quieter in between attacks, it dampens, while letting the louder stuff through. 
It works like a noise gate should thankfully.
When the threshold is really high, it mutes pretty much everything (visible on the right side of the meters), only the absolute loudest parts getting through for very short durations.
And when the threshold is low, it lets everything in (meters stay the same).

{{< video "/img/ngTesting-Letter_Experiment.mp4" "Letter Experiment Noise Gate Testing" "player-wrapper-1">}}

Once I put in the amp and cab processes, I'll be able to properly test it with a real guitar signal, and see if it needs any refining for realtime playing.

----

## 21/04/24: Apvts migration
Moved the input and output gain parameters to the apvts so I can save their state in the xml file

![](img/log2/april/2024-04-21.png)

The noise gate toggle button wasn't switching between true and false though, so I will have to fix later

----

## 23/04/24
Made the gate toggle work for now. It also updates its ui depending on the state.

![](img/log2/april/2024-04-23n1.png)

When the parameters are updated, the gate's status gets the parameter value from the apvts which is linked to the button. I've made the button toggleable so it acts how you would expect.

![](img/log2/april/2024-04-23n2.png)

### Why Command PhaseScriptExecution failed

Also, I got the Command PhaseScriptExecution failed with a nonzero exit code error again, after running the plugin in standalone to test gui positioning (all my other testing before was with the vst3 version).

Because I fixed the problem the other day by regenerating the build files from the projucer project in a new directory, I knew it was just a build configuration messing up that needed to be regenerated.

So in the project folder I deleted the builds folder and then regenerated them with the jucer file

![](img/log2/april/2024-04-23n3.png)

And then it ran fine
I am very glad

![](img/log2/april/2024-04-23n4.png)

So it ended up being the build files getting corrupt when trying to build the standalone application. 

So do that if it happens to you

----

## 24/04/24
I began working on the tube screamer stuff today

![](img/log2/april/2024-04-24n1.png)

    Parameter Layout Updates

I started with the tone knob of the tube screamer, which in the actual pedal removes some of the lower frequencies to make the output sound less "muddy"

Juce has a built in dsp module with a high-pass filter that does exactly this

So I declared it in the header:

![](img/log2/april/2024-04-24n2.png)

Then gave it its initialisation needs

![](img/log2/april/2024-04-24n3.png)

Attached the tone slider to the tone parameter

![](img/log2/april/2024-04-24n4.png)

Added this so that it can update its parameters when the slider value changes

![](img/log2/april/2024-04-24n5.png)

And then when I need to apply it in the process block, I replace the channelData of the current sample with the processed data

![](img/log2/april/2024-04-24n6.png)

Heaps easier than making it manually


### **HPF Testing**
You'll hear that when the slider goes up, the lower frequencies start to die down

{{< video "/img/TubeScr-HPF.mp4" "Tube Screamer Filter Testing" "player-wrapper-2">}}

----

## 25/04/24: Tube Screamer Functional
I found this third party juce module called melatonin inspector, which lets you move around gui components freely like in photoshop. I added it to the repository as a git submodule, then used it to improve some of the positioning.

It can't save these changes directly to the components, so I just noted down the new scale and position for each of them then replaced their old values in the resized() method.

![](img/log2/april/2024-04-25n1.gif)

I put in a toggle button and waveshaper for the tube screamer, so its at a functional level now.
The structure of it is high-pass filter -> waveshaper -> level adjustment

![](img/log2/april/2024-04-25n2.png)

And I'm using the jlimit function to stop it from blowing my eardrums out

The waveshaper looks like this as a graph:

![](img/log2/april/2024-04-25n3.gif)

When drive value increases, the steepness of the curve does as well.
This steeper curve will allow the audio data to clip, which is what causes the distortion effect.

![](img/log2/april/2024-04-25n4.png)

    (Example of clipped audio - the peaks are cut off)

### **Tube Screamer Testing**
Here's what it sounds like with a DI guitar signal

{{< video "/img/TubeScrOD.mp4" "Tube Screamer Overdrive Testing" "player-wrapper-3">}}

The audio distorts as the drive knob goes up, but the increasing of the really low frequencies gives it a muddy sound.
The tone knob compensates for this, and cuts out all the frequencies leading up to whatever value its set to, making it sound much clearer.
And the level just changes the level.

I'll probably try to expand on the waveshaper soon, because past 100 there isn't much change.

----

## 27/04/24: Moving Documentation to Website
Notion kinda wasn't cutting it

Installed Homebrew, ruby and jekyll to make a static site for the documentation

Made a site using a jeckyll template called chirpy

![](img/log2/april/2024-04-27n1.png)

Converted my word document to markdown with an online converter then started importing it into the site.

![](img/log2/april/2024-04-27n2.png)

There's still some formatting errors that I need to fix.

Took a long while but I managed to embed a local video file in the site, so I'll be able to use them as examples finally.

Spent ages on trying to deploy to github pages. I got it to work finally after removing leftover image text from the docx to markdown converter

![](img/log2/april/2024-04-27n3.png)

Migrated the first half of the project log to a new page

![](img/log2/april/2024-04-27n4.png)

The images aren't loading in the github pages deployment and i dunno why

![](img/log2/april/2024-04-27n5.png)

It ended up being something stupid in the end

![](img/log2/april/nobrokeyanymore.gif)

I was calling all my images like ``![image1](Assets/img/log/image1.png)`` , 

but my actual folder directory is ``![image1](assets/img/log/image1.png)``. 

----

## 29/04/24: Compressor
I started doing the compressor today. I'm just using the juce compressor dsp module for it.

![](img/log2/april/2024-04-29n1.png)

From left to right its got ratio, attack, release, threshold and the toggle switch.

![](img/log2/april/2024-04-29n2.png)

The compressors parameters are updated in the shouldupdate block,

![](img/log2/april/2024-04-29n3.png)

and the samples are sent through it if the toggle switch is true.

![](img/log2/april/2024-04-29n4.png)

Kind of a black box solution for now, cause I want to start to focus on the amplifier and cab sims

----

## 5/05/24
Forwarded the processor reference to the rest of the components.

![](img/log2/may/2024-05-05.png)

----

## 9/05/24: Impulse Response Loader
### **ImageButton**
Loaded a test image to use as a button for the effect bypass switch

![](img/log2/may/imagebutton.gif)

### **IR Loader**
I also ended up figuring out how to use the convolution module which means the ir loader now works at a barebones level

In the preparetoplay function, I load an IR file that I added to the projucer project. This is just a free one I downloaded from ml sound lab

![](img/log2/may/2024-05-09n1.png)

And at the end of the processblock I run the data through the filter if usingIR is true

![](img/log2/may/2024-05-09n2.png)

Here's what it sounds like:

{{< video "/img/IR-loader.mp4" "IR Testing" "player-wrapper-4">}}

Theres an obvious drop in volume though, so I'll have to boost the gain a little bit afterwards

Here it is with a different audio input and the actual gui. In this one I adjusted for the drop off in db with the output knob. (Output slider didn't do anything in the generic parameter editor from before)

{{< video "/img/mtd-irtesting.mp4" "Make Total Destroy DI IR Testing" "player-wrapper-5">}}

It's starting to sound pretty good, chugs could sound better but they'll develop well when I introduce the amplifier into the mix.

All I need now is to add a way to select your own IR files, the amp, reverb, presets and it should be pretty much done.

----

## 10/05/24: Moving Website to Hugo
I decided to rebuild the website with hugo, rather than jekyll, as it's known to be faster and more efficient. I found this theme called lotus docs which ticked my one real requirement - having floating table of contents on the side.

You can also scroll through the toc if it spills out of the screen, which is a good plus

![](img/log2/may/2024-05-10n1.png)

Also was able to change up the landing page to be fancier

![](img/log2/may/2024-05-10n2.png)

----

## 11/05/24
Added a gain boost in the IR section to compensate for the convolution function's volume loss.
![](img/log2/may/2024-05-11.png)

----

## 12/05/24: Amp EQ
I made three peak filters to use as the amplifier's EQ stage.

![](img/log2/may/2024-05-12n1.png)

Each parameter is between the range of 0 and 2, where 1 is halfway and the default noon value.

![](img/log2/may/2024-05-12n2.png)

When parameters update, I assign each parameter to their respective variable but lock them within the range of 0.01-2 (because a gain factor of 0 will just attenuate the signal completely). 

![](img/log2/may/2024-05-12n3.png)

Then I update the coefficients of each filter, for the new bass/mid/treble values.

Here's what it sounds like with only itself and the overdrive (with its high pass filter disabled).

{{< video "/img/AmpEQ.mp4" "Amplifier EQ Stage" "player-wrapper-6">}}

----

## 13/05/24: Migrating Project Log
Spent all day transferring my project log from obsidian to the website's markdown file (this page) and trying to embed the videos and images properly. Lots of manual file renaming torture because macos screenshots like to have lots of random spaces and have the date in the middle of the file name.

I wasted a lot of time trying to get an image zoom on click script to work and gave up after like 4 hours

The next (or first) thing I needed to fix was embedding videos.

Normally in markdown you embed images like this:
```markdown
![](img/log2/may/mishuggah.png) 
```
Which outputs:
![](img/log2/may/mishuggah.png)

But if you do the same thing with a video
```markdown
![](img/log2/may/mishuggah2.mp4) 
```

You get one of these ones (the whole site breaks):

![](img/log2/may/sitebrokey.png)

It turns out that hugo has no support for the embedding of local video files which suck. Luckily though I found someone who did it already: https://dev.to/hi_artem/add-a-video-to-your-hugo-website-104

It's a html file that creates some Hugo shortcode to embed a video using a video player called Clappr.
I added it to my project, and it worked with external links, but local videos were breaking.

It was breaking when I had two videos on the same page, so I added another field for the element's html id, to make each one unique. (at the .get 2 parts)

```html
<div class="container">
  <div id="{{ .Get 2 }}" class="{{ .Get 1 }}"></div>
</div>

<script
  type="text/javascript"
  src="https://cdn.jsdelivr.net/npm/@clappr/player@latest/dist/clappr.min.js"
>
</script>

<script>
  var playerElement = document.getElementById("{{ .Get 2 }}");

  var player = new Clappr.Player({
    source: "{{ .Site.BaseURL }}{{ .Get 0 }}",
    mute: true,
    height: 360,
    width: 640
  });

  player.attachTo(playerElement);
</script>

```


Then they embedded properly

![](img/log2/may/siteworkey.png)

----

## 15/05/24: IR File Chooser
Started adding the part 3 and 4 headings to a new markdown file for the documentation.


Made a file chooser for the ir loader. When the button is clicked, it opens a file chooser and assigns the selected wav file to a variable. From there it's passed into the impulse response loader in the processor script.

![](img/log2/may/2024-05-15n1.png)

{{< video "/img/irSelectorWorking.mp4" "IR File Chooser" "player-wrapper-7">}}

----

## 16/05/24
Had 3rd progress meeting.

----

## 17/05/24
Made a hugo shortcode script to resize and optimise my images

![](img/log2/may/2024-05-17n1.png)

Removed the default home page by auto redirecting to the documentation.

![](img/log2/may/2024-05-17n2.png)

I also implemented a waveshaper for the preamp stage of the amplifier.

![](img/log2/may/2024-05-17n3.png)

----

## 19/05/24
Worked on all of the GUI positioning to make everything flow nicer

![](img/log2/may/2024-05-19.png)

----

## 20/05/24
Added some more parameters to the amplifier, mainly resonance and presence.

![](img/log2/may/2024-05-20.png)

----

## 21/05/24: Reverb
Added reverb in between the amp and the cab

I've set it up to run two reverbs in parallel, one for left and one for right

![](img/log2/may/2024-05-21n1.png)

The reverb dsp includes its own parameter holder, so in the shouldupdate part, I just directly assign the GUI parameters to it rather than first sending them into variables.

![](img/log2/may/2024-05-21n2.png)

### **Demo**

{{< video "/img/tulpareverb.mp4" "Reverb Testing" "reverb-player">}}

----

## 22/05/24
Worked on the program development & techniques section of the documentation.

Started making the svg for the amplifier in illustrator.

![](img/log2/may/2024-05-22.png)

----

## 23/05/24
Continued on the amp svg

----

## 26/05/24
Added a level adjustment knob for the compressor
Added a custom knobs component called jb knobs for the amp's sliders.
And a new pair of images for the power toggle.

![](img/log2/may/2024-05-26n1.png)

Also added a new image for the pedal bypass switch, so it looks like an actual bypass switch

![](img/log2/may/2024-05-26n2.png)

----

## 27/05/24
Finished the code generation section of Program Development & Techniques.

In the Process of detecting and correcting errors, finished the Syntax Checking, Logic Errors, Desk Checking, Use of expected output and runtime errors sections.

Made some adjustments to the video player script on the website so that they're responsive to browser size.
The main change is that the position of the video container is relative, and the max width is by default 60% of the browser's screen. When it's underneath 1025 pixels wide, the max width is 100%.

![](img/log2/may/2024-05-27.png)

### Before

![](img/log2/may/mobilebefore.gif)

![](img/log2/may/desktopbefore.gif)

### After

![](img/log2/may/MobileAfter.gif)

![](img/log2/may/DesktopAfter.gif)

----

## 28/05/24
Finished the **design of individual screens** section found under the interface design part of the documentation.

Started the use of software debugging tools

----

## 29/05/24
Started working on the preset management system.

----

## 30/05/24
Finished the use of software debugging tools, started user documentation parts of the documentation.

Kept going on the preset manager

----

## 1/05/24
Finished the preset manager basis.
Ive spent ages on trying to get the ir loader to work with it, but its very finnicky

Right now ive got a problem where the selected ir will only be the previously selected one.

IR 2 loaded, but says and loads IR 1.
Switch to IR 3 preset, but says and loads IR 2.
This means that the previously selected preset is being loaded when a new preset is loaded.
  
This means that the irs are being loaded before the variables are changed,
which means that before loadpreset() is finished executing, valuetreeredirected() in impulse6component is setting the already loaded ir.

----

Alright I half did it finally.

In my loadpreset() function, set the lastIr path and name variables to the attribute found in the xml file.

After, I check if its a valid file that exists, and if so, I set a boolean to true, that loads the new file in the processor script.

![](img/log2/june/2024-06-01n1.png)

![](img/log2/june/2024-06-01n2.png)

Here's me going through some example presets. They all have relatively similar effect settings, but just different IRs. I've also got some debug statements that confirm the currently selected IR. Some presets do not contain an IR, that fulfil the else case of that if statement.

{{< video "/img/Ir_preset_testing.mp4" "Impulse Response Preset Testing" "irpresetTest-player">}}

I still have few problems that I need to fix. One is that the text on the GUI is the name of the previous IR selected. Better than having the previous IR loaded, but still necessary.

I also need to make a prompt if the IR location is invalid, because say if someone were to share a preset, they would need the option to select its directory on their own machine.

The last thing is recalling the loaded IR when you close and open your DAW again. At the moment, if you load an ir or preset, it will forget the IR when you close the app, which is inconvenient for any user. Sliders and buttons keep their state fine at the moment though, which I'm glad of.

----

## 3/05/24
Finished the process of detecting & correcting errors, user documentation, and started technical documentation parts of the documentation.

Fixed the issue where the IR name was stuck on the previous preset's ir name. 
I did this by creating a new variable tree in the processor and assigning the new ir name to one of its properties.

![](img/log2/june/2024-06-03n1.png)

Then in the impulse response GUI, I can use a listener to update the label only when that property changes.

![](img/log2/june/2024-06-03n2.png)


I made a button to fix the path of the broken IR that appears only when an invalid IR is loaded from a preset. In the same listener, I set it to visible, if the IR is invalid. When clicked, it functions the same way as the normal ir loader button.

#### Working (normal preset):

![](img/log2/june/2024-06-03n3.png)

#### Broken (fixable) preset:

![](img/log2/june/2024-06-03n4.png)

(I'll readjust the positioning later)


### Complications
When making it, I ran into an error where the fix button would hang around, even when going back to a working preset. It would also stay hidden after fixing a preset and then switching to another broken one.
After a bit of debugging, I figured out that the line where I set the new property, will always be the same error string.
```cpp
audioProcessor.variableTree2.setProperty("NEW_IRNAME", "Invalid IR File!", nullptr);
```

 I realised that resetting the property to the same string would not tell the listener, so I made an if statement in the load preset function.

![](img/log2/june/2024-06-03n5.png)

In the case of an invalid IR, I set a new property that is between one of two choices. When one is transmit, the bool value is flipped, so that the next one will be the other.

Then, in the listener, it checks if the IR was valid. An invalid IR will always have the same error message, which is set here. A valid one will get the string of the property that was changed and give it to the button.

![](img/log2/june/2024-06-03n6.png)


At the moment, this only fixes the currently loaded IR, which means I still have to include functionality for it to write the the path to the existing preset file.

----

## 4/06/24
**Code changes:**
https://github.com/Haito4/ArtisianDSP/commit/058ec966356a6ddf29c52c174938109fee41b9e8

Started working on part 4 of the documentation - comparing to the original design specifications.

I added the functionality for updating the old preset file with the new IR information. Luckily, because of the foundation I laid out yesterday, it was fairly simply to implement.

When the load preset function is called, before the attributes are updated, I set a variable within the audio processor to the path of the newly selected preset file, so it can be accessed by the impulse loader component.

![](img/log2/june/2024-06-04n1.png)


Within the impulse component, at the end of the fix button's onclick lambda, I use that path to create a file reference, open it as an xml, and set the attributes to the new values. Throughout it there are some debug statements which helped identify points of failure.

![](img/log2/june/2024-06-04n2.png)

### Preset Path Updating
Here's a video testing the new changes. I start off on an old preset called obzen from an earlier system that doesn't even have the IR path and name fields.

When I click fix, I choose a new wav file, and it gets loaded successfully like before.

The difference is now, when switching to another preset and back to the obzen one, it switches back to the wav file I selected with the fix button.

{{< video "/img/presetmanagerWorkingwell.mp4" "Preset Manager Working Well" "presetManagerWW-player2">}}

After, I also made some changes to immediately load the current IR the last selected preset when the plugin is launched, so that the user can avoid listening to the fizz of the plain amp.

The next (and last) step I can do on this is including support for wav files loaded into the binary data of the program, that do not exist in a directory. To do this, I'll probably need to include a new identifier called something like "usingbinaryIR" and set it to either true or false depending on the type of IR selected. I'll add the name of the internal IR as well.

Then, with a couple of if statements impacted by those attributes, I'll be able to have presets that work straight out of the box.

----

## 5/06/24
I spent ages trying to get this support working for binary data IRs within the preset system. 

I struggled for a while, but found the source of my problem to be a boolean getting set to true when it needed to stay false within a comboboxupdated listener in the impulse gui component.

Right now it's far too messy to fully explain, but what matters is it works now.

If you want to see just how terrible it is, here is where I gave up:
https://github.com/Haito4/ArtisianDSP/commit/a7e086883d4371b6d28ed001ee6bdf50f94447a7

and here is where I realised the problem:
https://github.com/Haito4/ArtisianDSP/commit/8e9803beab36b11cac3e5e6faa221e415cfc14c7

But yeah now its functional enough for me to not have to worry about it.


Here's what the IR screen looks like now:

![](img/log2/june/2024-06-05.png)

----


## 6/06/24
Added labels to all of the sliders so the user can know what parameter they're changing


Loaded in the SVG file I made before for the amplifier and readjusted the parameter scale & positions

![](img/log2/june/2024-06-06.png)

----

## 7/06/24
Added the help menu which is accessible from a button in the bottom left hand corner

It overlays the screen with a transparent black rectangle to dim the main screen, and whatever I need to include in the menu can go above it, where the placeholder text and box are right now.

![](img/log2/june/2024-06-07.png)

----

## 8/06/24
Finished off the compressor in illustrator and then added it to the program as a binary data SVG.

![](img/log2/june/2024-06-08n1.png)

Then I started trying to put it into the compressor scene.

Because it isn't the width of the window, it was hard to resize correctly

![](img/log2/june/2024-06-08n2.png)

I was able to get the right scale and position by making a rectangle based on the original aspect ratio of the pedal and then filling it with the svg.

![](img/log2/june/2024-06-08n3.png)

I also added a bypass indicator and changed the style of the sliders to match, and removed the existing labels because they're already in the image.

![](img/log2/june/compGUI.gif)

Later, I was doing some testing with the preset system and found a problem. If you delete a preset and then save and close the plugin, reopening the plugin will cause a crash. After debugging, I found that this was because it was trying to load the IR of a nonexistent preset, which can't really happen.

So in setStateInformation(), which is run on launch, executes, I added this if statement before the IR loading:

```cpp
if (!juce::File(presetManager->getCurrentPresetPath()).exists())
    return;
```

which will just exit the function if the path to the preset saved in the plugin's state doesn't exist.
And it fixed it.

----

## 9/06/24
Did a bunch of fixes to the preset system, mainly regarding GUI updates on different IR load states.

Started adding all the tooltips to each parameter.

Each one provides a short explanation of what the parameter does.

![](img/log2/june/2024-06-09n1.png)

In the help menu, I added a button which links to the website.

![](img/log2/june/2024-06-09n2.png)

After, I added a button pointing to the source code and and privacy disclosure.

![](img/log2/june/2024-06-09n3.png)

After, I wrote a few paragraphs about each function of the plugin, and chucked it in a single label. It was kind of troublesome to handle though, because the text would just spill out of the screen. To circumvent this, i made use of a viewport, which is kind of like a window you can peek through to its attached components. Because viewports automatically contain scroll bars, it worked perfectly.

Here's what the final thing looks like, with the links working:

![](img/log2/june/helpscreen.gif)

The last thing I need to do now is add the rest of the pedal images and fix one more IR loading error. After that the plugin's fully done.

----
