# Shadows Of Doubt Case Editing

## Intro

### Case Editor Tool

Cases can be created and modified using [piepieonline's web based tool](https://www.piepieonline.com/ShadowsOfDoubt-CaseEditor/) using Google Chrome browser.

### DDS Editor Tool

Evidence, dialogue, vMails, and some other things can be modified using [Shadows of Doubt dev team's editor tool](https://colepowered.itch.io/shadows-of-doubt-dialog-editor) or [piepieonline's DDS editor tool](https://www.piepieonline.com/ShadowsOfDoubt-DDSViewer/)

## How to

### Make a basic custom piece of evidence 

This evidence will spawn in the world as a crumpled pieces of paper. 
1. Open the DDS Editor. In a new DDS bundle, create a new tree for a document. ![](/assets/image/Shadows_of_Doubt_DDS_Editor_newtree.png)
2. Open the new tree to edit it.
3. Change the background on the right to crumpled paper, the size square, and move the text box back into the main frame of the image. ![](/assets/image/Shadows_of_Doubt_DDS_Editor_editdocumentbackground.png)
4. Click on the message box and then click on edit message the the top
5. On the first block click the cell to edit and enter `CITY NAME: |city.name|`
6. Click new block at the top of the window and enter `NEXT VICTIM: |killer.nextmurder.victim.fullname|` 
7. Click Done at the bottom.

![](/assets/image/Shadows_of_Doubt_DDS_Editor_dynamicCityandVictim.png)

What's happened so far? We have added 2 dynamic text blocks. Referring to the city and the killer's next victim's full name. 

![](/assets/image/Shadows_of_Doubt_DDS_Editor_completebasicdocument.png)

*`Tip: you can explore available DDS text by simply entering the first pipe, going up and down with arrows and pressing enter to expand into the next context`*

## MurderMO file

## Murder Manifest file

## Interactable Preset file
