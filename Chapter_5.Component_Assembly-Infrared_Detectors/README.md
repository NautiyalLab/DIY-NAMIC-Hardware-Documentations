# Component Assembly - Infrared Photo Interrupters 

#### What you will learn:

Basics of IR photo interrupters and how to test them
____

### Introduction
In any experiment, it doesn’t make sense both timewise and moneywise to just sit down and observe rodent behavior. If possible, we need to automate the process with machines. That’s what we will exactly do in this case – with sensors.

Infrared (IR) photo interrupters are handy sensors that can detect motion. Traditional Med Associates operant boxes utilize the photo interrupters to detect rodent nose pokes in receptacles. For the DNAMIC boxes, we will also be using the IR photo interrupters to detect rodent nose pokes.

***Note:*** I use the words *IR photointerrupters* and *IR detectors* interchangeably to reference the same object.

### What are IR detectors?

IR detectors are composed of two things: IR LED and a photo transistor. The basic working principle is that light and electricity signals are constantly getting converted through a certain medium. Once powered on, the IR LED of the photo interrupter will emit infrared light. The photo transistor, which is located across from the IR LED, will catch that light and convert it back to an electrical signal.

<p align="center">
    <img title = "figure1" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_1.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 1:</b> LEDs convert current to light and photo transistors convert light to current. Image Source: <a href="https://www.rohm.com/electronics-basics/photointerrupters/what-is-a-photointerrupter"> Link </a></i>
</p>

Therefore, if the photo transistor can receive light from the IR LED (absence of object in light path), it will convert light signals to HIGH electric signals. In contrast, if a photo transistor cannot receive light (presence of object in light path), then the photo transistor can’t convert any incoming signals so the electric signal would result in LOW.

<p align="center">
    <img title = "figure2" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_2.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 2:</b> Basic diagram of how light and electric signals get converted. Image Source: <a href="https://www.rohm.com/electronics-basics/photointerrupters/what-is-a-photointerrupter"> Link </a></i>
</p>

This is how photo interrupters detect state changes in motion. For example, if a mouse nose pokes and “breaks” the light path of the IR LED, photo transistors won’t be able to receive that light and will accordingly output LOW electric signal, notifying us that some activity is present.

### Photo Interrupter GP1A57HRJ00F

Our lab uses the photo interrupter [GP1A57HRJ00F](https://www.sparkfun.com/products/9299). This is mainly because other labs tend to use it, so feel free to explore other options for photo interrupters if you have the time.  

<p align="center">
    <img title = "figure3" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_3.png?raw=true" align=center width=300/><br><br>
    <b><i>Figure 3:</b> IR photo interrupter GP1A57HRJ00F </i>
</p>

Once you have the component, we have to power it up and connect it to our Arduino! To do that we will have to consult the [datasheet](https://www.sparkfun.com/datasheets/Components/GP1A57HRJ00F.pdf) for this particular photo interrupter since we don’t want to short the circuit prematurely. Below is an internal connection diagram from the official datasheet. It looks very confusing if you’re new to electronics. It certainly was for me when I started out! Thankfully I was able to find a “translated” version of the diagram (diagram 4). Note that diagram 3 and diagram 4 are top-down views of the photo interrupter. Also note that in diagram 4, the placement of the resistor doesn’t matter – it could as well be connected to ground and it will work just fine (as long as it’s a serial connection).

<p align="center">
    <img title = "figure4" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_4.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 4:</b> Internal connection diagram for the photo interrupter GP1A57HRJ00F. Note how the Infrared LED and the phototransistor are not connected electrically. Diagram Source: <a href="https://www.sparkfun.com/datasheets/Components/GP1A57HRJ00F.pdf"> Official Datasheet </a></i>
</p>

<p align="center">
    <img title = "figure5" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_5_1.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 5:</b> An easier “translated” version of the internal connection diagram in <b>Figure 4</b>. Image modified from: <a href="http://hmcbee.blogspot.com/2014/08/photogate-tutorial-part-2-basic.html?q=photogate"> Harvey Mudd Bee Lab </a></i>
</p>

### Breaking off the IR photo interrupter

Those of you who have keen eyes might have noticed from **Figure 4** already, but the IR LED and the photo transistor are not connected electrically! This means that we can break the IR in half and still get it to work as a photo interrupter as long as we align the light path of the IR LED to the photo transistor (Essentially the photo transistor needs nothing but infrared signals as input). This will effectively increase the working distance between the two components and allow us to be very flexible. As you might have already guessed, this is what we have exactly done in the lab.

<p align="center">
    <img title = "figure6" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_6_2.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 6:</b> IR photo interrupter broken into IR LED <b>(green)</b> and photo transistor <b>(yellow).</b>  </i>
</p>

IR LEDs are LEDs as well, so we also want to solder on current-limiting resistors to save the LEDs and the board. Just so that we are consistent with the regular LEDs, we will solder on the resistors to the shorter lead. Interestingly for GP1A57HRJ00F IR LED, the shorter lead happens to be the anode (opposite from regular LEDs). Note again that you may connect the resistor to the cathode as well and the current will still be limited. The important part is connecting the anode to PWR and cathode to GND when you are actually wiring the photo interrupters to the Arduino.

### Testing the IR LEDs

Human eyes have a limited wavelength detection spectrum. We can only detect wavelengths of light that are approximately 400 $nm$ – 700 $nm$. Therefore, it is literally impossible to “see” infrared light with the naked eye and to “see” if the IR LEDs are working or not.

<p align="center">
    <img title = "figure7" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_7.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 7:</b> Light spectrum. Infrared rays have longer wavelengths (700 $nm$ ~ 1 $mm$) than visible light.</i>
</p>

Luckily camera lenses are more sensitive to light than our eyes are. They can actually “see” (detect) infrared light. This allows us to “see” the infrared light through our camera lens. Test it out yourselves. Take only the IR LED part from the photo interrupter, wire it correctly to the Arduino (anode to GND, cathode to PWR) and power the Arduino with the USB. Turn on your phone camera and shine it over the IR LED. You’ll be able to see a purple glow like in **Figure 8**. This is actually pretty useful and important to us because we want to test the IR LEDs for any defects just like we tested the regular LEDs. If you don't see the purple glow under your phone camera even after powering up the Arduino, that means the IR LED has gone out.

Going slightly off topic, you can use this trick to "see" how remote controls communicate with TVs. More info [here](https://www.businessinsider.com/phone-camera-trick-can-see-infrared-light-tv-remote-2015-9).

<p align="center">
    <img title = "figure8" src="https://github.com/selincapan/DNAMIC-Hardware-Documentations/blob/finished-mardown-files/Chapter_5.Component_Assembly-Infrared_Detectors/imgs/Figure_8.png?raw=true" align=center width=350/><br><br>
    <b><i>Figure 8:</b> The purple glow of infrared light seen under a phone camera </i>
</p>

###### END OF CHAPTER
