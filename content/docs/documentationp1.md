---
weight: 1
title: "Documentation Part 1"
description: ""
icon: "article"
date: "2023-12-15T09:23:34+10:00"
lastmod: "2024-05-10T09:23:34+10:00"
draft: false
toc: true
scrollSpy: true
---
----
# **1. Defining And Understanding The Problem**
----
## **---Defining the problem---**

### **Identifying the problem**

#### Needs of the Client
When practising guitar or tracking within a digital audio workstation,
one will find themselves seeking a convenient signal chain solution that
enables them to instantly get a sound that works, diminishing the need
for costly external guitar hardware such as pedals, amplifiers, and
cabinets that require several sources of power, cables, careful setup,
and a recording solution, among other requirements. The solution will
benefit not only the beginner, with little knowledge of necessary gear,
but also the experienced player, allowing them to focus on the quality
of their playing without being hindered by a lack of equipment or case
of perfectionism.

As technology has evolved, so have the methods for signal processing,
and here the solution arises - digital signal processing.

Rather than contain these signal processors in physical form, such as in
guitar pedals, the function of their circuit can be replicated through
digital programming, and implemented within software - taking a live
input and giving a low-latency, altered output.

#### Functionality Requirements
When it comes to guitar DSP software, the user will have a multitude of
needs that must be met to ensure a smooth experience.

**Needs of the User**
-   High Sound Quality - Audio processing blocks must sound good enough for practice and demo recording use
-   Customizability: user-changeable parameters for customisable tone.
-   Ease of Use: Straightforward design elements to minimise confusion and is optimised for usability.
-   Real-time Processing: Audio is passed in and out with a relatively low amount of latency to ensure playability in real time.
-   Resource Efficiency: The program is optimised so as to make efficient use of system resources and leave computational power for other programs to run simultaneously.

Considering these needs, the solution will feature a fixed signal chain,
with toggleable blocks and editable parameters within each block.

For example, a block may be an overdrive booster, with its three
parameters adjusting the drive, tone and level applied to the signal as
it passes through.

Additionally, the solution will include preset creation and switching
based on these blocks and their parameters. The program will include
premade presets to act as templates.

**Functions the Software Solution will Include:**
-   Input gain adjustment
-   Gate
-   Compressor
-   Overdrive boost
-   Amplifier simulator
-   Post-amplifier reverb
-   Impulse response loader + included irs
-   Output level adjustment
-   Output mute switch
-   Preset selection and saving, built-in template presets

Input gain will be adjustable to add or remove from the original signal.

Gate will be adjustable to completely silence the signal if it is
quieter than the chosen level e.g. (-70db to +10db).

Compressor will be simplified, with attack and release controlled by a
single parameter, accompanied by a level parameter. The compression
ratio will also be adjustable.

The overdrive will mimic a tube-screamer style overdrive, with
parameters for amount of drive, amount of level, tone and on/bypass
status. The tone knob will introduce a low cut into the frequency
spectrum of the signal.

#### Compatibility Issues 

An important aspect of the solution to discuss is the hardware and
software prerequisites for it to be able to function as intended.

The program will be capable of running as a standalone app as well as be
hosted within a Digital Audio Workstation (DAW) as a VST plugin.

To use the program **standalone**, the user will require:

-   a Windows, MacOS or Linux PC
-   an audio interface (if connecting instrument) or
-   an audio file such as .wav or .mp3 containing a dry di signal to be loaded

To use the program **as a VST plugin**, the user will require:
-   a DAW that supports the loading of VST audio inserts

#### Performance Issues

As there will be multiple algorithms running simultaneously, they must
be optimised so as to not cause any performance issues that inhibit the
intended use of the program. However, even with such optimisation, users
equipped with weaker systems may face issues.

Because of this, during testing, a list of minimum and recommended
specifications will be created to advise potential users before they
attempt to use the program.

Even so, as blocks will have toggleable on/off parameters, the solution
will be able to be configured to bypass certain algorithms and only use
the desired ones, to focus system resources and increase performance.

**Performance to Consider:**
-   CPU usage by algorithms
-   Ram usage via quantity of algorithms run in series
-   GPU / Graphics utilisation via the interactable GUI
-   Storage space - keeping application a small as possible whilst retaining all necessary functionality

#### Boundaries of the Problem

**Language Support** - Users that do not speak english may have trouble
interpreting tooltips, ui and tutorials. To mitigate this the software
solution can include localisation for common languages other than
English.

