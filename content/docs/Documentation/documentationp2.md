---
weight: 30
title: "Part 2"
description: "Major Project Documentation"
icon: "article"
date: 2023-11-24 12:00:00
date: "2024-05-10T09:23:34+10:00"
lastmod: "2024-05-10T09:23:34+10:00"
draft: false
toc: true
scrollSpy: true
---

----
# 3. **Implementation of Software Solutions**
----

## **Interface Design**
### **The Design of Individual Screens**
#### Identifying Data Required

During the design of the individual screens, it was vital that I identified the necessary data that was to be used, and how it would be stored and manipulated. I made sure that the plugin could receive and interpret various different types of data, including parameter changes, audio data, preset information and audio settings.

By setting up the plugin’s effect parameters within a parameter layout, all the data could be stored within an xml file on the user’s machine. This allowed me to store and recall parameter information for the purposes of preset management, as well as easily link the parameters to  sliders and buttons within each GUI component.


#### The Design of An Effective User Friendly Interface

During the development of the graphics user interface (GUI), I maintained a focus on the stylised, colour-coded recreation of reference pedals and amplifiers, to provide visually distinguishable points in the signal chain. This allows users to be able to immediately differentiate between each one by forming a colour association with the affected sound, allowing for a more intuitive experience. The use of different fonts for each effect’s text works to supplement this.

I upheld a standard of consistency throughout the GUI layout to keep the experience ergonomic. Rows of buttons, including the effects and preset selectors, are evenly spaced out from the centre, keeping the layout clean and symmetrical.

Pedals are positioned in the same centred position in each scene, sharing a similar shape and button / slider style, with an glowing on/off indicator for quick status identification. 

White space (black in this case) surrounds each pedal to direct the user’s focus to the centre through contrast. The amp and cab possess some differences in size and position, but still follow this principle.

I also included simplistic level meters to provide an active sense of responsiveness to the plugin, allowing users to visually see the audio data they input, and the difference in signal intensity by the time it is output.


#### Help Screens
To ensure an accessible experience for all users, I included various forms of help, explaining the functions of the different features of the plugin, and how to use them.
I made use of popup tooltips for quick on-the-spot explanations of the plugin’s sliders. Each window includes an identification of what the slider does, and how changing the value will affect the audio.

An example from the compressor:
![Tooltips](img/p2/helpscreens.png)


#### Level, Social, Ethical Issues

