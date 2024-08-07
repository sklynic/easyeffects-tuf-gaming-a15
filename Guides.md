# Guides

## Preparation

Before we start, you needs the Dolby Atmos driver `Dolby Atmos CMedia driver for ROG_TUF`, which you can get either from ASUS website (newest version) or `C:\eSupport\eDriver\Software\Win32App\Dolby\Dolby Atmos CMedia driver for ROG_TUF` folder (factory version). (ThSere should have no difference between them, though.)

## Steps

### Find your audio card's device id

#### Linux

Run command below:

`lsusb | grep Audio`

For example, on my device (FA507RM) the output is:

`Bus 005 Device 002: ID 0b05:6208 ASUSTek Computer, Inc. C-Media(R) Audio`

`0b05:6208` is the device id we needs for next steps.

#### Windows

You can find it in Device Manager. Check on internet for steps.

### Find the right tuning xml

Under the driver folder, find a xml file named `USB_VID_xxxx_PID_xxxx.xml`.

For my device it's `USB_VID_0B05_PID_6208.xml`.

### Extract and process tuning data

Use your favorite text editor to open it. In the xml file you can find different presets, which you may already familiar in Dolby Access.

Let's take the "Music" preset as example. You can also do these steps on other presets, such as Dynamic, Movie, Game, Voice and others.

Find section `<profile type="music">`, then jump to `<tuning-vlldp>`, then `<audio-optimizer-bands>`. For example, you can find:

` <ch_00 value="-46,82,138,186,150,-30,-74,-54,-51,8,69,118,48,-22,48,48,48,155,150,150"/>`

There are 20 numbers here, that indicates it's a 20 band equalizer.

Let's find the corresponding frequency. Find `band_20_freq` in the file. The result is:

` <band_20_freq fs_44100="43,129,215,301,431,603,775,947,1206,1550,2067,2756,3618,4651,5685,7063,8958,11025,13781,18777" fs_48000="47,141,234,328,469,656,844,1031,1313,1688,2250,3000,3750,4688,5813,7125,9000,11250,13875,19688"/>`

We will need the `fs_48000` series.

Now, open a office app and create a `.csv` file. In the first row write down the frequency, in the second row write down the tuning result (all the number should be multiply with 0.1).

The result should looks like this:

| 47    | -4.6 |
|-------|------|
| 141   | 8.2  |
| 234   | 13.8 |
| 328   | 18.6 |
| 469   | 15   |
| 656   | -3   |
| 844   | -7.4 |
| 1031  | -5.4 |
| 1313  | -5.1 |
| 1688  | 0.8  |
| 2250  | 6.9  |
| 3000  | 11.8 |
| 3750  | 4.8  |
| 4688  | -2.2 |
| 5813  | 4.8  |
| 7125  | 4.8  |
| 9000  | 4.8  |
| 11250 | 15.5 |
| 13875 | 15   |
| 19688 | 15   |

### Generate the presets

Open [AutoEq](https://autoeq.app) site. In the headphone selection, choose "Flat".

Then, chick the "Show advanced" button on left panel. In the "Target" section, also choose "Flat". 

Find "Sound signature" section, and click the second button "Open CSV file". Select the `.csv` file we just created.

Finally, in the right panel choose "EasyEffects". Now you have a preset that can be used in EasyEffects (or equalizerAPO, it's the same). Enjoy!