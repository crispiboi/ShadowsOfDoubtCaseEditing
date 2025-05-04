# Shadows Of Doubt Case Editing

## Intro

### Case Editor Tool

Cases can be created and modified using [piepieonline's web based tool](https://www.piepieonline.com/ShadowsOfDoubt-CaseEditor/) using Google Chrome browser.

### DDS Editor Tool

Evidence, dialogue, vMails, and some other things can be modified using [Shadows of Doubt dev team's editor tool](https://colepowered.itch.io/shadows-of-doubt-dialog-editor) or [piepieonline's DDS editor tool](https://www.piepieonline.com/ShadowsOfDoubt-DDSViewer/)

## How to

### Make a basic custom piece of DDS evidence 

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

> Tip: you can explore available DDS text by simply entering the first pipe, going up and down with arrows and pressing enter to expand into the next context

### Migrate your DDS data for the custom evidence

The evidence DDS data is created but we need to move it into the folders that meet the structure for the case editor.

1. Drill into your DDS Editor's save folder.

`Shadows DDS Editor Build\Shadows of Doubt DDS Editor_Data\StreamingAssets\DDS\(YOUR BUNDLE)`

2. Open the Case Editor's file folder. 

`ExampleCase\DDSContent`

3. Move files in directories as follows

DDSEditor\Trees -> CaseEditor\DDSContent\DDS\Trees

DDSEditor\Messsages -> CaseEditor\DDSContent\DDS\Messsages

DDSEditor\Blocks -> CaseEditor\DDSContent\DDS\Blocks

4. Move these files as follows

DDSEditor\Strings\English\dds.blocks -> CaseEditor\DDSContent\Strings\English\DDS

5. Create evidence.names in CaseEditor\DDSContent\Strings\English\Evidence
6. Edit evidence.names and add a new row

`KillerNotes,,"Note",,,,11:49 05/03/2025`
> Note the time and date here does not appear to matter. The important entries are KillerNotes and "Note" 

### Create InteractablePreset file for the evidence to spawn in the world
1. In the [case editor tool](https://www.piepieonline.com/ShadowsOfDoubt-CaseEditor/) click Add new file.
2. Select InteractablePreset from the dropdown for File Type, and CrumpledPaper for the Copy From, name your file. Name this file `KillerNotesInteractable`

> Tip: It's important to keep track of your file names and which evidence they tie to. Name your files appropriately! 

3. For simplicity sake in this guide, edit the file directly first and paste this in as the json.

```
{
  "name": "KillerNotesInteractable",
  "fileType": "InteractablePreset",
  "copyFrom": "InteractablePreset|Note",
  "presetName": "KillerNotesInteractable",
  "spawnEvidence": "REF:EvidencePreset|KillerNotesEvidence",
  "fingerprintsEnabled": true,
  "printsSource": 12,
  "summaryMessageSource": "2007b0c9-ed2b-487c-99a8-152a0ba19977",
  "fingerprintDensity": 4
}
```
4. Go back to the case editor tool and open the file. 
5. Refer to your DDS Editor again for the GUID for the evidence in the top right of the window, and copy this value.

![](/assets/image/Shadows_of_Doubt_DDS_Editor_guidpointer.png)

6. Paste the value into the summaryMessageSource field in the case editor.

What's going on at this point? We have a file that refers to the DDS we have created and define some basic additional attributes for the evidence that will spawn in the world. The enum should be translated by the case editor tool where printsSource 12 is the killer's prints. We have a placeholder for the evidence file (KillerNotesEvidence) that will be opened in the evidence board. Everything else will be copied from the vanilla Note preset unless overridden.

### Create the EvidencePreset file for the evidence to appear in case board
1. In the [case editor tool](https://www.piepieonline.com/ShadowsOfDoubt-CaseEditor/) click Add new file.
2. Select EvidencePreset from the dropdown for File Type, and CrumpledPaper for the Copy From, name your file. Name this file `KillerNotesEvidence`

> Tip: Again, It's important to keep track of your file names and which evidence they tie to. Name your files appropriately! 

3. Just like for the interactablePreset, edit the file again directly and paste this as the json for simplicity.

```
{
  "name": "KillerNotesEvidence",
  "fileType": "EvidencePreset",
  "copyFrom": "EvidencePreset|CrumpledNameCipher",
  "presetName": "KillerNotesEvidence",
  "ddsDocumentID": "2007b0c9-ed2b-487c-99a8-152a0ba19977
}
```
5. Just like in the InteractablePreset file, make sure the ddsDocumentID is the one from the DDS Editor.

### Prepare the MurderMO file to use the custom evidence
1. In the [case editor tool](https://www.piepieonline.com/ShadowsOfDoubt-CaseEditor/) open the murderMO file that is created by default. 
2. Right click on "MOleads" to add a new entry, then expand the tree.

![](/assets/image/Editor_expandMO.png)

* Refer to the MurderMO file reference for details on what the fields do.
3. For the example, enter the name `KillerNotes`and fill out the first few entries as follows

|compatibleWithAllMotives|true|
|spawnOnPhase|executing|
|tryToSpawnWithEachNewMurder|true|
|belongsTo|killer|
|chance|1|

4. On the spawnItem dropdown, click the entry for custom, and in the prompt that opens, enter `KillerNotesInteractable`

![](/assets/image/Editor_completedMO.png)

What's set up at this point? We have some basic spawning variables set for the evidence. Most importantly, we have called the custom KillerNoteInteractable file that we created, which will spawn in the world with the settings we applied. The object in the world when interacted with will now refer to the KillerNoteEvidence file we created, which in turn will display the DDS object we created in the editor.

 
## MurderMO file

## Murder Manifest file

## Interactable Preset file
