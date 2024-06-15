# Music Machine by Jacob Simmons
<h1>A device that allows for music notes to be selected and stored in a shift register to be played manually or as a pretimed sequence using the mono audio output jack on the Nexys4 DDR board. Coded in Verilog.</h1>

<p>The device is able to store up to 16 notes to be played within the range of one octave - from
low to high F. The first eight switches on the board are used to select the desired note that
will be stored in the shift register. The color of the left RGB LED is used to show the
currently selected note, as shown in the table below.</p>

|Switch|RGB Color|Corresponding Note|
|---|---|---|
| 0 | Red | Low F |
| 1 | Orange | G |
| 2 | Yellow | A |
| 3 | Green | B |
| 4 | Blue | C |
| 5 | Purple | D |
| 6 | Pink | E |
| 7 | Red | High F |

<p>Additionally, turning on the rightmost switch (switch 15) toggles whether the selected note
becomes flat. The right RGB LED becomes green if the note is chosen to be flat.</p>
<p>After selecting the desired note, the center button can be pressed to add the note’s frequency
value to the shift register, as illustrated by the 16 LEDs at the bottom of the board. These LEDs
show how many notes have been added to the shift register. </p>
<p>To clear the register, the next-to-last switch (switch 14) is used. </p>
<p>When all the desired notes are added to the register, the up button can be pressed to play
all the notes with a half-second on/off duration between the notes. Releasing the button will stop playing the note
and the register will automatically shift to the next note in the sequence, starting over when the
last note has been played.</p>
<p>The two color LEDs have three IO pins each in the constraints file, corresponding to the red,
green, and blue (RGB) values that can be displayed by these LEDs. Driving these inputs with
PWM signals allows for the necessary variety of colors to be displayed, with a higher duty cycle
corresponding to the intensity of the red, green, or blue light from each LED.</p>
<p>The mono audio output jack on the board has two IO pins that can be assigned values in the
constraints file, one named AUD_PWM for a PWM signal carrying the desired audio data, and
the other a simple on/off signal named AUD_SD as an enable value. AUD_SD can also be
driven with a PWM signal to specify output volume by varying its duty cycle.</p>
<p>The Nexys4 DDR board contains a Sallen-Key Butterworth low pass 4th order filter which allows
for the PWM signal passed to the AUD_PWM IO pin to be effectively integrated into a
sinusoidal wave, provided that the duty cycle of the given PWM wave varies from a maximum to
a minimum value and back over the course of one period. Optimally, this period should be
modeled to correspond to the desired frequency of the audible sine wave.</p>
<p>As for the audio wave, a PWM signal whose duty cycle varies from 10% to 100% and back to
10% over one period corresponding to the desired frequency of the resulting sine wave is
generated.</p>
<p>A ROM file is used in the code to specify the frequency values of the sinusoidal audio output to be created. These fourteen 
frequency values are input in binary and incorporate the frequencies in mHz of low to high F centered around middle C, as on a piano. The file containing these frequencies is labeled
ROM_DATA.mem and is included in the repository.</p>
<p>Finally, the master constraints file for the Nexys4 DDR board is also included in the repository. Due to version and OS differences, the outputs/inputs of the Verilog code must be assigned manually in this file.</p>
