---
weight: 2
title: "Project Log"
description: ""
icon: "article"
date: 2023-11-24 12:00:00
date: "2024-05-10T09:23:34+10:00"
lastmod: "2024-05-10T09:23:34+10:00"
draft: false
toc: true
scrollSpy: true
---

# Part 1

## 24/10/23

![image1](/img/log/image1.png)

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


![image2](img/log/image2.png)

Built an empty standalone plugin application.

![image3](img/log/image3.png)

Created local git repository for the project folder with fork application then pushed source code to github repository for an online backup.

![image4](img/log/image4.png)

Created a readme file online in the github repository then pulled the change to the local folder.
![image5](img/log/image5.png)

![image6](img/log/image6.png)
Readme file was added, so it worked.

----

## 14/11/23
Following the framework structure, I created a parameter layout to be communicated to the application.

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

## 19/01/24
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

This is all it is. I feel stupid for trying to salvage 5 year old code using outdated JUCE functions.

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

## 16/04/24
Finished the implementation of the input gain slider. It has a range of -15.0f to 15.0f. It returns a float value that is converted to decibels and then multiplied by the current sample from the buffer to either increase or attenuate the volume of the incoming signal.

![](img/log2/feb/2024-02-16n1.png)

![](img/log2/feb/2024-02-16n2.png)

![](img/log2/feb/2024-02-16n3.png)

![](img/log2/feb/2024-02-16n4.png)

when the slider value changes, it also checks if the slider is at the minimum value, and if so it makes the variable affecting the sample data a smaller number, effectively muting it.

----

## 19/02/24
Began creating a function to resize the application window while maintaining aspect ratio. 

![](img/log2/feb/2024-02-19n1.png)

Right now, I've implemented a combo (dropdown) box in the bottom right corner. When pressed , the user receives three options - small, medium and large, which will be used to determine the size of the application window when I finish its logic.

![](img/log2/feb/2024-02-19n2.png)

----

## 20/02/24
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

## 27/02/24
My scaling method works perfectly fine when resizing the window. However, I could not pass the uiScaleFactor variable to the multiSceneComponent and its child buttons since it is in a seperate script. It is either impossible or non achievable due to my lack of knowledge past adding a new include line.

After searching, I came across a better method. Rather than use a scale factor variable that is applied to every single child component of the editor, a wrapper can be made, assuming the role of the editor (drawing the displayable application window). 
Also, all of the displayable area of the window, including all of the components can be added as a single component to the wrapper.

Because the wrapper contains a single full-sized component all the time, it can be scaled on its own according to the wrapper.

Here it is, after implementation, and it works smoothly.

![](img/log2/feb/2024-02-27.gif)

----

## 28/02/24
Added functionality to save and recall the plugin's size when closed and reopened.
Also added a bottom bar and repurposed the size selection combobox for preset selection.

![](img/log2/feb/2024-02-28n1.png)

I added an input meter on the left side to represent the program's incoming audio.

![](img/log2/feb/2024-02-28n2.png)

In action:
![](img/log2/feb/2024-02-28n3.gif)

----

## 1/03/24
Improved the organisation by moving the component definitions to their header files, then deleting their source files.

![](img/log2/march/2024-03-01n1.png)

![](img/log2/march/2024-03-01n2.png)

The directory is heaps more manageable now.

![](img/log2/march/2024-03-01n3.png)

----

## 6/03/24
Created ui elements in an illustrator canvas so I can export them as svg's for use as icons.

----

## 8/03/24
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

## 12/03/24
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

Also, I got the Command PhaseScriptExecution failed with a nonzero exit code error again, after running the plugin in standalone to test gui positioning (all my other testing before was with the vst3 version).

Because I fixed the problem the other day by regenerating the build files from the projucer project in a new directory, I knew it was just a build configuration messing up that needed to be regenerated.

So in the project folder I deleted the builds folder and then regenerated them with the jucer file

![](img/log2/april/2024-04-23n3.png)

And then it ran fine
I am very glad

![](img/log2/april/2024-04-23n4.png)

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

## 25/04/24
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

## 27/04/24
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

All just a capital character breaking the whole thing.

----

## 29/04/24
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

## 9/05/24
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

{{< video "/img/IRloader.mp4" "testIR" "player-wrapper-4">}}

Theres an obvious drop in volume though, so I'll have to boost the gain a little bit afterwards

Here it is with a different audio input and the actual gui. In this one I adjusted for the drop off in db with the output knob. (Output slider didn't do anything in the generic parameter editor from before)

{{< video "/img/mtd-irtesting.mp4" "Make Total Destroy DI IR Testing" "player-wrapper-5">}}

It's starting to sound pretty good, chugs could sound better but they'll develop well when I introduce the amplifier into the mix.

All I need now is to add a way to select your own IR files, the amp, reverb, presets and it should be pretty much done.

----

## 10/05/24
I decided to rebuild the website with hugo, rather than jekyll, as I've heard it's faster and more efficient. I found this theme called lotus docs which ticked my one real requirement - having floating table of contents on the side.

You can also scroll through the toc if it spills out of the screen, which is a good plus

![](img/log2/may/2024-05-10n1.png)

Also was able to change up the landing page to be fancier

![](img/log2/may/2024-05-10n2.png)

----

## 11/05/24
Added a gain boost in the IR section to compensate for the convolution function's volume loss.
![](img/log2/may/2024-05-11.png)

----

## 12/05/24
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

## 13/05/24
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

![](img/log2/may/sitebrokey.png)

