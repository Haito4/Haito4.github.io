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


<!--![image1](img/log/image1.png)-->


{{< mediumzoom src="/img/log/image1.png" width="70%" id="zoom-margin" class="medium-zoom-image" loading="lazy" >}}



Downloaded and unzipped juce framework folder.

## 5/11/23
Begun researching the process of creating a pitch shifting algorithm.

Took notes regarding important aspects of hop size, window functions, waveform similarity, and the SOLA algorithm.

## 6/11/23
Continued researching the process of a phase vocoder. Began installing c++ requirements in visual studio.

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
## 29/11/23
Worked on social and ethical considerations for the solution. These include accessibility and privacy.

## 30/11/23
Expanded on data types and data structures in documentation.

## 5/12/23
Worked on pseudocode algorithm documentation for the noise gate.

Expanded on relevance to the user’s hardware environment.

Built standard noise gate plugin as VST3 and tested with audio file in an audio plugin host.

The threshold and alpha settings were adjustable, and functionally worked.
![image18](img/log/image18.png)
## 12/12/23
Completed data flow and context diagrams.

Expanded on boundaries of the problem, data types and structures.

Began a new iteration of noise gate pseudocode.

## 13/12/23
Revised and finished noise gate pseudocode. Added relevant context for variables.

Finished selection of programming language section.

Made flowchart for the noise gate algorithm.

Finished structure chart.

Finished system flowchart.

Finished data dictionary.

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
### Scene 1
{{ $image = resources.Get "img/log2/feb/18-01-24.png" }}

![](img/log2/feb/18-01-24.png)

### Scene 2

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
