---
title: 1.3 Binary Coding and Decoding
categories: [FP DAW bilingual, Computer System]
tags: [] # TAG names should always be lowercase
---

## ✅ INT, Decimal, CHAR

1. Positive INT
2. Negetive INT: add sign flag
3. Decimal
4. Characters: ASCII, UTF-8
   - in ASCII, each char has 8 bits
   - 8bits = 1byte
   - 3bytes: Korean

## ✅ Image

### ☑️ Two types of pictures

#### 1️⃣ Raster

- divided into **pixels**, get pixelized when increase size
- `JPG`, `gig`, `png`
- HR: Horizontal Resolution: how many pixels in horizontal
- VR: Vertical Resolution: how many pixels in vertical
- Resolution = HR \* VR

#### ✔️ Color Depth in Raster

- **Color Depth**: how many bits you need for your image
- `1` or `8` or `24`
- black and white ➡️ need 2 combos, need `1 bit(2^1)` ➡️ color depth: 1
- gray-scaled ➡️ need 256 combos, need `8 bits(2^8)` ➡️ color depth: 8
- full-colored ➡️ every color is `R(0~255) + G(0~255) + B(0~255)` ➡️ each R, G, B need 8 bits ➡️ need `24 bits` ➡️ color depth: 24

  - pure red would be `255.0.0`
  - pure green would be `0.255.0`
  - black would be `0.0.0`
  - white would be `255.255.255`
  - as soon as there is one colored pixel, even if all pixels are black and white, color depth will be 24
  - if full color, each pixel will have 24bits, graphic card will write the bits

- color codes are stored in graphic cards, in the driver
- Red = `111111110000000000000000`
- I can use up to `2^24` colors, more or less 16000000(16 million)
  - `(2^4)*(2^10)*(2^10)` = more or less 16 _ 1000 _ 1000
- If a graphic card had 64bytes, it can have `2^64` colors

  - `(2^4)*(2^10)*(2^10)*(2^10)*(2^10)*(2^10)*(2^10)`

#### ✔️ Picture size in Raster

- Picture size = `HR * VR * D(color depth)`

```
Q: How many bits would a black and white picture have of 100 * 50?
- Picture size = HR * VR * D(color depth)
- 100 * 50 * 1 = 5000
```

```
Q: How many bits would a gray picture have of 100 50?
- Picture size = HR * VR * D(color depth)
- 100 *  50 * 8 = 40000
```

```
Q. If all the sound that my computer can make are 8, how many bits do my computer have?
- 3
- because 2^3 = 8
```

```
Q: How many bits would a full color picture have of 100 * 50?
- 100 * 50 * 24 = 120000
```

#### 2️⃣ Vector

- more professional, more efficient when picture is not so detailed
- `svg`

- do not use pixel, use `area by area`/ `zone by zone`
- call the color just once, then call the length/size/measurements of the area that has that color
- `red(255.0.0)* 10 meters + white(255.255.255) * 2 meters`
- the picture tends to be more compressed
- 👍🏻 more efficient
- 👍🏻 when the area is uniform, no big transition of color, use vector
- ⭐️ big areas of same color(like football field, all green)
- ↔️ image with many color changes, use Raster(like a christimas tree with lights)
- if I make the picture bigger, zoom in, then just have to change the length/size/measurements
- do not get pixelized

- 👎🏻 however, as measuring device is more expensive,
- vector is only used for professional purposes

## 📌 Main Computing Principle

- 0: 0.5v
- 1: 5v

- If you have `n bits` to store 0s and 1s, you can have total of `2^n` combinations
- 1 bit: 2 combinations `0, 1`
- 2 bits: 4 combinations `00, 01, 10, 11`

## ✅ Audio

- Audio is vibration, need air to transmit
- microphone has a small surface to capture vibration
- microphone transforms the vibration to binary code
- extension for audio is `.wav`
- when compressed/summarized `.mp3`
- if `la, la, la, la`, `.mp3` summarizes sound and save `la * 4`
- ⭐️ `.mp3` does not lose sound, but just summarized
- `.mp3` is very compressed when there are uniform, repetitive sounds in the track
- if many different sounds, `.mp3` will not be so efficient

#### ☑️ Sampling Frequency(Hertz)

- how many times per second the computer pays attention to the microphone/vibration
- sampling frequency ⬆️ better sound quality, capture more details of the sound wave ⬆️
- sampling frequency ⬇️ cannot capture all the details of the sound ⬇️
- if frequency is `1Hz`, then listening `1 time/sec`
- if frequency is `1KHz`, then listening `1000times/sec`
- if frequency is `1MHz`, then listening `1000000 million times/sec`
- if frequency is `1GHz`, then listening `1000000000 thousand million times/sec`
- ⭐️ If you capture a sound with a high sampling frequency, will get more details of the sound

#### ☑️ Amplitudes(bits)

- number of all the different sounds you want to capture
- in an orchestra, you want to capture more instruments, need higher amplitude
- higher amplitude ⬇️ more variety of sounds ⬇️

- Q: If orchestra used 16 different sounds, how many bits would we need?
- need 4 bits
- Amplitude = 4

- Q: If orchestra used 80 different sounds, how many bits would we need?
- need 7 bits (2^7 = 128)
- Amplitude = 7

