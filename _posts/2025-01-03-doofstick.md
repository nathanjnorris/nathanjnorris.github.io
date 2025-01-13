---
title: Doofstick
description: An on-the-go infinity mirror
date: 2025-01-03 09:00 +1000
tags: [python, adafruit]
image:
  path: /assets/img/posts/doofstick.jpg
  alt: Hold on tight to the ones you love
---
In 2024 I completed a two month Creative Technology residency at [MakerLabs](https://www.makerlabs.com/) in Vancouver.

In the first month, our cohort built a solid foundation in electronics, soldering and 3D printing skills in weekly classes.
Then in the second month we worked on our own projects, with weekly drop in session with our mentor.

I went into the residency with the intention of building a doof stick - a fun stick you would take to a bush doof (outdoor music festival) to add art to the dance floor. It can also help your friends find their way back to you, as doofs are usually held in remote areas with little if any mobile coverage.

## See it in action
{% include embed/youtube.html id='JsKdECeikFQ' %}

## Parts

| Name                                       | Price |                                              Link |
| :----------------------------------------- | :---- | ------------------------------------------------: |
| RP2040 Prop-Maker Feather                  | US$20 | [Adafruit](https://www.adafruit.com/product/5768) |
| Mini Skinny NeoPixel RGB LED Strip 1m      | US$60 | [Adafruit](https://www.adafruit.com/product/2969) |
| RGB Metal Pushbutton, 16mm 6V Momentary    | US$11 | [Adafruit](https://www.adafruit.com/product/3350) |
| Breadboard-friendly SPDT Slide Switch      | US$1  |  [Adafruit](https://www.adafruit.com/product/805) |
| Electret Microphone Amplifier - MAX4466    | US$7  | [Adafruit](https://www.adafruit.com/product/1063) |
| Panel Mount 10K potentiometer              | US$1  |  [Adafruit](https://www.adafruit.com/product/562) |
| INIU Power Bank, 100W 25000mAh             | CA$72 |     [Amazon](https://www.amazon.ca/dp/B08VDJP7WN) |
| Glow in The Dark PETG Filament Blue 1.75mm | CA$44 |     [Amazon](https://www.amazon.ca/dp/B0BGX8Y53F) |
| 5V USB Type C PD to DC Power Cable         | CA$15 |     [Amazon](https://www.amazon.ca/dp/B0B9G1KFL3) |
| USB C Extension Cable                      | CA$15 |     [Amazon](https://www.amazon.ca/dp/B086YBP5VW) |
| Straight Slide Potentiometer B10K 75mm     | CA$15 |     [Amazon](https://www.amazon.ca/dp/B09BZM6325) |
| #6x3/4 Flat Head Sheet Metal Screws        | CA$11 |     [Amazon](https://www.amazon.ca/dp/B0C3ZMTCHK) |
| M2 Screws Bolts various sizes              | CA$7  |     [Amazon](https://www.amazon.ca/dp/B0C774CP5G) |
| Silver One Way Window Film, 17.5" x 6.5ft  | CA$16 |     [Amazon](https://www.amazon.ca/dp/B0B5D8RM3T) |
| Vinyl Squeegee Felt Edge                   | CA$8  |     [Amazon](https://www.amazon.ca/dp/B01HLUUXYO) |
| PCB Board Prototype Kit                    | CA$11 |     [Amazon](https://www.amazon.ca/dp/B0D31TX8RL) |
| JST Plug Set                               | CA$13 |     [Amazon](https://www.amazon.ca/dp/B015Y6JOUG) |
| Threaded Insert Set                        | CA$27 |     [Amazon](https://www.amazon.ca/dp/B0CQ4MKY3L) |

## Wiring 
This diagram was created using the software package [Fritzing](https://fritzing.org/download/). It provides a visual reference for wiring of the components: 
![Wiriing diagram](/assets/img/posts/wiring.png){: width="972" height="589" }
_Fritzing file is [available on GitHub](https://github.com/nathanjnorris/doofstick/raw/refs/heads/main/wiring.fzz)_

## Software
The microcontroller I used in this project can run CircuitPython and Arduino code. 
I'm more familiar with Python than C++, so CircuitPython was easier for me to adopt. 
I collaborated with [Claude](https://claude.ai) to speed up my development, and had some really nice moments:
![alt text](/assets/img/posts/claude.png){: width="972" height="589" .w-75 .normal}

The code for this project is [available on GitHub](https://github.com/nathanjnorris/doofstick/blob/main/code.py)

## 3D modelling and printing

## Assembly




