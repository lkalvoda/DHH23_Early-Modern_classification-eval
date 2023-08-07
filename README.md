# Evaluation of CLIP-based classification of eighteenth-century images (ECCO)
Quantitative and qualitative analysis of image classification results produced using a CLIP-based model. Extension of the [Early Modern group's work](https://github.com/dhh23/early_modern) during the Helsinki Digital Humanities Hackathon 2023.

## Introduction and data
The Early Modern group investigated how the intellectual, economic, and societal changes of the Enlightenment era were reflected in the use of scientific illustrations. The sample examined consisted of works aimed at eighteenth-century British audiences, collected in the Eighteenth Century Collections Online (ECCO). Specifically, we used data from the Scientific collection, counting just over 100 000 individual pages containing illustrations.

During the Hackathon, three different image classification iterations were run, using or based on [the CLIP model](https://github.com/openai/CLIP):

1. **The first run (CLIP1)** used the zero-shot model, trained on ~ 2100 classification annotations produced by the group.
---- add numbers for annotations; no of groups, how many annotated per group ----


2. **The second run (CLIP2)** 

3. **The third run (CLIP3)**
------ 
While CLIP1 and 2 both gave the top one classification prediction only, with CLIP3, we had it
provide the two highest value predictions. This 'second most likely class' in the CLIP3 data, along with ------, makes it ideal for
further analysis. --------why---------

In the Hackathon outcomes, only classification entries with min. 50% accuracy for the first candidate were included into the
analyses and subsequent interpretation. However, the accurracy span was wide in all three runs. In this task, I summarise these tendencies, verify them with close-reading, and speculate on their possible reasons and outcomes. I do this on the data about the third run (CLIP3), for several reasons:
- the data from this run also provides the second most probable category the model assigned to each entry, which can shed light on the model's behaviour with this type of a dataset
- the model used in the third run was already customised based on human-annotated feedback on the previous two runs: --- and so ---

### Primary data
A spreadsheet containing (per image):
- URL from a database containing all images from the dataset (for qualitative close-reading analysis)
- first-choice category and the certainty score of the classification (score is based on training data; for CLIP3 this is human-produced image annotations (classification))
- second-choice category and -,,-

### Secondary data
A spreadsheet containing (per image):
- URL from a -,,-
- first-choice classification category as assigned by CLIP3
- certainty score of the classification (as compared to human-annotated control batch; i.e. the probability of CLIP3 classifying an image as the same category that human annotators did)

## Research question and hypothesis
RQ: ------ Do the certainty scores in CLIP3 predictions reflect the actual categories and/or visual form of the images classified, and, if so, then what are the tendencies? What can we conclude about the performance of a model thus customised? --------
H0:
H1:

## Methods
To answer the above, I examine the 'first-choice category' values in the primary data, focussing on the highest and the lowest confidence values to scan the data for possible patterns. To interpret any tendencies found, I use preliminary evaluation data produced during the Hackathon ('Secondary data' above), and close-reading of the images themselves.

## Conclusions

## Future directions
Performing a similar mixed-methods analysis on the prediction results made by CLIP1 and CLIP2 each, and then comparing all three runs could bring valuable insight into which features in particular had the most profound effect on the correspondence of the actual category and the one predicted. This could be in both directions: which specs increase the model's 'correctness' significantly, and are there perhaps any that we had predicted to be effective, but ended up making no to little difference?

## Acknowledgements
I'd like to thank Ari Vesalainen for providing me with valuable details on the three model runs.
