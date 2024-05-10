---
weight: 2
title: "Project Log"
description: ""
icon: "article"
date: 2023-11-24 12:00:00
date: "2024-05-10T09:23:34+10:00"
lastmod: "2024-05-10T09:23:34+10:00"
draft: true
toc: true
scrollSpy: true
---



## Part 1
## 24/10/23


![image1](img/log/image1.png)

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

## Part 2


