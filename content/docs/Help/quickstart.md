---
weight: 520
title: "Quick Start"
description: "Getting up and running with the plugin"
icon: "help"
date: "2023-12-15T09:23:34+10:00"
lastmod: "2024-05-10T09:23:34+10:00"
draft: false
toc: true
scrollSpy: true
---

## Setting up your plugin
Once you've installed and activated your plugin, it's ready to set up and start being used. To get started, launch the standalone version of the plugin and click the settings button at the top-left corner of the plugin interface.

{{< alert context="info" text="The settings menu within the plugin interface is only visible in the standalone version. To set up audio settings for plugins within a DAW, open the audio settings section of your DAW's preferences menu. From there, you can select your audio interface, set the input and output channels, and adjust the sample rate and buffer size." />}}

Use the following settings to optimise your plugin's performance and get the best possible sound out of it.

### Audio output device
Set this to your audio interface. Depending on your interface, you may have to specify the output(s) to route your signal to depending on the interface that you have.

### Audio input device
This should also be set to your audio interface. Select the input you have plugged your instrument into.

{{< alert context="info" text="On Windows computers, you need to select “ASIO” as the audio device type for the plugin to function correctly." />}}

### Sample rate
Set it to 48000 Hz (unless you specifically require a different sample rate).

### Audio buffer size
Set it to 128 samples or lower. Increase the buffer size to 256 samples if you have an older computer.

## Installing plugins to your DAW
Artisian DSP comes with a standalone version, which means you don’t need a DAW to play. However, if you’re intending to record your playing, you will need to install your plugins to your DAW.

A complete installation will automatically install all the different plugin formats Artisan DSP comes in (VST, VST3).
You can also perform a ‘Custom install’, where you can install only the format(s) you need.

Normally, most DAWs will automatically scan for new plugins when they are launched. This means that after you install the plugin, it should be available to use inside your DAW without the need for any more steps.

If you can’t find the plugin in your DAW’s plugin list, you can manually rescan your plugin folder to locate it and make it available for use.

Once the plugin is found by your DAW, create a new project, insert an audio track, and insert the plugin into its effects chain. After doing so, you’re ready to start using the plugin within your DAW.

Note: Specific steps for installing and using plugins in a DAW will vary depending on which DAW you are using.

---

## Tips for using your plugin
Now that everything is set up, it's time to explore the different sections of your plugin. Use your mouse to control knobs and switches within the plugin’s user interface.

Click and drag upward to turn knobs clockwise, and drag downward to turn anticlockwise.

### Plugin modules
Familiarise yourself with the user interface, which is broken down into different sections accessible by buttons at the top of the plugin window.

#### 1. Noise Gate Section
The noise gate is used to eliminate unwanted noise and hum. It helps maintain a tight sound by cutting off the signal below the value specified by the threshold knob. If you have any hum or hiss in your signal, dial up the noise gate to reduce it.

The attack and release knobs alter the speed at which the gate opens and closes. Using the gate is beneficial for playing syncopated phrases that also need to utilise distortions.

{{< alert context="info" text="Please note that if the threshold is set too high, sustained notes may be prematurely cut off, resulting in shorter sustain. The threshold should be set to a level that cuts out the noise you want to eliminate, but doesn’t affect the tone or feel of your playing." />}}

#### 2. Compressor Section
The compressor helps to even out the dynamics of your guitar by reducing the volume of loud sounds and increasing the volume of softer sounds.

This results in a more consistent tone. It's particularly useful for tapping, ensuring that every note is clearly balanced levelwise.

#### 3. Overdrive Section
The overdrive pedal serves multiple purposes. It can be used to tighten up high-gain tones by cutting out the low frequencies with the tone knob, or used as the main source of distortion with the drive knob.

The latter use case serves as an excellent way to add clarity to modern metal tones.

#### 4. Amplifier Section
The amp sim provides the saturated distortion needed for metal genres, whilst also being able to be used lightly. Its various knobs allow for a wide range of tone-shaping options.

Use in conjunction with a low-drive, high-tone overdrive setting for a distorted, but clean tone.

#### 5. Reverb Section
Reverb adds a sense of space and depth to the sound by simulating the reflections of sound within a room, its size adjustable with the size knob.

When used properly, it creates a more natural sound, making the tone less dry. Reverb is versatile, spacing out clean tones, adding depth to leads, and thickening rhythms.

#### 6. Cabinet Section
The impulse response (IR) loader is used to simulate the response of different speaker cabinets and recording environments.

The most drastic transformation to tone is achieved by loading different IRs, which can emulate anything from a vintage 1x12" cab to a modern 4x12" stack, as well as different mic placements and recording rooms.

The plugin contains 13 IRs that you can select with the dropdown box. If you have your own IRs in the form of .wav files, you can load them by clicking the "Load IR" button and selecting them.


### Global features (top menu)
The global features menu has various features and settings that allow you to customise your sound.

----
![](img/help/toprow.png)

----

#### 1. Input
The input knob adjusts the level of the signal being fed into the plugin. If your guitar has a low output, you can increase the input to get a little more level to drive the amp. Alternatively, if your guitar is driving the amp too hard, dial the input down to get a cleaner tone.

#### 2. Module Selection
Click a button on the top row to switch the plugin’s focus to its corresponding effect.

#### 3. Presets
The plugin is built around a preset system that allows you to save the state of all of your adjusted parameters and store them within a unique file. When clicking the save button, a file prompt will open. Choose a name for the preset and click save. It will now be available to load via the dropdown menu.

Presets are also navigable via the arrow buttons adjacent to the dropdown box. Should you no longer wish to have a certain preset, you can delete the currently loaded preset with the delete button. If a preset contains a path to an IR file that doesn't exist, a "fix" prompt will appear, allowing you to select the proper path of the file. The new path will be added to file automatically, and loaded.

The plugin comes with some example presets that you can find prefixed with "EX". These allow you to jump straight into a fully-designed preset and get straight to the point.

#### 4. Output
The output will affect how much signal the plugin will feed out. Adjust when needed.


### Help features (bottom menu)

The help menu is accessible from the question mark icon found in the bottom-left corner of the plugin window.

----
![](img/help/helpmenu.png)

----

From this menu, you can view a brief explanation of how to use the plugin, as well as go to the source code and online help pages via the ‘external links’ buttons.

To close the help menu, click on the question mark icon again.


