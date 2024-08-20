# M4L Sustain Pedal

This is a Max for Live device for Ableton Live. It allows you to play fast rhythmic patterns like that of a rhythm guitar and hold the sustain pedal throughout chord changes without slurring the two chords. Each note press will lift the pedal first and then sustain the new notes.

The purpose is to play chord changes much smoother and with no gaps from having to lift the pedal. It also allows for note repetitions with no gaps same as normal sustain would. To play legato lines smoothly, you would then play it more staccato to make sure there's no overlap between the notes.

The inspiration came from [Omnisphere](https://www.spectrasonics.net/products/omnisphere/)'s [Sustain Mode 2](https://support.spectrasonics.net/manual/Omnisphere2/25/en/topic/main-page12) which does the same thing, so it's essentially a M4L MIDI implementation of that.

In short, it's a performance MIDI device meant to make guitar-like chord changes easier to perform on the keyboard.

## Context

This is part of a couple devices I wrote in the summer of 2021 when I first learned Max. 3 years later, I thought "hey, maybe I should upload these." Someone might find them useful, and they're an interesting showcase on my GitHub profile.

So they all have some properties in common:

1. They're a little old and a little late.
2. They're my first foray into Max, so they might not be the most well-designed devices.
3. The commits are added after the devices are already finished based on previous versions of the devices instead of being atomic commits making incremental changes.

## Purpose

As mentioned, this is part of a semi-collection of performance MIDI devices with the common purpose being to make guitar-like playing easier to accomplish on the keyboard, specifically note repetition and chord changes with no gaps.

Guitarist "just" strum a string again. Keyboardists have to lift the key in order to press it down again. We can use a sustain pedal, but then when we need to change notes, the pedal timing needs to be super precise not to slur the notes or miss one. Additionally, and this might just be a me problem, it's incredibly hard to do fast repetitions on piano in the style of tremolo picking.

This present us with two projects.

1. Modified sustain pedal that lets us change notes without slurring.
2. Map key to repeat last played note so we can tremolo pick same note by alternating hands.

This project is the former.

For the latter project, see [M4L Note Repeat](https://github.com/MedicodiBiscotti/m4l-note-repeat).

I have one other M4L project that isn't really related to guitar playing. It lets you convert CC from one controller to another (e.g. modulation -> soft pedal), [M4L CC Converter](https://github.com/MedicodiBiscotti/m4l-cc-converter).

## Contents

This project contains multiple devices.

### Sustain

This is the most important one in terms of what it does. It performs the sustain pedal modification described above where you can perform chord changes while holding the pedal, and it won't slur the chords together. This allows you to perform fast rhythm patterns like that of rock rhythm guitar playing without needing crazy precise pedal lifts.

### Soft

A small utility that converts sustain pedal into soft pedal. Like the [M4L CC Converter](https://github.com/MedicodiBiscotti/m4l-cc-converter), this was made to simulate guitar palm muting. Holding the pedal down will activate muting and lifting will let the notes ring out.

### Pedals

An interface to switch between different pedal modes. It has 3 basic settings.

1. **Sustain 1**: This does essentially nothing, just passing on the sustain MIDI.
2. **Sustain 2**: The Sustain device from this project, based on Omnisphere's Sustain Mode 2.
3. **Soft**: The Soft device from this project.

Soft here has some extra settings to add leeway to the playing style.

**Next note** will prevent the pedal change from affecting the current note and instead wait until the next note plays. Ideally you'd want to press the pedal right before you play a note, but that will also briefly affect the sound of the current note. This prevents that.

**Only off** is to address an issue with **Next note**. I found I was often slightly late in releasing the pedal, which meant that the note wouldn't ring out how I wanted to until the next note was pressed. This settings allows the sound to immediately change with the **pedal lifts**. There hopefully shouldn't be that big of a difference having start of the muted sound. You should have lifted fast enough that the envelope didn't have a real chance to alter the sound.

In all honesty, having neither settings enabled might provide the smoothest, most intuitive playing feel, but they're there if you want them.
