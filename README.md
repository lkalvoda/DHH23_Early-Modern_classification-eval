# Evaluation of CLIP-based classification of eighteenth-century images (ECCO)
Quantitative and qualitative analysis of image classification results produced using a CLIP-based model. Extension of the [Early Modern group's work](https://github.com/dhh23/early_modern) during the Helsinki Digital Humanities Hackathon 2023.

## Introduction and data
The Early Modern group investigated how the intellectual, economic, and societal changes of the Enlightenment era were reflected in the use of scientific illustrations. The sample examined consisted of works aimed at eighteenth-century British audiences, collected in the Eighteenth Century Collections Online (ECCO). Specifically, we used data from the Scientific collection, counting just over 100 000 individual pages containing illustrations.

During the Hackathon, three different image classification iterations were run, using or based on [the CLIP model](https://github.com/openai/CLIP). Changes were made based on parallel close-reading analysis, as well as evaluation.

**1. The first run (CLIP1)** used the zero-shot model, trained on ~ 2100 classification annotations produced by the Early Modern group. The amount of annotation entries was distributed over given classes as follows:

| Class                    | Count   |
| :----------------------- | :-------|
| 1. Anatomy               | 72      |
| 2. Architecture          | 26      |
| 3. Botany                | 393     |
| 4. Mathematics/Astronomy | 896     |
| 5. Mechanics/Tools       | 185     |
| 6. Miscellaneous/Other   | 332     |
| 7. Zoology               | 262     |
| **{\textstyle \sum }**   | **2166**| 

These served as the training data for all three runs, with the second and third run having additional modifications. A line of reasoning to be examined below is whether the amount of training material in a category could affect the performance in it. However, a counter-argument would be that the sample was chosen randomly and presumed to be representative of the population (i.e., the whole dataset the group worked with).

**2. For the second run (CLIP2)**, the number and names of both classes and keywords were changed to:

| Category                          | Keywords                                                                                                                                            |
| :-------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. Agriculture/Gardening          | "garden agriculture farming husbandry"                                                                                                              |
| 2. Anatomy                        | "medicine anatomy surgery body organ heart lung dissection artery brain neural system kidney liver muscle bone joint"                               |
| 3. Architecture                   | "building column landscape architectural plan"                                                                                                      |
| 4. Botany                         | "flower seed fruit petal botany root tree plant stem leaf fungi herb"                                                                               |
| 5. Cooking                        | "plate cutlery tea pie porcelain menu"                                                                                                              |
| 6. Mathematics/Geometry/Astronomy | "geometry algebra astronomy triangle mathematics globe map universe earth trigonometry"                                                             |
| 7. Mechanics/Tools                | "surgical instrument microscope knife scissors machine tool mechanics lister thermometer scales needle telescope orrery wood bottle vial carpentry" |
| 8. Microbiology                   | "cell embryo bacteria tissue microbe"                                                                                                               |
| 9. Miscellaneous                  | "text letter ornament person people table of contents coats of arms emblem flag optical"                                                            |
| 10. Sea                           | "sea water boat navigation compass naval ship"                                                                                                      |
| 11. Zoology 1                     | "mammal animal horse cattle"                                                                                                                        |
| 12. Zoology 2                     | "bird egg nest insect fish eel wing feather reptile butterfly horn"                                                                                 |

**3. The third run (CLIP3)** model was fine-tuned to categories and keywords merged and/or extended as follows:

| Category                 | CLIP2 categories (and their keywords) it consists of |
| :----------------------- | :----------------------------------------------------|
| 1. Anatomy               | Anatomy                                              |
| 2. Architecture          | Architecture, Agriculture/Gardening                  |
| 3. Botany                | Botany, Microbiology, Agriculture/Gardening          |
| 4. Mathematics/Astronomy | Mathematics/Geometry/Astronomy                       |
| 5. Mechanics/Tools       | Mechanics/Tools, Agriculture/Gardening               |
| 6. Miscellaneous/Other   | Cooking, Miscellaneous, Sea, Agriculture/Gardening   |
| 7. Zoology               | Zoology 1, Zoology 2                                 |


Additionally, while CLIP1 and 2 both gave the top one classification prediction only, with CLIP3, we had it
provide the two highest value predictions. This 'second most likely class' in the CLIP3 data and the above information on categories and keywords make CLIP3 ideal for further analysis. The results could shed light on specifications desirable for work with similar Enlightenment era book illustrations.

In the Hackathon outcomes, only classification entries with min. 50% accuracy for the first candidate were included into the
analyses and subsequent interpretation. However, the accurracy span was wide in all three runs. In this task, I summarise these tendencies, verify them with close-reading, and speculate on their possible reasons and outcomes. I do this on the data about the third run (CLIP3), for several reasons:
- the data from this run also provides the second most probable category the model assigned to each entry, which can shed light on the model's behaviour with this type of a dataset
- the model used in the third run was already customised based on human-annotated feedback on the previous two

### Primary data
A spreadsheet containing (per image):
- URL from a database containing all images from the dataset (for qualitative close-reading analysis)
- CLIP3 first-choice category and the certainty score of the classification (score is based on training data; for CLIP3 this is human-produced image annotations (classification))
- CLIP3 second-choice category and -,,-

### Secondary data
A spreadsheet containing (per image):
- URL from a -,,-
- CLIP3 first-choice classification category as assigned by CLIP3
- CLIP3 certainty score of the classification (as compared to human-annotated control batch; i.e. the probability of CLIP3 classifying an image as the same category that human annotators did)

## Research question and hypothesis
RQ: Do the certainty scores in CLIP3 predictions correspond to the actual categories and/or visual form of the images classified, and, if so, then what are the tendencies? Is there significant variation in performance between clategories? Are there CLIP3 predictions not corresponding to human classification in cases classified by CLIP with low/high confidence? What can we conclude about the performance of a model thus customised?

H0: There are no significant patterns in the performance of CLIP3 across categories.
H1: There is a significant amount of misclassified images (as compared to human-produced classification).
H2: CLIP3 performed significantly better in one or more categories (as compared to other categories).
H3: CLIP3 performed significantly worse in one or more categories (as compared to other categories).
H4: The classifications made by CLIP3 do not correspond to human classification in those cases where it states low prediction confidence.
H5: The classifications made by CLIP3 do not correspond to human classification in those cases where it states high prediction confidence.

## Methods
To answer the above, I examine the 'first-choice category' values in the primary data, focussing on the highest and the lowest confidence values to scan the data for possible patterns. To interpret any tendencies found, I use preliminary evaluation data produced during the Hackathon ('Secondary data' above), and close-reading of the images themselves.

## Conclusions

## Future directions
Performing a similar mixed-methods analysis on the prediction results made by CLIP1 and CLIP2 each, and then comparing all three runs could bring valuable insight into which features in particular had the most profound effect on the correspondence of the actual category and the one predicted. This could be in both directions: which specs increase the model's 'correctness' significantly, and are there perhaps any that we had predicted to be effective, but ended up making no to little difference?

## Acknowledgements
I'd like to thank Ari Vesalainen for providing me with valuable details on the three model runs.
