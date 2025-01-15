---
title: Doof stick
description: An on-the-go infinity mirror
date: 2025-01-03 09:00 +1000
tags: [electronics, microcontrollers, python, AI, CAD, 3D printing]
image:
  path: /assets/img/posts/doofstick.jpg
  alt: Hold on tight to the ones you love
---
From April last year, I completed a two month Creative Technology residency at [MakerLabs](https://www.makerlabs.com/) in Vancouver.
In the first month, our cohort built a solid foundation in electronics, soldering, CAD, and 3D printing skills in weekly classes.
Then in the second month we worked on our own projects, with weekly drop in session with our mentor.

I went into the residency with the idea of bringing a doof stick to life - a fun stick you would take to a bush doof (outdoor music festival) to add art to the dance floor. It can also help your friends find their way back to you, as doofs are usually held in remote areas with little if any mobile coverage.

I took inspiration for this project from Ruiz Brothers' [NeoPixel Infinity Mirror Coaster](https://learn.adafruit.com/infinity-mirror-coaster) and [Lightsaber Prop-Maker RP2040](https://learn.adafruit.com/lightsaber-rp2040/)

## See it in action
{% include embed/youtube.html id='JsKdECeikFQ' %}

## Software
The [RP2040 microcontroller](https://www.adafruit.com/product/5768) I used in this project can run CircuitPython and Arduino code. 
I'm more familiar with Python than C++, so CircuitPython was easier for me to adopt.
I began with a proof of concept, using two potentiometers to adjust the brightness and colour of the embedded LED on the board:
{% include embed/youtube.html id='8pinbfl5puA' %}
Once I got a hang of it all, I collaborated with [Claude](https://claude.ai) to speed up my development, and had some really nice moments:

![A multimodal chat with Claude, with the LLM responding to a picture of the code it generated](/assets/img/posts/claude.png){: width="972" height="589" .w-75 .normal}

The code for this project is [available on GitHub.](https://github.com/nathanjnorris/doofstick/blob/main/code.py)

## CAD
After sketching out a few ideas on paper, I went straight into building out a model of the doof stick using [Autodesk Fusion](https://www.autodesk.com/products/fusion-360/personal).
I wanted to iterate by printing out sections of my design to ensure it would all integrate. After a few rounds of trial and error, I landed on the final design:

![CAD model of the doof stick](/assets/img/posts/fusion.png){: width="972" height="589" .w-90 .normal}

The case for this project has three main components:
  - Ring case for the LED strip and mirror discs
  - Brain box
  - Battery box

The ring and brain box are brought together using joints with tight tolerances and M2 screws. 
The brain and battery box are connected together using a wooden pole, with a cable transferring power wrapped around the pole.
   An editable Fusion file is [available on GitHub.](https://github.com/nathanjnorris/doofstick/raw/refs/heads/main/Fusion/doofstick.f3z)

## 3D printing
I was able to use a [Bambu Lab P1S](https://bambulab.com/en/p1?product=p1s) 3D printer at MakerLabs.
It was a reliable printer with great features like automatic bed leveling, and its fast prints helped my iterative process.
If you have [Bambu Studio](https://bambulab.com/en/download/studio) on your computer, you can explore the print files that are [available on GitHub](https://github.com/nathanjnorris/doofstick/tree/main/Bambu)

## Wiring 
This diagram was created using the software package [Fritzing](https://fritzing.org/download/). It provides a visual reference for wiring of the components:

![Wiriing diagram of the doof stick](/assets/img/posts/wiring.png){: width="972" height="589" .w-90 .normal}

![Microcontroller wired to components, and housed within the printed case](/assets/img/posts/wiring_irl.jpg){: width="972" height="589" .w-90 .normal}

An editable Fritzing file is [available on GitHub](https://github.com/nathanjnorris/doofstick/raw/refs/heads/main/Fritzing/wiring.fzz)

# Parts
Some parts, like wires and connectors, were available to me at MakerLabs so this isn't a complete list.
But it does contain the key components should you choose to make your own doof stick:

| Name                                       | Price |                                                                Link |
| :----------------------------------------- | :---- | ------------------------------------------------------------------: |
| RP2040 Prop-Maker Feather                  | US$20 |                   [Adafruit](https://www.adafruit.com/product/5768) |
| Mini Skinny NeoPixel RGB LED Strip 1m      | US$60 |                   [Adafruit](https://www.adafruit.com/product/2969) |
| RGB Metal Pushbutton, 16mm 6V Momentary    | US$11 |                   [Adafruit](https://www.adafruit.com/product/3350) |
| Breadboard-friendly SPDT Slide Switch      | US$1  |                    [Adafruit](https://www.adafruit.com/product/805) |
| Electret Microphone Amplifier - MAX4466    | US$7  |                   [Adafruit](https://www.adafruit.com/product/1063) |
| Panel Mount 10K potentiometer              | US$1  |                    [Adafruit](https://www.adafruit.com/product/562) |
| INIU Power Bank, 100W 25000mAh             | CA$72 |                       [Amazon](https://www.amazon.ca/dp/B08VDJP7WN) |
| Glow in The Dark PETG Filament Blue 1.75mm | CA$44 |                       [Amazon](https://www.amazon.ca/dp/B0BGX8Y53F) |
| 5V USB Type C PD to DC Power Cable         | CA$15 |                       [Amazon](https://www.amazon.ca/dp/B0B9G1KFL3) |
| USB C Extension Cable                      | CA$15 |                       [Amazon](https://www.amazon.ca/dp/B086YBP5VW) |
| Straight Slide Potentiometer B10K 75mm     | CA$15 |                       [Amazon](https://www.amazon.ca/dp/B09BZM6325) |
| #6x3/4 Flat Head Sheet Metal Screws        | CA$11 |                       [Amazon](https://www.amazon.ca/dp/B0C3ZMTCHK) |
| M2 Screws Bolts various sizes              | CA$7  |                       [Amazon](https://www.amazon.ca/dp/B0C774CP5G) |
| Silver One Way Mirror Film, 17.5" x 6.5ft  | CA$16 |                       [Amazon](https://www.amazon.ca/dp/B0B5D8RM3T) |
| Vinyl Squeegee Felt Edge                   | CA$8  |                       [Amazon](https://www.amazon.ca/dp/B01HLUUXYO) |
| PCB Board Prototype Kit                    | CA$11 |                       [Amazon](https://www.amazon.ca/dp/B0D31TX8RL) |
| JST Plug Set                               | CA$13 |                       [Amazon](https://www.amazon.ca/dp/B015Y6JOUG) |
| Threaded Insert Set                        | CA$27 |                       [Amazon](https://www.amazon.ca/dp/B0CQ4MKY3L) |
| 60-inch Hardwood Pole                      | CA$13 |                 [Home Depot](https://www.homedepot.com/p/100151067) |
| Transparent Acrylic Disc 300mm x 2mm, 2pcs | CA$28 | [AliExpress](https://www.aliexpress.com/item/1005006231672307.html) |


## Assembly
The steps I took somewhat follows the [Infinity Mirror Coaster](https://learn.adafruit.com/infinity-mirror-coaster/case-assembly) assembly instructions.
Once all the parts where printed, I still needed to drill out some holes and sand down edges so it could all fit. 
Before closing it all up, I made sure all of the electrical components were working as expected:
{% include embed/youtube.html id='_ksaKlXkdj4' %}
I definitely learned a few lessons about tolerances, and the age old adage of measure twice, cut once. 
I was really happy with how this all came together, albeit with a bit of elbow grease. 

## Party
At the end of July last year, some friends were visting my partner and I in Vancouver, and we went to [Shambhala Music Festival](https://www.shambhalamusicfestival.com/).
It was finally time to take the doof stick for a spin!

![Nathan at a music festival, shoving the doof stick into a friend's face](/assets/img/posts/party.jpg){: width="972" height="589" .w-90 .normal}

It was hit and a magnet for the electronics nerds out on the dancefloor, as plenty of people were chatting my ear off about microcontrollers and 3D printing.
It also worked really well - the battery lasted well over two nights before needing to be recharged, and the case held up drops and the wear and tear of the dance floor.
I'm looking forward to joining another makerspace soon and working on another project, and I'll be sure to post more about my next creator experience!