#### ☑️ Time(seconds)

- how long the music lasts, measured in seconds
- more time ⬆️ can save longer song ⬆️

#### ☑️ Stereo

- full stereo: use two sequences of bits(2bits) per ear, duplicate the sound
- left and right ear listen to the whole song
- need to multiply formula by 2

- mono stereo: one sequence of bit, divide sound in two
- left ear: background music, right ear: singer voice

#### ✔️ Audio Size

- size: `Hertz * A * t`

```
Q: How many bits do you need for an orchestra for a 4 minute song, with 300 amplitude, sampled at 2GHz?
- size: Hertz * A * t
- 2*10^9 * 9 * (4*60)
 = 2000000000 * 9 * 240` bits
```

## ✅ Video

- sequence of pictures + sound
- `.avi`, `.mov`
- compressed into `.mp4`
- however, `.mp4` suffered from forking
- forking: people started using another form of video `.wmv`, not compatible with `.mp4`

#### ☑️ FPS, Frames per second

- how many images video shows per second
- fps ⬆️ better quality of video ⬆️

#### ☑️ Prediction in video

- in video use prediction
- as some pictures are important,
- but other pictures are evident, so not as important
- use picture I, P, B

#### ✔️ Types of picture in video

- **Picture type I**: Important
- independent pictures, important pictures
- mandatory to record them independently

- **Picture type P**: Predicted
- predicted pictures
- can predict them, as it is very similar to the previous picture

- **Picture type B**: Bidirectional
- Bidirectional
- extra movement to make video transition more natural
- pictures used to improve transitions
- make video look softer

#### ✔️ Video size

- `picture size * fps * t + Audio * 2(stereo)`
- `HR * VR * D * fps * t` + `Hertz * A * t * 2`
- ⭐️ audio is added

```
Q: How many bits a 5 minute video have that has resolution of 1920\*1090 full color at 1000fps with stereo sound of 100 amplitudes sampled at a frequency of 25MHz?
- {(1920*1920 * 24) * 1000 * (5*60)} + {( 25 * 10^6)  * 7 * (5*60) * 2 bits}
```

- ⭐️ only **color depth** and **amplitude** has to be converted into bits

## ✅ File

- all the bits are stored in a unit called `file`
- `file`: set of bits with information

- `metadata`: extra information about the file
- ⭐️ metadata is stored in the Operating system
- Timestamp: `created_date`, `last_modified_date`

  - `owner of the file`
  - `size of the file`;lkj
  - `extension of the file`
  - `permissions over the file`, read/write/execute permissions, what you can do with the file
  - `access control`, who can access the file

- Linux keeps metadata very far from data itself, 👍🏻 safe from haking
- However, Windows keep metadata close to the data itself, not very safe

## ✅

## ✅

## ✅

As an 𝙚𝙭𝙥𝙚𝙧𝙞𝙚𝙣𝙘𝙚𝙙 𝙅𝙖𝙫𝙖 𝘽𝙖𝙘𝙠𝙚𝙣𝙙 𝘿𝙚𝙫𝙚𝙡𝙤𝙥𝙚𝙧, this 𝘽𝙞𝙡𝙞𝙣𝙜𝙪𝙖𝙡 𝙒𝙚𝙗 𝘼𝙥𝙥𝙡𝙞𝙘𝙖𝙩𝙞𝙤𝙣 𝘿𝙚𝙫𝙚𝙡𝙤𝙥𝙢𝙚𝙣𝙩 𝙁𝙋 program strengthened my technical expertise to design, develop, and deploy complete web solutions, expanding my abilities for not only backend but also as a frontend developer. Through this study, I will gain advanced skills in both client-side and server-side web development, including languages such as 𝙅𝙖𝙫𝙖 𝟮𝟭, 𝙋𝙮𝙩𝙝𝙤𝙣, 𝙃𝙏𝙈𝙇, 𝘾𝙎𝙎, 𝙅𝙖𝙫𝙖𝙨𝙘𝙧𝙞𝙥𝙩 and 𝙍𝙚𝙖𝙘𝙩.

I will also enhance my understanding of 𝙍𝘿𝘽𝙎 𝙖𝙣𝙙 𝙎𝙌𝙇, 𝙘𝙤𝙢𝙥𝙪𝙩𝙚𝙧 𝙨𝙮𝙨𝙩𝙚𝙢𝙨, 𝙖𝙣𝙙 𝙥𝙧𝙤𝙛𝙚𝙨𝙨𝙞𝙤𝙣𝙖𝙡 𝙙𝙚𝙫𝙚𝙡𝙤𝙥𝙢𝙚𝙣𝙩 𝙚𝙣𝙫𝙞𝙧𝙤𝙣𝙢𝙚𝙣𝙩𝙨, building a stronger foundation for scalable, secure, and maintainable applications.

Additionally, the program emphasizes professional 𝙀𝙣𝙜𝙡𝙞𝙨𝙝 🇨🇮🇺🇸🇬🇧 𝙖𝙣𝙙 𝙎𝙥𝙖𝙣𝙞𝙨𝙝 🇪🇸 communication, preparing me to collaborate effectively in international and cross-functional development teams.
