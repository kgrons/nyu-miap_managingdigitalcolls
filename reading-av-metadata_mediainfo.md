
# Reading key A/V metadata with MediaInfo

The following information was originally used in the _NDSR 2016 Immersion Week - Automating Procedures for Digital Asset Management_ presentation found in the [America Archive of Public Broadcasting Immersion Week GitHub repository](https://github.com/NationalDigitalStewardshipResidency/aapbndsr_iw2016/tree/master/KathrynGronsbell). 

## Overview

This page focuses on getting comfortable using a common tool - [MediaInfo](http://mediaarea.net/en/MediaInfo) - for basic metadata tasks related to audiovisual archiving and preservation. 


## Getting started

1. Open Terminal (Applications > Utilities > Terminal). 

2. Download copies of collection materials. Use `mv` to move the zip file to your Desktop. Then use `unzip` to unpackage it into a directory (see [cli-basics](./cli-basics.md) for a refresher on how to do this). 

3. You should already have MediaInfo installed. Check this by trying to look at the documentation for MediaInfo by typing this into the Terminal:

            mediainfo --Help


If you do not have either of these tools installed, [install MediaInfo](http://mediaarea.net/en/MediaInfo/Download). If you are using Homebrew (which is a great, simple to use package installer for Mac), you can simply type for MediaInfo:

            brew install media-info


### Read metadata using MediaInfo

MediaInfo is ["a convenient unified display of the most relevant technical and tag data for video and audio files."](https://mediaarea.net/en/MediaInfo). It also is one of the most common and referenced metadata tools for a/v material in use by those working in the archiving and preservation fields. The tool has a GUI but these instructions will explore MediaInfo on the CLI. The CLI has more flexibility and opportunities for customization of commands. It also makes it possible to integrate MediaInfo commands into programs or scripts, if you choose to in the future. 

1. Let's start by looking at MediaInfo's output when it is run on a sample file with no options. `cd` to the folder with local copies of collection material on your Desktop. Run this command and look at the output:

            mediainfo aquarium.mov


 The data presented as part of this full output may be divided into:
 - General
 - Video
 - Audio
 - Text
 - Chapters
 - Other

 You may also wonder what [KiB, MiB, GiB](https://mediaarea.net/us/MediaInfo/Support/FAQ#BinaryPrefix) is in the File Size value?

2. You can also review the output formatted as XML by adding an option and then opening the XML. This command redirects MediaInfo's output to a new XML document you are creating in your working folder:

            mediainfo --Output=XML aquarium.mov > ~/Desktop/aquarium-mediainfo.xml

3. Now, open that XML file and review. Type this command to open the XML file in your default XML viewing application:

            open aquarium-mediainfo.xml

4. Run MediaInfo on the other files from this collection. 
 - Review the output with a partner. 
 - Where is the technical metadata? The descriptive metadata? Where are administrative values present?

 - Run MediaInfo with the Full option (`-f`) - what additional information is available in the output? 

5. There may be workflows where you do not want the general output from a metadata extraction tool. For example, you may just want to audit the wrapper formats or durations for a target set of files. You can specify which tags you want to output from MediaInfo. Try out these commands for any of the sample files:

            mediainfo --Inform="General;%FileName%" aquarium.mov


            mediainfo --Inform="Video;%Format%" aquarium.mov


            mediainfo --Inform="Audio;%SamplingRate%" aquarium.mov

6. Now try to output only the values for: *duration, video bit depth, and audio compression mode* for a few different files. (HINT: Run `mediainfo --Language=raw [file]` to see the tag names as they need to be called as an option.) You can also throw the `--Inform` options together on the same line - so the combined command for Step #5 would look like:
            
            mediainfo --Inform="General;%FileName%" --Inform="Video;%Format%" --Inform="Audio;%SamplingRate%" aquarium.mov

  Want to dig down to a specific string within the full output? Find out from this [stackexchange answer](http://stackoverflow.com/a/26508567) from the MediaInfo creator/main developer. 

7. How to create formatted PBCore record outputs using MediaInfo:

            mediainfo --Output=PBCore aquarium.mov > ~/Desktop/aquarium-pbcore.xml
            
            mediainfo --Output=PBCore2 aquarium.mov > ~/Desktop/aquarium-pbcore2.xml


## Recommended resources

- Check out the original version of this exercise, which includes using *ffprobe* which "gathers information from multimedia streams and prints it in human- and machine-readable fashion". It, like MediaInfo, is a common metadata extaction and analysis tool that can be incorporated into workflows or used on its own. Additional resources and exercises are available in the [America Archive of Public Broadcasting Immersion Week GitHub repository](https://github.com/NationalDigitalStewardshipResidency/aapbndsr_iw2016/tree/master/KathrynGronsbell).