**Lack of required hardware -** Users may lack hardware such as an audio
interface for audio input. Whilst this will prevent usage of the
software solution with an unbalanced line level instrument, other input
methods such as windows input and audio files can be used with extra
considerations during development.

**Operating System:** Users likely only use a single operating system,
so a build of the software to only one OS may inhibit its usage from
some users. As a result, the building of the solution to multiple
operating systems will need to be undertaken when the time comes in
development. It will also need to be tested on these other operating
systems.


### **Issues relevant to proposed solution**

#### Social & Ethical Considerations

**Accessibility**

One issue that may impact the solution is the accessibility of the
software for all users. Some users will need additional accessibility
preferences to be able to smoothly use the software solution without
trouble. Accessibility options that I can include may be:
-   Tooltips in UI
-   Screenreader for tooltips (text to speech)

**Privacy**

Another issue that impacts users is the strength of their privacy when
using the software solution. When a piece of software runs, it may have
access to all sorts of information. Malicious pieces of software contain
trackers that take this information, without the knowledge of the user.
To communicate and maintain full disclosure that there are no malicious
trackers embedded within the software, the source code will be available
to the user, allowing them to check the code and its dependencies before
deciding whether or not to install the program.

#### Consideration of Existing Software Products

**Similar Solutions Available Include:**
-   Amplitube
-   Bias Fx
-   Neural DSP Archetypes

Currently, there are several other software products available on the
market that serve a similar purpose. Each has its own unique set of
features and libraries, however they all share the same similar purpose.

Likewise, my software solution shares functional overlaps with these
existing products, and will possess its own unique characteristics to
differentiate itself from them. A large drawback of most of these other
software products is their high price.

Therefore, a low-cost/free alternative is needed in the area. This will
be a characteristic of the software solution.

#### Skills Required Throughout the Various Stages of This Project

The software solution will require knowledge of the C++ language as well
as the JUCE framework and its functions. Additionally, knowledge of the
mathematical functions used to digitally process the audio signal will
be required, as will be the methods of implementing them within the
software's code. Overall, with progressive research throughout the
creation of the software solution, the end result stands to be
attainable.

----
## **---Design Specifications---**

### **The Developer's Perspective**

#### Data Types

DSP software consists of many different components working together, and
as such need to store important data within variables.

**Integer:** Integers will be used throughout the solution to:
-   Count the number of samples in the audio buffer
-   Calculate current position within audio buffer
-   Receive midi data (Program & command changes)
-   Store midi data

**Boolean:** Booleans will be utilised throughout the program to allow
functions to be toggled. E.g:
-   Output mute on/off
-   Bypass effect on/off

**Float:** Floats will be used throughout the program to store the
values of specific parameters. Their decimal value between 0 and 1 will
act as a percentage. E.g:
-   Adjust gain levels
-   Adjust the various parameters of an effect (e.g. tone, drive, level, etc.)

**String:** Strings will be used to store information to display in the
GUI for the user. E.g:
-   Names of effects
-   Function of effects
-   Warnings
-   Tooltips

#### Data Structures

Data structures enable this important data to be stored within a set
layout so that it is able to be simply called upon in an easy format.

**Arrays:** Arrays are used to group data together and as such can be
used for a multitude of purposes in the software solution's context.
Arrays can be used to process and store audio samples as chunks of data.
Different types of arrays can be used for different purposes:

> ***Float Array:*** Float arrays can be used to store audio samples,
> allowing for manipulation of specific data points.
>
> ***Int Array:*** Integer arrays can be used to store MIDI data,
> allowing the program to receive program & control change messages and
> be able to interpret them to respond with a particular function.
>
> ***String Array:*** String arrays can be used to store parameter
> options in dropdown lists. These enable a set number of parameters to
> be interacted with by the user and be named accordingly.

#### Software Development Approach

The software solution will be developed using a mixture of the
prototyping and agile approaches. This is due to the progressive nature
of the program, the main aspects being different processors in series.
Due to this, the agile approach will allow for alterations in the
planned structure, provoked by various factors during the testing of
software prototypes in pursuit of quality. Overall, combining the agile
and prototyping approaches will allow for a flexible and quality
software solution.

### **The User's Perspective**

#### Interface Design

To ensure and maintain a high level of quality and polish, the interface
design will need to remain consistent across all of the software's
different scenes. The main layout of the interface will consist of a
graphical representation of the subject in the centre (currently
selected signal processor) with its parameters sitting ready to be
interacted with. Interactable icons will reside on the header, which
will change the currently selected audio processor display in the
centre.

