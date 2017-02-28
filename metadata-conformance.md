# Checking metadata conformance with MediaConch

## Overview

This page focuses on getting comfortable using the MediaConch tool to check metadata conformance across a variety of audiovisual formats using one or many policies. It is "an extensible, open source software project consisting of an implementation checker, policy checker, reporter, and fixer that targets preservation-level audiovisual files (specifically Matroska, Linear Pulse Code Modulation (LPCM) and FF Video Codec 1 (FFV1)) for use in memory institutions, providing detailed and batch-level conformance checking" [[From the MediaConch _Project Overview_](https://mediaarea.net/MediaConch/about.html)].

## Getting started

On the [MediaConch website](https://mediaarea.net/MediaConch/) you can find directions on how to download/install the CLI and/or GUI versions. We will use the web version for this exercise. See the next section to get started.

## Using MediaConch (GUI)
1. For this exercise, we will explore the user-friendly [MediaConchOnline](https://mediaarea.net/MediaConchOnline/). Click _Software > MediaConchOnline_.

2. We will create a new policy, and run a conformance check based on that policy on some sample files. Here is an overview of what a policy is from [MediaConch's "How to Use" Documentation, *Policies* section](https://mediaarea.net/MediaConch/documentation/HowToUse.html) (emphasis mine):  

> In the “Policies” section, you can create customized policy tests to check for conformance to a specific set of standards that your collection must adhere to. You can also import previously generated policy sets in either XSL or Schematron format.

> **Policy sets consist of individual rules and assertions. A policy may contain one or more rules, and rules may consist of one or more asserts.** Rules and asserts typically contain a metadata field (e.g., “Format”), that field’s associated metadata stream type (e.g., “General), a validator (e.g., “is_equal), and a desired value (e.g., “Matroska”). Rules and asserts are automatically saved during creation, but you may duplicate or delete it using the associated buttons on each rule/assertion window.

> For example, the following rule/assertion would ensure that all reported files must contain a frame rate associated with the NTSC broadcast standard:

> * Type: General
> * Field: FrameRate
> * Validator: Equal
> * Value: 29.970

### Run a conformance check

1. First, we are going to use the checker with an **existing policy**, which you can download [here](./mediaconch-samples/NYU-MIAP-samplepolicy.xml) (Click _Raw_ and _Save as..._). 

2. Go to the [MediaConchOnline Policy Checker](https://mediaarea.net/MediaConchOnline/policyEditor). Note you are logged in as a Guest. (Later you can register by creating a username / password.)

3. Under _Import a Policy_, use the selection tool to choose the sample XML file (NYU-MIAP-samplepolicy.xml). The click the _Import Policy_ button.

4. On the left side of the screen, you will see your policy listed with all its associated rules/assertions. Select **General/Format is QuickTime**. What do you see on the right side of the screen? (Hover over the `i` tool tips for more info about the fields that make up each rule). Check out a few more of the rules within this sample policy.

5. OK now it's time for the **Checker**. At the top of the screen, click _Checker_ from the menu options. 

6. Under _Check Files_, click on the _Check by file upload_ tab. 

7. Configure the following:
  - **Policy** - choose aquarium.mov (sample policy)
  - **Display** - choose MediaConch HTML
  - **Verbosity** - choose Default level
  - **File (max 128M)** - choose your local copy of aquarium.mov

8. Click _Check File_. Let's review our results in the **Results** section together.
  - Click the 👁️ under Policy to see pass/fail info per rule
  - Apply a different public policy to all results (drop down menu directly below **Results** header)

9. Now try running the sample or public policies on other sample files. Review the results across files with different formats, codecs, number of channels, etc. 

### Create a new policy

1. Pick a sample A/V file (not aquarium.mov). There are 2 simple ways to create a new policy. The first is to simply and manually add rules in the **Policy editor**. Or you can upload an A/V file, have MediaConch analyze it and auto-populate rules as a new policy. We are going to start with the manual approach.

2. Run MediaInfo on your sample A/V file and keep Terminal open to scroll through the output:

  `mediainfo your-sample-file.mov`

3. Create a new policy in MediaConchOnline's **Policy editor** based on **FIVE** metadata fields in the MediaInfo output for your sample A/V file. (Hint: review [**Create a policy Documentation**](https://mediaarea.net/MediaConch/documentation/HowToUse.html) for steps on how to add rules to your policy)

4. Use MediaConchOnline to test your policy against the sample A/V file with the Checker. Did it pass?

## Next: Use the CLI!

- Download/install the [command-line version of MediaConch](https://mediaarea.net/MediaConch/installation.html). 
- Check out the manual page by typing `mediaconch --Help` into Terminal to see how to structure CLI commands and use options to run conformance checking. 