Considering the addressed legal, social and ethical issues identified in [Section 1](docs/documentation/documentationp1/#social--ethical-considerations), I took privacy into great consideration whilst designing the software solution. I made sure to protect my users’ data by reviewing the source code of any third-party submodules I had included, verifying that there was no malicious logic.

I also provided full closure about any data collection in my plugin to ensure trust in users. Additionally, because the project repository is public, any user is able to review the codebase and compile it themselves if they wish. A button on the help screen points to the source code on the github repository for this purpose.

![Help Screen](img/p2/helpscreenwall.png)

----

## **Program Development & Techniques**
### **Code Generation**

#### One Logical Task Per Subroutine
I approached code generation in a structured manner, where each element of the signal chain is treated as its own “block” within the processor. Within each block are 1-10 subroutines, each applying the result of one logical task to the audio samples.

Following this same mindset, I also structured the source code to include a unique header file for each scene’s GUI elements. By implementing these techniques, isolating the source of particular errors became much easier, and allowed for easier codebase navigability.

#### Debugging Output Statements
When errors arose, their corresponding messages were not always of great help. To solve these, I would make use of debug output statements to find out where exactly things were going wrong.

![](img/p2/debuggingoutput.png)

Juce has a built-in function, DBG(), for this purpose. When a parameter change seemingly had no effect on the audio, I would call DBG(variable) to verify that a certain variable was working as expected. If not, I would know where to start implementing fixes.

#### Elegance of the Solution
An important detail I took into consideration during development was the elegance of the solution. I aimed to create a clear, understandable and easy to navigate codebase, without any unnecessary complexity. In the beginning, this was definitely not the way it looked, but as I progressed through development and became more accustomed to the language and the framework, I was able to immensely improve the code by following best practices, and restructuring unnecessary chunks.

![](img/p2/neatcode.png)

#### Comments
To help ensure the understandability and navigability of the code, as well as improve the intrinsic documentation, I included many comments throughout the source files.

By using comments to explain or title lines or chunks of the code, I aimed to ensure that the functions of each segment are easy to understand, even for someone unfamiliar with the framework’s offerings.

![](img/p2/explancomments.png)

In addition, comments can serve as dividers, which I implemented in a structured manner throughout the source code. These serve as large visual identifiers that allow one to easily differentiate sections of code, even when scrolling through at a high speed.

![](img/p2/dividers.png)

#### Logical Variable Names
When creating variables, it is vital that they are named in a correct and understandable manner, to prevent confusion and improve the ease of internal configurability. For example, it would not be wise to name a variable comp, when it really relates to the amp.

Taking this into consideration, I made sure to name variables according to their intended functions, making use of the widely used formatting convention in software, camelcase.

An example of variable names from the help screen:

![](img/p2/helpscreennames.png)

#### The Use of Correct Control Structures
Within an audio plugin, audio is sent in via groups called blocks. To easily modify audio data with mathematical transformations, sample-by-sample processing is favourable.
To achieve this, I made use of an iterative control structure by using a for loop, in which samples move through a sequential chain of transformations. 

Each transformation is housed within its own conditional if statement, their state each governed by a corresponding user-toggleable boolean. Rather than acting like a traditional conditional control structure, they can be thought of as a series of modular processing chunks, that the audio is sequentially modulated by when each is activated.

In each transformation, the result is applied to the data within the buffer at the index of the iterable’s current value, until it reaches the maximum index of the buffer. After this, the entire process repeats for a new block of audio data, following a repetition control structure.


#### Taking Legal, Social and Ethical Issues into Account
Throughout the generation of my code, I ensured that it always upheld the terms stated within the solution’s privacy disclosure - that it doesn’t take personal data. To guarantee this, I made sure not to include any malicious logic within the code, in addition to reviewing the safety of the code of third-party submodules that I had included. 

Overall, by implementing these code generation practices, I was able to ensure that my codebase was easy to read, understand, and navigate. By employing techniques of isolated subroutines, debug statements, comments, logical variable names and correct control structures as well as taking privacy and the elegance of the solution into account, the overall quality of my code was able to be thoroughly improved.



----

### **Process of detecting and correcting errors**
Throughout the development of my software solution, I took various steps to detect and correct errors in the source code. By regularly utilising these processes, I could ensure that the reliability of the code and stability of the software solution existed to a high standard.

#### Syntax Checking
While creating my code, I took care in laying everything out while adhering to C++’s syntax rules. Fortunately, Xcode, the IDE I was using, provides syntax highlighting and error detection, which saved me lots of trouble from syntax errors by picking up on wrong indentation and typos.

#### Logic Checking
Logic errors appeared in great abundance throughout development. These are easy to notice, as they stop the build process, however finding their source often proved to be a challenge, as Xcode can’t always pinpoint exactly where they start.

To find where the logic errors emanate from, I followed a process in which I would check what had changed since the last git commit, and comment out / revert new lines before rebuilding the program. By following this methodical process, I was able to find the source of logic errors and adjust them according to their circumstances.

#### Peer Checking
Alone, one may not be able to find and detect all the irregularities that may be present in the source code. Because of this, a thorough review of the codebase with a fresh set of eyes may be warranted.

At various points throughout the development process, I would seek feedback from peers who were able to analyse the codebase for any potential sources of error. These reviews, from different sources, allowed me to unearth any oversights in my code, and appropriately address them.

#### Desk Checking
Prior to executing new code in the audio processor, I would perform desk checks - the manual process of tracking the code’s effects on variables and output line-by-line. By calculating that the expected behaviour was within reasonable bounds (important in digital signal processing), I would be able to then go on to verify the actual results. Doing this would allow me to detect irregularities in new algorithms that could pose potential dangers, before they happened. E.g. - loud pops in audio, which can destroy monitoring equipment and damage hearing.

#### Use of Expected Output
I used expected output as a comparative tool to confirm my code’s correctness. I did this by predefining the expected numerical results (from desk checks) as well as the expected audio output/transformation (e.g. comp will even out dynamics) for the comparison. Any variations that I found were able to be used to fix errors and inconsistencies.

#### Runtime Errors
Upon building the program with code adjustments, I kept an eye out for runtime errors like unexpected output, crashes, and behaviour that triggers Juce’s assert points. Through implementing exception handling techniques as well as taking screen recordings and logs of the console’s output, I could examine runtime errors after the short moments that they had occurred, allowing me to identify the underlying issues and formulate the appropriate fixes.


The utilisation of these error detection and correction methods enabled me to reduce the frequency of errors and raise the overall standard of my code. The employing of a combination of Syntax Checking, Logic Checking, Peer Checking, Desk Checking, Use of Expected Output, and Runtime Error Checking allowed me to greatly improve the reliability of my software solution.



----

### **The Use of Software Debugging Tools**
Throughout the development of the software, I regularly found myself face to face with a frequent amount of bugs and errors. To resolve such issues, I made use of a variety of software debugging tools.

#### Resetting Variable Contents
Sometimes, when testing a new algorithm with audio data and parameter sliders, the audio output differed greatly from what was expected. This would mean an error is present in said algorithm. 

To troubleshoot, I employed a debugging technique in which I would reset the values of certain variables to a default value. For audio data this would commonly be any constant within [0, 1] and for parameter values, this would normally be at the halfway point (50%). In doing this, I could watch over to see that the variables change according to an expected output, and be able to pinpoint the sources of any potential errors.

#### Program Traces
Throughout the codebase, I made a wide use of program traces - console output statements placed at important locations throughout the code. In the execution of the code, I was able to see the program’s execution flow through these statements within the console. This acted as a point of identification for any unexpected flow of operations, allowing me to find the source of errors.

#### Single Line Stepping
Single line stepping is a debugging process in which lines of code are individually executed, one after the other. Xcode provides a debugger in which I could utilise this method, which works upon a basis of breakpoints. By stopping at and stepping past these breakpoints, I was able to closely monitor changes in variables as well as observe the flow of execution, all in real time. Doing this allowed me to identify any logical errors as they affected the program during runtime.


By making use of these software debugging tools, I was able to identify numerous sources of error throughout my software solution, and be able to formulate the means to fix them. These methods: resetting variable contents, program traces and single line stepping, all helped to fix and improve the overall stability of the final version of the software solution.


----

## **Documentation**
### **User documentation**
Sometimes, the software solution itself does not provide a thorough enough explanation of how it is used and its functionality. Taking this into account, it is vital to include some forms of documentation in order to ensure a straightforward experience for all users. 

#### Installation Guide
Prior to the user’s installation of the software solution, an installation guide should be present, describing all the included modules to be installed. It should additionally specify, in particular, the minimum hardware requirements and versions of operating platforms.

The software solution includes a text file that provides this information. Because the solution is packaged within an installer, specific installation instructions are delegated to the installer.

#### User Manual
A user manual should describe the functionalities of the software solution, whilst being written in such a way that it is understandable by the target audience.
It should introduce and explain the executable aspects of the software, establish the importance of such aspects, and how to use them effectively. The content within the manual should be presented in a visually appealing, consistent style, with explanations in easy-to-understand language. 

The user manual for the software solution takes these points into consideration, and is located within the local files of the software as a PDF, allowing for quick and easy access, even without an internet connection.

#### Tutorials
Tutorials are a helpful addition to a software solution. A tutorial should describe in detail how a specific operation or task is performed, in a very specific and learning-oriented manner.

The software solution includes a video tutorial to teach the user how to choose the right audio input, enable effects, change their parameters, save presets, among other functions.

The software solution provides a tutorial in video format, taking these aspects into account. Video allows the user to hear an example of the expected audio usage, with visible responsiveness for reinforcement.

#### Online Help
Online help is a topic-oriented form of reference information designed to assist the user. During modern times, it has largely come to replace printed manuals and live, call-based customer support. This form of help may be deployed on a web server, accessible to users only with an internet connection, or able to be hosted locally on a user’s computer.

In the realm of software products, online help is commonly utilised to provide an easily updatable and interactive form of assistance for the users of a product. Dynamic online help sites also often make use of feedback, comment and forum systems to allow users to assist one another, as well as prompt the developers areas to be improved from the user’s point of view.


My software solution provides its documentation through its included files as well as internal help screens. Internal prompts within the software point to the website, which hosts video tutorials and online help. Local forms of user documentation bundled with the software - the installation guide and the user manual, can also be found on the website. In employing these forms of documentation, I can ensure that users are able to fill any gaps in knowledge and be able to utilise the software to its fullest extent if they so wish.



----

### **Technical Documentation**
The creation of technical documentation is a commonly found, yet essential practice in software development. Such documentation provides vital information about the inner workings of the software solution to collaborators, internal members, clients and end users. It ensures that everything can be understood and used efficiently.

#### Source Code Documentation
Within technical documentation, source code is the most important aspect, as it directly impacts the logic of the compiled program. Without access to the source code, any sources of errors found are effectively impossible to isolate and fix. As a result, the source code provides the most overall insight into the code’s functionality.

##### Clean Codebase
A clean codebase serves as a good source of documentation. By neatly structuring the code within each source file, it can be more easily understood and navigated by those accessing it.

##### Comments
Comments are lines of text prefixed with a symbol that act as a note, either to oneself, or for other developers. They are used to give background information or explain the thinking behind certain implementation decisions. 

Ideally, a comment should precede each different logical process, identifying what it is, and typically what it does. A common error developers make during the creation of comments is forming an exact restating of what the code does, logically. Comments should ideally convey the code’s intention in a short form, as an underlying baseline of clean code should ideally explain the logic by itself.

##### Intrinsic Documentation
Intrinsic documentation is a form of internal documentation that refers to the logical use of variable names, highlighting keywords, and anything else that affects the actual code. In properly applying intrinsic documentation, the ease of navigability of the codebase will be thoroughly improved.

##### White Space
White space refers to the strategic use of blank lines to structure source code. An effective use of white space will enable easier readability of code and facilitate a better understanding of the code’s logic.

#### Data Dictionary
A data dictionary serves as a centralised repository of information about data such as meaning, relationships to other data, origin, usage, and format. Maintaining a data dictionary ensures consistency in data management.

Click [here](/docs/documentation/documentationp1/#data-dictionary) to view my data dictionary.


Overall, by making use of technical documentation, I was able to maintain a smooth and understandable codebase. By maintaining a clean codebase, comments, intrinsic documentation, white space, and data dictionaries, the coherence of the entire program improved, and potential sources of error were prevented before they even emerged.


----

## **Communication**

### **Agenda for progress meeting**
#### Meeting 3

Date: 16/05/24

Time: 12:50pm

**Agenda**

- Show current plugin prototype with DI audio files
- Go through the website and current state of documentation

### **Minutes of progress meeting**
#### Meeting 3

Date: 16/05/24

Time: 12:50pm - 12:55pm

**Agenda**

- Show current plugin prototype with DI audio files ✓
- Go through the website and current state of documentation ✓

**Feedback**

On track

### **Log Book**

Click [here](docs/projectlog/#part-2) to go to my project log.

### **Updated and completed GANTT Chart**
[SDD Gantt Chart](https://docs.google.com/spreadsheets/d/17Ok0trQZ1qZ9iUKaFopEbsBKpJLXorLFDxOz9PAvpSk/edit?usp=sharing)


----

# 4. **Testing and Evaluation of Software Solutions**
## **Testing the Software Solution**
### **Comparing with the original design specifications**

My software solution includes most of the features from the original design specifications. Each effect contains a togglable switch that enables or bypasses their according audio algorithms.

#### Functionality Requirements
##### Input / output gain adjustment
My solution includes sliders that allow for an adjustment of +/- 15db.

There is no output mute switch however, which contrasts with the original design specifications.

##### Gate
The gate is implemented as originally planned, containing a threshold slider (-100dB to +6.0dB), and attack & release sliders (1ms to 100ms).

##### Compressor
The compressor varies slightly from the original specification of bundling multiple parameters into a single “compression” knob. To make the most out of the compressor’s internal DSP, attack & release, threshold ratio and output level sliders are included as independently adjustable parameters.

##### Overdrive
The overdrive satisfies the original design specifications, including level, tone and drive knobs. The tone knob adjusts the cutoff frequency of a high-pass filter within the range [20.f, 700.f], mimicking a tube-screamer style circuit.

##### Amplifier
The plugin contains an amplifier with adjustable sliders for pre gain, presence, bass EQ, mids EQ, treble EQ, post gain, and master volume. The amp contains a single channel that mimics the sound of a high-gain tube amplifier.

##### Reverb
The reverb contains adjustable sliders for room size, damping, width, and blend. It is positioned after the amplifier, but before the cabinet, to come closer to how a reverb pedal would be set up in an analog rig.

##### Impulse Response Loader
The solution contains an IR loader that is able to load .wav files via a user-selected file path or via the program’s internal binary data. The name of the currently selected preset is indicated within the GUI.

##### Preset System
The plugin contains a preset system that allows for saving and loading presets. Each preset contains data for all of the parameters, as well as the specified IR file path / name. 

In the case preset with a reference to a non-existent IR file, a fix preset prompt will appear on the IR loader screen, allowing the user to respecify the location of the according IR file.

The preset system also contains built-in presets that allow for a quick jump into a fully adjusted setup, without the need for any manual tinkering on the user’s part.

#### Needs of the User
##### High Sound Quality
Audio passed through the plugin when all effects are bypassed has little impact on the quality of the output. As a result, it can be said that the plugin maintains a high sound quality, aligning with the original design specifications.

##### Ease of Use
The plugin makes use of straightforward design elements throughout the graphics user interface, allowing for ease of use whilst minimising confusion.

##### Real-time Processing
Audio sent into the plugin is processed in real-time, with a low amount of latency, to allow for fluid responsiveness of output audio. This allows users to monitor themselves while playing in real time, without needing to worry about input lag.

##### Resource Efficiency
The program is optimised so as to make efficient use of system resources, allowing it to run smoothly on a wide range of computers, taking into account a large range of hardware.




### **Levels of Testing**
Software testing is an integral part of the software development process that helps to ensure that code quality is maintained to a high standard throughout the codebase of the solution. The process allows for the continuous improvement of the program by detecting sources of bugs and errors, bringing to light methods of fixing them.

#### Unit Testing
Unit testing is the process in which the smallest functional units of code are independently tested in isolation from the rest of the system. Unit tests verify the accuracy of these isolated blocks of application code, typically being that of a function, class, or method, and check to ensure that they run as expected according to the developer’s theoretical logic behind it, and meet the software’s functionality requirements.

In my process of unit testing, I made sure to isolate individual parts of my code, to accurately monitor for errors and bugs. When testing particular audio algorithms, I was able to do this by bypassing every other audio process, allowing for audio output altered by nothing but the currently tested algorithm. In the completion of my unit tests, I was able to verify that each unit worked smoothly, free of any errors, and that their functionality met the requirements.

#### Module Testing
Module testing is a process in which components of the solution are tested. Upon initiation, module testing’s purpose is to isolate a section of code and verify its functionality. From here, interfaces between modules are evaluated according to the expected output, to make sure that the system successfully works with itself internally.

There are numerous methods of module testing, the common being black-box testing, in which the test cases are designed based on the functionality of the code, without taking into consideration its internal structure.

Following the unit testing process, I proceeded to module testing, to test the program’s components and their ability to work correctly with each other. This is particularly vital in my plugin, as each and every part of the signal chain needs to work together to be able to form a coherent guitar tone. Module testing allowed me to verify the integrity of each module, and the stability in which they communicate with each other.

#### System Testing
System testing is a software testing method that evaluates the complete functionality and performance of a complete software solution. It aims to test whether or not the system meets the specified requirements and if it is suitable for delivery to the end users. 

In system testing, passed components from the module testing stage are taken as input, and treated as black boxes. Stages of system testing include:

- **Performance testing:** testing speed, scalability, stability and reliability
- **Load testing:** determines behaviour of the software under extreme load
- **Stress testing:**  tests the robustness of the solution under varying loads
- **Scalability testing:** checks the performance of the software in terms of its capacity to scale up or scale down the number of user requests

After unit and module testing, I tested the entire system to validate its complete functionality. This involved going through system testing stages such as performance, load, stress and scalability testing, ensuring that the program maintained its functionality requirements even as it reached its upper limits. After completing system testing, I was able to verify that the system worked, as a whole, as expected.


### **The Use of Live Test Data to Test the Solution**
When a solution reaches a point in which it is releasable, it must undergo numerous tests utilising real, “live”, test data to ensure its reliability, performance, and user-friendliness when faced with the scenarios it will regularly be interfacing with.

Using live test data allows for the possibility of extreme, conceivably possible scenarios to occur and be monitored during the testing stage, letting developers make changes accordingly, something that may be harder to replicate with synthetic test data.

#### Large File Sizes
Generally, pieces of software are designed with a particular size in mind for files that are input, while other sizes are not taken into consideration. A program that performs well whilst using the expected small file sizes may act much worse when faced with larger files. As a result, it is vital that files of larger sizes are tested. In doing so, inefficiencies in particular algorithms can be identified, isolated, and accordingly adjusted.

In my program, I tested this by selecting files of larger sizes within the few file choosers, including the IR loader. When the loader was faced with a larger file than expected (in both length and size), it handled it fine, due to its automatic cropping of the files.

#### Mix of File Types
Ideally, testing should check scenarios in which files of a variety of random types are entered into various points of the program. If a file of incorrect type is successfully entered, it may cause an unprepared system to break or crash. As a result, it is vital that systems are prepared for cases where unexpected types are input, and know how to act accordingly.

I tested my program by loading files of varying types into the IR loader. Because my system only accepts a .wav file as a valid result, it does not attempt to load files of other types. So, when testing for this, there was no unexpected output.

#### Response Times
Response time is a software quality metric that measures the time it takes for a system to respond to a user’s request, or internal change. A high response time is not a favourable outcome for a program, as it can lead to user annoyance and even abandonment of the software. Since elements like buttons should provide a near instantaneous response (<100 milliseconds), they generally require no visual feedback. Elements with a longer response time (>1 second), possess a noticeable delay, and should resultantly provide visual feedback, such as a spinner or progress bar. To ensure that response times are kept low for users, the program must be coded in an efficient manner, with performance in mind.

During my testing for response time, I found that all buttons and sliders respond instantaneously to user inputs (<100ms). When changing presets, there is a slight audio delay as all the parameters are updated to their new values. Any changes in input and output audio are represented visually through the meters on each side of the window, ensuring that there is always visual responsiveness when the audio side of the plugin is working correctly.

#### Volume Data (Load Testing)
Load testing determines how a software solution will behave during normal and peak load conditions, in addition to its breaking point (if it exists below the peak load). The goal in load testing is to identify bottlenecks to performance, make sure that the system can handle the expected peak loads, and verify that it upholds the functional requirements.

I used my plugin as an audio insert in a track in Reaper for load testing. I first tested a single instance with multiple audio recordings for input, going from simple sine waves to direct interface guitar recordings. I adjusted the parameters from minimal to maximum settings during this testing, and found moderate CPU usage increases, but no audio dropouts. 

When running multiple instances of the plugin in parallel, CPU usage jumped considerably, until I closed each GUI window. After, resource usage went back down to normal levels. This allowed me to identify the source of a performance bottleneck, within the GUI.

#### Interfaces Between Modules and Programs
An interface acts as a bridge between internal modules and components within a system. Interfaces commonly exist in the form of controls that are used as points of input to change values within the system and pass it on to other components as data. In practice, such controls are usually found within the system’s graphics user interface, which makes it the main way for users to interact with the program.

Testing the interfaces within my program was essential, as the main way for users to change parameters is via the GUI. Parameter information and values are stored within a parameter layout, which contains links that attach to GUI components like sliders and buttons which exist within each scene. Through this testing, I made sure that every linked component worked and affected the system as intended on every screen.
#### Comparison of Actual with Expected Results
Prior to the testing stage, expected results are created (e.g. in the form of desk checks) to act as a benchmark for the performance of the program. During the testing stage, the same test data should be entered into the program to ensure that the expected results match the actual results. Any discrepancies between the prior and current actual outputs allows for the identification of any solved or new problems.

When comparing, I found that there were no deviations with the actual and expected results, with everything running smoothly as per the expectations, ensuring that the program was ready to be packaged up for deployment.

----

## **Reporting on the testing process**
Documentation of tests undertaken are essential to the overall testing process. Any problems identified through test results will need to be addressed in order to prevent them from surfacing in the release. To effectively communicate such results for further fixes, the testing process must be adequately reported on and documented.

#### Test Requirements
For a test to be of any value, it must outline certain requirements. Testing undertaken will mirror qualities laid out in the earlier-defined functionality requirements.

#### Creating Test Data
Test data is the exact data that will be input and monitored throughout the testing process. Test data must be chosen and created according to the requirements of the test, to achieve an evaluatory output of value.

#### Test Plans
A test plan should identify what part of the software is being tested, and the overall approach that is taken in doing so.

#### Test Results
The test results will be an exact recording of the actual output of the test. These results will be kept, even if they fail to meet requirements, to assist in the creation of a solution to the problem, and confirm that the changes have in fact been implemented later on.

#### Recommendations
Should the results of a test differ from what is expected, a course of action to take to solve the problem should be recommended.

### **Testing Table**
| Test plan | Test data | Expected results | Test results | Recommendations of how to solve the problem |
|---|---|---|---|---|
| Run a simple sine wave through the plugin with no effects enabled and test for audio degradation. | Sine wave at a pitch of C3 from a virtual synth. | The audio output meter will be identical to that of the input, since no effects are enabled. <br>There should be no change in signal intensity when the plugin is bypassed. | Input and output meters sit at the same level. <br> Plugin Disabled: Audio level sits at +3dB. <br> Plugin Enabled: Audio remains at +3dB. No audible difference in the output signal. | None needed |
| Use the noise gate with DI guitar audio | DI Audio, <br>Enable only the noise gate and adjust parameters | The noise gate functions according to the current parameter values | After using the gate for an extended amount of time, the signal starts degrading | Change the noise gate algorithm to a working DSP process that does not rely on an averaging buffer |
| Use the Compressor | DI Audio, <br>Enable only the compressor and adjust parameters | The compressor functions according to the current parameter values | The compressor worked according to the selected parameters | None needed |
| Use the Overdrive | DI Audio, <br>Enable only the overdrive and adjust parameters | The overdrive functions according to the current parameter values | The overdrive worked according to the selected parameters | None needed |
| Use the Amplifier | DI Audio, <br>Enable only the amplifier and adjust parameters | The amplifier functions according to the current parameter values | The amplifier worked according to the selected parameters | None needed |
| Use the Reverb | DI Audio, <br>Enable only the reverb and adjust parameters | The reverb functions according to the current parameter values | The reverb worked according to the selected parameters | None needed |
| Use the IR Loader | DI Audio, <br>Enable only the IR loader and adjust parameters | The IR loader functions according to the current parameter values | The IR loader worked according to the selected parameters | None needed |
| Make use of the whole signal chain | DI Audio, <br>Enable every effect and adjust parameters | All parameters work in coordination with each other, and a usable guitar tone is made. | Parameters continued to work, and a usable guitar tone was made. | None needed |
| Test the View Code button | Click the View Code button | The link to the source code opens in the default browser | Worked as expected. | None required |
| Test the Online Help Button | Click the Online Help button | The link to the online help opens in the default browser | Worked as expected. | None needed |
| Test the input and output meters | Input DI audio, enable effects | Both meters reflect their proper states, and output level is greater than the input. | The output metre always remains at zero on the windows version. | Move the RMS calculation for the output metre to the end of the process block. |
| Use in a full mix (hard panned, distorted guitars) | Use the plugin on two guitar tracks simultaneously, with  no other plugins on their signal path | The guitars sit well in the mix, notes played sound cohesive | Worked as expected. | None needed. |