#### Appropriate Messages & Icons

The program should prompt the user with an appropriate message and icon
when faced with errors and such.

In the context of an error in audio devices (no input / output device
selected), a user may be prompted with a message informing them of the
steps to fix the error, alongside a red GUI element / graphic.

#### Appropriate Icons

Icons will consist of a minimalistic, outline-based art style for
consistency across the program. The icons will be simple visual
representations of the software different signal processors, allowing
for quick and intuitive selection of processor scenes.

#### Relevant Data Formats For Display

The GUI design of the solution will need to format data for display in a
simple way in the interest of ease of use. Icons will be located in set
positions that do not change, and text will be easily readable,
contrasting with its background. Colour will also be used throughout to
easily and persistently convey functions such as errors, warnings, and
more.

#### Evaluate the Legal, Social & Ethical Issues

The software solution will directly impact musicians that use digital
signal processing, and are looking for more sonic options. Users are
always on the lookout for more options, and free ones typically appear
on their radars. Due to the zero-cost aspect of the software, users will
take the opportunity to try it, resulting in a user base of some
magnitude. Should the program adequately meet one's expectations, one
may choose to share it with others, resulting in new users that can
further chain the process, effectively promoting the software solution.
Overall, while it may not have a great impact on the general public, it
may moderately affect individuals in the music industry, in turn
allowing music demos and projects to be fulfilled and ultimately brought
to the ears of said general public.

#### Relevance to The User's Environment and Computer Configuration

Users may already have experience in similar DSP software solutions
targeted towards guitar processing, and the general structure of their
graphics user interfaces.

The solution will consist of a familiar and intuitive layout streamlined
for ease of use.

Since the nature of the program requires CPU resources to run the audio
processors, hardware optimisation and compatibility will be considered
during the solution's development.

Compatibility requirements that will be considered include operating
system, CPU, and graphics processing units.


## **---Modelling---**

### IPO Charts

| Input | Process | Output |
|---|---|---|
| - User’s direct interface input signal<br> - Adjust parameters of processors | Run through input block with selected parameters.<br> Mute signal if below selected gate threshold. <br> Run signal through compressor with selected parameters.<br> Run signal through drive with selected parameters.<br> Run signal through Amplifier Simulator with selected parameters.<br> Run signal through reverb with selected parameters.<br> Run signal through impulse response loader with selected parameters.<br> Run signal through output block with selected parameters. | Effected audio output<br> Display adjusted parameters for each block in GUI |


| Input | Process | Output |
|---|---|---|
| - Save Current Preset<br>- Input preset name | Get all current parameter states and store in an array<br>Ask for preset name<br>Save array as a file within the program’s presets folder<br>Add new preset to list of selectable presets within the software’s GUI | Prompt for preset name<br>Display saved preset as current preset<br>Show new preset in preset selection list |

### Context Diagram
![Context Diagram](img/Charts/context.png)

### Data Flow Diagram
![Data Flow Diagram](img/Charts/dfd.png)

### Structure Chart
![Structure Chart](img/Charts/structurechart-fullsize.png)

### System Flowchart
![System Flowchart](img/Charts/sysflow.png)

### Data Dictionary

| **Data Item** | **Data Type** | **Description** | **Unit** | **Example** |
|---|---|---|---|---|
| sample_rate | integer | Represents how many audio samples are sent per second. | Kilohertz (kHz) | 48000 |
| windowsize | integer | The size of a window of audio to be analysed. | No. of samples | 512 |
| threshold | float | The noise level at which a consequence occurs, varies based on the algorithm. | Decibels (dB) | -12.0 |
| attack_time | float | The time that the processor will take to apply the effect once the threshold is crossed. | Seconds | 0.025 |
| release_time | float | The time that the processor will take to remove the effect once the threshold is crossed. | Seconds | 0.10 |
| hopsize | integer | The increment between adjacent analysis frames within a signal. | No. of samples | 128 |
| gainfactor | float | The number multiplied by the input signal to increase input gain | Decibels (dB) | 3.0 |


### Storyboard
![Noise Gate](img/modelling/noisegate.png)

![comp](img/modelling/comp.png)

![od](img/modelling/overdrive.png)

![amp](img/modelling/amp.png)

![verb](img/modelling/reverb.png)

