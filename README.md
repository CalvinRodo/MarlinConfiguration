# MarlinConfiguration

## Description

This repo contains the Marlin Configuration that I'm using for my Ender 3v2. 

My build contains the following: 

- BLTouch Clone (3D Touch)
- BTT SKR Mini E3 V3.0
- BTT TFT35 E3 v3.0

I set this up as I was unhappy with my build loop locally, and I can't figure out how (well okay I'm too lazy) to get PIO to dump the firmware right to my board. 

I'm an SRE by trade so setting up CI for my Marlin Configuratio was an easy thing for me. 

This repo is driven by a Github Action Workflow [.github/workflows/platformio.yml](https://github.com/CalvinRodo/MarlinConfiguration/blob/main/.github/workflows/platformio.yml), it should be fairly simple to modify for your own use. 

It's pretty straightforward, it will only run when the following files are changed on the `main` branch.

- Configuration.h
- Configuration_adv.h
- platformio.ini

## Here is a brief overview of what it does. 

1. It gets the Marlin Firmware.
https://github.com/CalvinRodo/MarlinConfiguration/blob/82ff4a0017c4fb1a25ae9b0cfde0784ebfe96593/.github/workflows/platformio.yml#L17-L:21

You can configure the branch or tag you want to get by modifying this line:

https://github.com/CalvinRodo/MarlinConfiguration/blob/82ff4a0017c4fb1a25ae9b0cfde0784ebfe96593/.github/workflows/platformio.yml#L20 

2. It then checks out this code and copies it on top of the existing configuration files here:

https://github.com/CalvinRodo/MarlinConfiguration/blob/82ff4a0017c4fb1a25ae9b0cfde0784ebfe96593/.github/workflows/platformio.yml#L37-L41

3. It builds using PIO: 

https://github.com/CalvinRodo/MarlinConfiguration/blob/82ff4a0017c4fb1a25ae9b0cfde0784ebfe96593/.github/workflows/platformio.yml#L42-L44

4. If that is successfull it tags the latest commit on the main branch using the action https://github.com/anothrNick/github-tag-action

https://github.com/CalvinRodo/MarlinConfiguration/blob/82ff4a0017c4fb1a25ae9b0cfde0784ebfe96593/.github/workflows/platformio.yml#L45-L49

5. It will then create a release of the tagged version and will upload the compiled `firmware.bin`here:

https://github.com/CalvinRodo/MarlinConfiguration/blob/82ff4a0017c4fb1a25ae9b0cfde0784ebfe96593/.github/workflows/platformio.yml#L50-L53

You can find the releases here: https://github.com/CalvinRodo/MarlinConfiguration/releases

It should be pretty easy to modify this for your own use, you just need to copy the `.github/workflows/platformio.yml` file into your own repo at that path, and then commit your configuration files. 
