```Smalltalk
"Start EcoPhausto, you should hear all its sound playing together".
EcoPhausto start.

"create a new instance of EcoPhausto"
ep := EcoPhausto new.

"you can see all the EcoPhausto instruments in a Transcript"
EcoPhausto listAllInstruments. 

"play the Performance"
ep playFor: 128 bars. 
"it is empty now but we will add a sequencer to it in the following lines"
"Sequencers can be created by sending the asSeq message to an array of 1 and 0"
 #(1 0 0 1 0 0 0 0) asSeq to: #kick.
"or by sending the asRhythm message to a valid rhythm preceded by an hash (that's a Pharo symbol btw)"
#rumba asRhythm to: #conga.
"CMD+i (Mac) or CTRL+I (Win/Linux) on the next line to open an Inspector on the list of available rhythm"
Rhythm list.
"but if you want to type less (losing iconicity), just send the message to: to a valid rhythm"
#plena to: #conga.
"or sending the hexBeat message to a string containing only hexadecimal characters"
'020F' hexBeat to: #snare.
"sending the index: message to a Sequence with a string of integers as an argument changes the samples indexes(if playing a TpSampler), which by default are all 0s" 
16 quavers index: '0 1 2 3 ' to: #bleep.
"sequencers can be joined with a comma - binary operator for joining collections in Pharo"
16 quavers , 16 semiquavers to: #oh.
"we can mute sequencers"
ep mute: #(#kick #snare #bleep).
"and unmute them"
ep unmute: #(#kick #snare).
"you can create randomTrigs - and then cascade a string to change the level of the sound"
16 randomTrigs to: #ch; level: '0.8 0.4 0.3'.
"or randomTrigs with a probability"
(16 randomTrigsWithProbability: 65) to: #ch.
"or you can create Sequencers by sending the asDirtNotes message to a string"
'-/8 , 38 , 56*2 , -/4 , 41 , 66' asDirtNotes to: #acid; envMod: '0.8 0.2 0.3'.
"or sending asDirtIndex if you want to play a different sample in the folder (if more than one available)"
"sending the notes: message to a Sequence with a string of MIDI notes as an argument changes the notes of the Sequencer, which by default are all 60 (C3)."
'1 , -/16 . 7 , -/9 , 12 , -/12, 18' asDirtIndex notes: '38 45 78 62  81' to: #speakspell.
"Euclidean rhythms can be created by sending the euclidean message to an array, where the first element is the number of steps and the second is the number of pulses."

#(5 16) euclidean index: ' 1 3 5 2'; to:  #bongo.
"Trigs inside a Sequencer can be offset forward"
#(5 16) euclidean offset: 1; to: #cowbell.
"or backwards"


"we can arpeggiate the notes of a Sequencer"
#cumbiaClave asRhythm arpeggiate: '12-sus4 0-min'; to: #psg; level: '0.4'.
"or we can random walk through a scale over an octave span from a root note"
64 randomTrigs notes: (32 randomWalksOn: Scale sakura octaves: 2 root: 48) to: #psg.

"sequencers can be soloed"
ep solo: #(#psg #cowbell).
"and unsoloed - that takes the performance back to the status between the solo"
ep unsolo: #(#psg #cowbell).

"change the bpm"
ep bpm: 96.
"stop the performance"
ep stop.
```