![cab](img/modelling/cab.png)

![presets](img/modelling/presets.png)


----

## **---Communication---**

### Scheduling -- GANTT chart

Click to open gantt chart.

[Software Gantt Chart](https://docs.google.com/spreadsheets/d/17Ok0trQZ1qZ9iUKaFopEbsBKpJLXorLFDxOz9PAvpSk/edit?usp=sharing)

### Agenda for progress meeting

#### Meeting 1

Date: 7/11/23

Time: 11:30am

**Agenda**

-   Explain project

-   Go through current documentation

-   Go through gantt chart

#### Meeting 2

Date: 29/02/24

Time: 1:00pm

**Agenda**

-   Show current state of project

-   Go through new progress logs

-   Go through todos

### Minutes of progress meeting

#### Meeting 1

Date: 7/11/23

Time: 11:30am - 11:40am

**Agenda**

-   Explain project: ✓

-   Go through current documentation: ✓

-   Go through gantt chart: ✓

**Feedback**

-   On track

#### Meeting 2

Date: 29/02/24

Time: 12:47pm - 12:51pm

**Agenda**

-   Show current state of project: ✓

-   Go through new progress logs: ✓

-   Go through todos: ✓

**Feedback**

-   On track

### Development log
[Click here](projectlog)


# **2. Planning and Design of Software Solutions**

## **---Algorithms---**

### Noise Gate

***sample_rate*** - the sample rate selected by the user. This
represents how many audio samples are sent per second. 48,000kHz or
44,100kHz are standard options.

***windowsize*** - the size of a window of audio to be analysed,
measured in amount of audio samples. e.g. the window size might range
from 32-512 samples

**Parameters:**

***Threshold*** - The noise level (dB) at which the gate will let sound
freely through. Audio below this level will be muted.

***Release Time (release_time)*** - Sets the time (in seconds) that it
will take to mute the signal once it falls behind the threshold.

***Attack Time (attack_time)*** - Sets the time (in seconds) that it
will take to open the gate once the signal passes the threshold.
```
BEGIN NoiseGate
WHILE True:
  sample = read_input_sample()
  amplitude = get_avg_amplitude(sample, windowsize)
  
  IF attack_time > 0 and gate_state < 1.0:
    attack_factor = math.exp(-1.0 / (attack_time * sample_rate))
    gate_state = gate_state * attack_factor + (1 - attack_factor)
  ENDIF

  IF amplitude > threshold:
    gate_state = 1.0
  ELSE:
    IF release_time > 0:
      release_factor = math.exp(-1.0 / (release_time * sample_rate))
      gate_state = gate_state * release_factor
    ELSE:
      gate_state = 0.0
    ENDIF
  ENDIF

  output_sample = output_sample * gate_state
  write_output_sample(output_sample)
ENDWHILE
END NoiseGate
```

![Noise Gate Flowchart](img/modelling/ngflowchart.png)


### Compressor

***knob_position*** - determines the intensity of the compression out of
three options from least compressed to most compressed.

***threshold*** - dB that compression will begin at.

***ratio*** - the amount that a signal is altered. E.g. a ratio of 2:1
causes a signal exceeding threshold by 2 dB to be attenuated down by 1dB.

***attack_time*** - time taken (in seconds) to apply compression.
 
***release_time*** - time taken (in seconds) to bypass compression.

```
BEGIN Compressor

WHILE True:
  sample = read_input_sample()

  IF knob_position == 1:
    threshold = -30.0
    ratio = 2.0
    gain = 1.0
    attack_time = 0.01
    release_time = 0.05
  ELIF knob_position == 2:
    threshold = -20.0
    ratio = 4.0
    gain = 0.8
    attack_time = 0.005
    release_time = 0.025
  ELIF knob_position == 3:
    threshold = -12.0
    ratio = 8.0
    gain = 0.5
    attack_time = 0.002
    release_time = 0.01
  ENDIF

  amplitude = get_avg_amplitude(sample, windowsize)
  IF amplitude > threshold:
    gain_reduction = 1.0 - (1.0 / ratio)
    gain_reduction = gain_reduction * ((amplitude - threshold) / (10.0 * gain_reduction))
    gain = gain * (1.0 - gain_reduction)
    output_sample = sample * gain
  ELSE:
    output_sample = sample
  ENDIF

  IF attack_time > 0:
    attack_factor = math.exp(-1.0 / (attack_time * sample_rate))
  ELSE:
    attack_factor = 1.0
  ENDIF

  IF release_time > 0:
    release_factor = math.exp(-1.0 / (release_time * sample_rate))
  ELSE:
    release_factor = 0.0
  ENDIF

  gate_state = gate_state * release_factor + (1 - release_factor) *sample

  IF gate_state < 1.0:
    gate_state = gate_state * attack_factor + (1 - attack_factor)
  ENDIF

  output_sample = output_sample * gate_state

  write_output_sample(output_sample)

ENDWHILE
END Compressor
```

### Tube Screamer Overdrive

**Parameters:**

**Level** - audio level leaving the pedal.

**Drive** - gain applied to the signal.

**Tone** - intensity of filter applied to signal.

```
BEGIN Overdrive
toneCenter = 0.5
i = 0
WHILE True:
  sample = read_input_sample()
  clippingThreshold = 0.707 * drive
  toneCap = 0.1 * (1 + drive)
  preGain = 1.0 * (1 + drive)
  preGainSample = sample * preGain
  clippedSample = tanh(preGainSample * clippingThreshold)
  IF i = 0:
    previousClippedSample = clippedSample
    i = 1
  ENDIF

  toneFilteredSample = clippedSample + toneCap * (previousClippedSample - toneCenter * clippedSample)
  previousClippedSample = clippedSample

  outputSample = toneFilteredSample * level
  outputSample = max(min(outputSample, 1.0), -1.0)
  write_output_sample(outputSample)
ENDWHILE
END Overdrive
```

### Amplifier

**Parameters:**

**Gain** - Alters the gain of the incoming signal

**Bass** - Alters the bass frequencies of the signal

**Mids** - Alters the middle frequencies of the signal

**Treble** - Alters the high frequencies of the signal

**Master** - Adjustment of the output signal

```
BEGIN Amplifier

preGain = 1.0

WHILE True:
  sample = read_input_sample()

  gainSample = sample * gain
  bassSample = BassShelfFilter(gainSample, bassGain)
  midSample = MidPeakingFilter(bassSample, midGain)
  trebleSample = TrebleShelfFilter(midSample, trebleGain)
  masterOutput = trebleSample * master

  outputSample = max(min(outputSample, 1.0), -1.0)
  write_output_sample(outputSample)
ENDWHILE
END Amplifier
```

### Reverb

**Parameters:**

**Level** - The loudness of the effected signal.

**Blend** - The balance between the effected and original signal to be
output.

**Time** - How long the reverb should take to fully decay.

```
BEGIN Reverb

WHILE True:
  sample = read_input_sample()

  wetGain = level * (1.0 - blend)
  bufferIndex = (bufferIndex + 1) % bufferSize
  reverbBuffer[bufferIndex] = sample

  FOR i in range(bufferSize):
    decayFactor = 1.0 - time
    reverbBuffer[i] *= decayFactor
    outputSample += wetGain * reverbBuffer[i]
  ENDFOR

  outputSample = (1.0 - blend) * sample + outputSample
  write_output_sample(outputSample)
ENDWHILE
END Reverb
```

### Impulse Response Loader

**selectedIR** - the IR file that the user has selected from a specified
directory

```
BEGIN IRLoader
WHILE True:
  sample = read_input_sample()
  output_sample = convolute(selectedIR, sample)
  write_output_sample(output_sample)
ENDWHILE
END IRLoader
```





----
## Selection of Programming Language

The most appropriate programming language for this software solution is
C++. C++ is a compiled language, which helps the application's
performance to focus on its functions, rather than interpretation. This
is due to the fact that upon building, C++ is converted into machine
code that the processor can execute.

Whilst interpreted languages such as Python can also be used for digital
signal processing, they take much more time to execute due to the fact
that they must interpret the code sequentially whenever it is executed.
For this reason, using C++ is optimal as speed is a necessity in the
digital processing of audio.

C++ also allows the use of the JUCE framework, an open-source
cross-platform C++ application framework. As it is one of the most
widely used frameworks for audio applications and plugins, there is a
great amount of documentation and resources available to support
development.

A major aspect is that it is cross-platform, allowing a single codebase
to compile to native applications and plugins consistently on Windows,
macOS, and Linux. It also contains tools to build and customise the
graphics user interface of the application.

Overall, this selection allows for a consistent user interface and
experience in the implementation of the solution across all desktop
platforms, whilst also optimising the usage of system resources to
better run digital processing algorithms.
