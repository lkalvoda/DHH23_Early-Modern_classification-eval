# Evaluation of CLIP-based classification of eighteenth-century images (ECCO)
Quantitative and qualitative analysis of image classification results produced using a CLIP-based model. Extension of the [Early Modern group's work](https://github.com/dhh23/early_modern) during the Helsinki Digital Humanities Hackathon 2023.


## Introduction and data
The Early Modern group investigated how the intellectual, economic, and societal changes of the Enlightenment era were reflected in the use of scientific illustrations. The sample examined consisted of works aimed at eighteenth-century British audiences, collected in the Eighteenth Century Collections Online (ECCO). Specifically, we used data from the Scientific collection, counting just over 100 000 individual pages containing illustrations.

During the Hackathon, three different image classification iterations were run, using or based on [the CLIP model](https://github.com/openai/CLIP). Changes were made based on parallel close-reading analysis, as well as evaluation.

**1. The first run (CLIP1)** used the zero-shot model, trained on ~ 2100 classification annotations produced by the Early Modern group. The amount of annotation entries was distributed over given classes as follows:

| Class                    | Count    |
| :----------------------- | :--------|
| 1. Anatomy               | 72       |
| 2. Architecture          | 26       |
| 3. Botany                | 393      |
| 4. Mathematics/Astronomy | 896      |
| 5. Mechanics/Tools       | 185      |
| 6. Miscellaneous/Other   | 332      |
| 7. Zoology               | 262      |
| **Σ**                    | **2166** |

*Table 1 The figures for our training data images, as classified into categories by human annotators*

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

*Table 2 Categories and keywords for CLIP2*

**3. The third run (CLIP3)** model was fine-tuned to categories and keywords merged and/or extended as follows:

| Category                          | CLIP2 categories (and their keywords) it consists of |
| :-------------------------------- | :----------------------------------------------------|
| 1. Anatomy                        | Anatomy                                              |
| 2. Architecture                   | Architecture, Agriculture/Gardening                  |
| 3. Botany                         | Botany, Agriculture/Gardening                        |
| 4. Cooking                        | Cooking                                              |
| 5. Mathematics/Geometry/Astronomy | Mathematics/Geometry/Astronomy                       |
| 6. Mechanics/Tools                | Mechanics/Tools, Agriculture/Gardening               |
| 7. Microbiology                   | Microbiology                                         |
| 8. Miscellaneous/Other            | Miscellaneous, Agriculture/Gardening                 |
| 9. Sea                            | Sea                                                  |
| 10. Zoology                       | Zoology 1, Zoology 2                                 |

*Table 3 Categories and keywords for CLIP3*

Additionally, while CLIP1 and 2 both gave the top one classification prediction only, with CLIP3, we had it
provide the two highest value predictions. This 'second most likely class' in the CLIP3 data and the above information on categories and keywords make CLIP3 ideal for further analysis. The results could shed light on specifications desirable for work with similar Enlightenment era book illustrations.

In the Hackathon outcomes, only classification entries with min. 50% accuracy for the first candidate were included into the
analyses and subsequent interpretation. However, the accurracy span was wide in all three runs. In this task, I summarise these tendencies, verify them with close-reading, and speculate on their possible reasons and outcomes. I do this on the data about the third run (CLIP3), for several reasons:
- the data from this run also provides the second most probable category the model assigned to each entry, which can shed light on the model's behaviour with this type of a dataset
- the model used in the third run was already customised based on human-annotated feedback on the previous two

### Primary data
A spreadsheet containing (per image):
- its URL (from a database containing all images from the dataset; for qualitative close-reading analysis)
- CLIP3 first-choice category and the certainty score of that classification (score is based on training data; for CLIP3, this is human-produced image classification annotations)
- CLIP3 second-choice category and the certainty score of that classification (-,,-)

### Secondary data
(used for refining the RQ and hypotheses; would recommend for exploration of H2, H3)
A spreadsheet containing (per every image from CLIP3 first-choice):
- its URL (see Primary data)
- CLIP3 first-choice category (see Primary data)
- evaluation score of that classification (i.e., a percentage score expressing the probability of a human annotator classifying an image as belonging in the same first-choice category as CLIP3 did; based on human-annotated control batch produced by the group)<br>
Various visualisations based on the above spreadsheet (created during the hackathon)


## Research question(s), hypotheses
RQ: Do the certainty scores in CLIP3 predictions correspond to the actual categories and/or visual form of the images classified, and, if so, then what are the tendencies? Is there significant variation in performance between clategories? Are there CLIP3 predictions not corresponding to human classification in cases classified by CLIP with low/high confidence? What can we conclude about the performance of a model thus customised?

**H0:** There are no significant patterns in the performance of CLIP3 across certainty levels and categories.

**H1:** There is a significant amount of misclassified images (as compared to human-produced classification).<br>
(fals.: There is not a significant amount of misclassified images (as compared to human-produced classification).)

**H2:** CLIP3 performed significantly better in one or more categories (as compared to other categories).<br>
(fals.: CLIP3 did not perform significantly better in any category (as compared to other categories).)

**H3:** CLIP3 performed significantly worse in one or more categories (as compared to other categories).<br>
(fals.: CLIP3 did not perform significantly worse in any category (as compared to other categories).)

**H4a:** A significant amount of first-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states low prediction confidence.<br>
(fals.: There is not a significant amount of first-choice classifications made by CLIP3 that do not correspond to human classification in those cases where CLIP3 states low prediction confidence.)

**H4b:** A significant amount of second-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states low prediction confidence.<br>
(fals.: There is not a significant amount of second-choice classifications made by CLIP3 that do not correspond to human classification in those cases where CLIP3 states low prediction confidence.)

**H5a:** A significant amount of first-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states high prediction confidence.<br>
(fals.: There is not a significant amount of first-choice classifications made by CLIP3 that do not correspond to human classification in those cases where CLIP3 states high prediction confidence.)

**H5b:** A significant amount of second-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states high prediction confidence.<br>
(fals.: There is not a significant amount of second-choice classifications made by CLIP3 that do not correspond to human classification in those cases where CLIP3 states high prediction confidence.)

## Methods, results
To answer the above, I examined the 'first-choice category' values in the primary data, focussing mainly on the highest and the lowest confidence values to scan the data for possible patterns. To interpret any tendencies found, I used preliminary evaluation data produced during the Hackathon ('Secondary data' above), and close-reading of the images themselves. 

To test H4a/b and H5a/b, I started by filtering out entries with the highest and the lowest first-choice confidence scores in the following ranges:<br>
**'Low-confidence' subset**  (2734 entries)<br>
      x ∈ [0;30) <br>
i.e.  0 ≤ x < 30.(0)


**'High confidence' subset** (95 781 entries)<br>
      x ∈ (70;100]<br>
i.e.  70.(0) < x ≤ 100.(0)

For the 'Low-confidence' subset, I started by looking at the distribution of certainty scores:<br>
| Score range | Number of entries |
| :---------- | :-----------------|
| [0-5)       | 0                 |
| [5-10)      | 0                 |
| [10-15)     | 0                 |
| [15-20)     | 18                |
| [20_25)     | 656               |
| [25_30)	  | 2060              |
| **Σ**       | **2734**          | 

*Table 4 Detailed distribution of entries per certainty score range in the 'Low-confidence' subset*

Besides being a valuable item of information in and of itself, it allowed me to take a weighted sample from each subset for the close-reading result verification below. Doing this enabled me to conduct a mixed-methods analysis viably, especially later for the second subset. Below is the same data for the second subset:

| Score range | Number of entries |
| :---------- | :-----------------|
| (70-75]     | 7904              |
| (75-80]     | 7857              |
| (80-85]	  | 8089              |
| (85-90]	  | 9443              |
| (90-95]	  | 12161             |
| (95-100]	  | 50327             |
| **Σ**       | **95781**         | 

*Table 5 Detailed distribution of entries per certainty score range in the 'High-confidence' subset*

Next (this further narrowing down of the subsets was mainly due to the high number of entires especially in the second subset), I took a random sample of approximately 270 entries (guided by: 10 % of 'Low-confidence' subset). The distribution across the 'Score ranges' (See Table 4 above) was weighted by the respective number of entries in these; i.e., for the 'Low-confidence' subset:

| Score range | Number of entries for analysis |
| :---------- | :------------------------------|
| [15-20)     | 2                              |
| [20_25)     | 65                             |
| [25_30)	  | 203                            |
| **Σ**       | **270**                        | 

*Table 6 Number of entries for analysis in the 'Low-confidence' subset*

I close-read the randomly generated entries to verify whether the CLIP3 classification given for each of these corresponds to my own (i.e., human-produced) classification. I noted this down in a 0-1 system. I annotated both the first- and the second-choice classification in this manner, and the close-reading analysis results follow below. Table 7 below shows the four annotation possibilities and the actual distribution of these among the 270 entries annotated:<br>

| First-second                                              | Occurrences in 'Low-confidence' subset |
| :-------------------------------------------------------- | :--------------------------------------|
| 0-0 = neither classification is possibly correct          | 101                                    |
| 0-1 = first-choice is incorrect, second-choice is correct | 79                                     |
| 1-0 = first-choice is correct, second-choice is incorrect | 69                                     |
| 1-1 = both classifications are correct (acceptable)       | 21                                     |
| **Σ**                                                     | **270**                                | 

*Table 7 The four annotation possibilities for human evaluation of CLIP3 classifications of the 'Low-confidence' subset (random weighted sample) explained; how many times each one of these combinations occurrs in the dataset*

Note: A potential caveat of this method is that even a human assessor cannot always classify an illustration with full certainty, either; e.g., Anatomy v Botany in Figure 1 below. In this particular case, CLIP3 classified this image as Anatomy (20.57 %) or Botany (19.02 %), so both answers were noted as '1'. The approach taken is the same used in the group work evaluation: if a classification is feasible, it is regarded as correct; otherwise, it is obviously incorrect. For example, in Figure 2 we can see an image that would belong to Miscellaneous/Other, so both the first-choice Zoology (20.73 %) and the second-choice Mechanics/Tools (20.09 %) get a score of '0'.

<img width="200" alt="Figure 1" src="https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/23a39c4e-a3ce-477c-8ef3-f6d46c535644">

*Figure 1 Image annotated as correctly classified by CLIP3 as either Anatomy (first-choice) or Botany (second-choice)*

![Figure 2](https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/8d7cd94e-a7bc-4975-844d-dadb85e67573)

*Figure 2 Image annotated as incorrectly classified by CLIP3 as either Zoology or Mechanics/Tools*

It must be stressed that often, it is simply not possible for a human annotator to classify an image into one category, either, in which case any CLIP3 classification that is not in clear contradiction with the annotator's observation is noted as correct. Below are several examples of different kinds of frequent misclassifications (first-choice or both choices).

A strong tendency observed in the 'Low-confidence' subset was for images to be falsely classified as either Zoology or Architecture, no matter their human-annotated class.
A peculiar example (Figures 3 and 4) that was quite frequent was (obviously to the human eye) geometric shapes classified by CLIP3 as first-class Zoology.

<img width="200" alt="Figure 3" src="https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/7db7b2a1-8f1a-4bdb-b55d-a50c0fa999d2">

*Figure 3 Image classified by CLIP3 as Zoology (27.73 %) and Miscellaneous/Other (24.48 %)*

<img width="200" alt="Figure 4" src="https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/0930cf25-95d7-4c86-9087-28b3b0c24a52">

*Figure 4 Image classified by CLIP3 as Zoology (25.9 %) and Miscellaneous/Other (20.48 %)*

Another CLIP3 tendency in this subset was classifying what we would describe as a single straight line, essentially (i.e. Miscellaneous/Other, or, possibly, Mathematics/Geometry/Astronomy) in the first choice as Zoology. In Figure 5, the second-choice classification is correct, but the first-choice one is somewhat staggering.

<img width="200" alt="Figure 5" src="https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/3b3a13ad-bedd-4946-bee2-7ecfaeeaf026">

*Figure 5 Image classified by CLIP3 as Zoology (27.51 %) and Miscellaneous/Other (15.67 %)*

Figure 6 shows another example of an obvious misclassification (human-annotated only possibly as Miscellaneous/Other):

<img width="200" alt="Figure 6" src="https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/1cdf81e1-0bd4-47d8-b232-6aa16ff54db0">

*Figure 6 Image classified by CLIP3 as Zoology (27.83 %) and Anatomy (24.56 %)*

Finally, an example that we would actually have expected, is a botanical drawing classified as both Botany and Zoology with a 25.93 % certainty (Figure 7): 

<img width="200" alt="FIgure 7" src="https://github.com/lkalvoda/DHH23_early-modern_classification-eval/assets/135222568/0a9e9213-2ebd-4271-b437-6a7913b747c9">

*Figure 7 Image classified by CLIP3 as both Botany and Zoology with the same certainty (25.93 %)*

With the above in mind, when we turn back to Table 7, we can see that the largest portion of entries was misclassified entirely (0-0). The 1-1 and 1-0 scores can be taken as one category, since both are perfectly correct. The 0-1 category is notably large, and would definitely merit further analysis, as described in the relevant section below.

The summarised figures (for each choice out of the total of 270) are as follows:
- first-choice correct: 91
- first-choice incorrect: 179
  
- second-choice correct: 100
- second-choice incorrect: 170,

presenting evidence in the direction of considering both H4a and H4b valid.


Onto our second dataset, the distribution of the sample (n=270) of entries analysed in the same manner in the 'High-confidence' subset is shown in Table 8 below.

| Score range | Number of entries for analysis |
| :---------- | :------------------------------|
| (70-75]     | 22                             |
| (75-80]     | 21                             |
| (80-85]	  | 23                             |
| (85-90]	  | 28                             |
| (90-95]	  | 34                             |
| (95-100]	  | 142                            |
| **Σ**       | **270**                        | 

*Table 8 Number of entries for analysis in the 'High-confidence' subset*

Annotating this subset in the same manner as the 'Low-confidence' one above, Table 9 shows the distribution of correctness of CLIP3 classification combinations in this subset:

| First-second                                              | Occurrences in 'High-confidence' subset |
| :-------------------------------------------------------- | :---------------------------------------|
| 0-0 = neither classification is possibly correct          | 13                                      |
| 0-1 = first-choice is incorrect, second-choice is correct | 14                                      |
| 1-0 = first-choice is correct, second-choice is incorrect | 224                                     |
| 1-1 = both classifications are correct (acceptable)       | 15                                      |
| **Σ**                                                     | **270**                                 | 

*Table 9 The four annotation possibilities for human evaluation of CLIP3 classifications of the 'High-confidence' subset (random weighted sample) explained; how many times each one of these combinations occurrs in the dataset*

The summarised figures (for each choice out of 270) in this subset are as follows:
- first-choice correct: 236
- first-choice incorrect: 34
  
- second-choice correct: 33
- second-choice incorrect: 237,

presenting evidence in the direction of H5a being false. This is expected, but what is more interesting is the data's supporting H5b. At a first glance, a large portion of the second-choice classifications from the annotated sample being incorrect might seem like a 'negative' metric. However - and this was one of the motivations behind the mixed design - in the 'High'confidence' dataset, this turns out to be in majority because the entries in question can actually only be classified as a single class. Therefore, the only 'correct' combination is 1-0.


H1 is very broad, so to answer it, I first consider the outcomes of H4a,b and H5a,b with the following rationale: the presence of evidence supporting one or more of these increases the likelihood of H1 being supported by the data, too. As it is the case for H4a,b and 5b:

H4a: A significant amount of first-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states low prediction confidence;<br>
H4b: A significant amount of second-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states low prediction confidence;<br>
H5b: A significant amount of second-choice classifications made by CLIP3 does not correspond to human classification in those cases where CLIP3 states high prediction confidence,

I choose to examine H1. In order to do that, the selection of data is extended slightly to be more representative. The 'H1 dataset' is comprised of the 'Low-confidence' and the 'High-confidence' datasets, plus a 'Mid-confidence' smaller one, spanning entries with 45-55 % certainty.<br>
Using the same method as before, we look at the distribution of entries across the category:

| Score range | Number of entries |
| :---------- | :-----------------|
| [45-50)     | 8052              |
| [50-55)     | 8902              |
| **Σ**       | **16954**         | 

*Table 10 Detailed distribution of entries per certainty score range in the 'Mid-confidence' subset*

In consistency with the samples from the abovementioned, 270 entries chosen randomly from the 'Mid-confidence' dataset will be examined by close-reading (weighted as per table 11 below).

| Score range | Number of entries for analysis |
| :---------- | :------------------------------|
| [45-50)     | 127                            |
| [50-55)     | 143                            |
| **Σ**       | **270**                        | 

*Table 11 Number of entries for analysis in the 'Mid-confidence' subset*

We can see the distribution of correctness of CLIP3 classification combinations in this subset in Table 12:

| First-second                                              | Occurrences in 'High-confidence' subset |
| :-------------------------------------------------------- | :---------------------------------------|
| 0-0 = neither classification is possibly correct          |                                       |
| 0-1 = first-choice is incorrect, second-choice is correct |                                       |
| 1-0 = first-choice is correct, second-choice is incorrect |                                       |
| 1-1 = both classifications are correct (acceptable)       |                                       |
| **Σ**                                                     | **270**                                 | 

*Table 12 The four annotation possibilities for human evaluation of CLIP3 classifications of the 'Mid-confidence' subset (random weighted sample) explained; how many times each one of these combinations occurrs in the dataset*

A noteworthy occurrence in the 'Mid-confidence' subset is the misclassification of an image obviously belonging into 'Botany' as 'Zoology'. The certainty scores in this misclassification are (inherently in this subset) of similar values x(%) ∈ [45-55) with images so obviously belonging into 'Botany' that we would expect to have a first-choice 'Botany' classification value of, say, at least 70 %.

H2 and H3: take the bottom and top 30 results and check what the distribution is across categories -> graphs

worth examining: does correctness increase w certainty? same methodology, but an even wider sample and even distribution

## Conclusions
 


## Future directions
Performing a similar mixed-methods analysis on the prediction results made by CLIP1 and CLIP2 each, and then comparing all three runs could bring valuable insight into which features in particular had the most profound effect on the correspondence of the actual category and the one predicted. This could be in both directions: which specs increase the model's 'correctness' significantly, and are there perhaps any that we had predicted to be effective, but ended up making no to little difference?

For the overview collected for H4a/b, it could be directly applicable to get more information on the patterns in the 0-1 category. Close-reading analysis could provide directions for specification alterations to get the result to 'flip' to 1-0 or 1-1. The correct second-choice classification might be a very useful lead for a relatively low-effort boost (cf. e.g., the 0-0 case).<br>
The evidence collected for H4a/b being true aligns with the low certainty levels given by CLIP3 for the classification instances in the 'Low-confidence' subset. Also in the light of this, we would expect the opposite tendency in the 'High-confidence' subset.

Based on observation from the close-reading analysis, it might be beneficial to redefine the 'Architecture' category. Images ofetn fall between this and other categories (particularly 'Mathematics/Geometry/Astronomy' - building plan v 'generic' geometric drawing, as opposed to a hand-drawn column or building). One option might be to re-name the category and revise its keywords, so that it doesn't include any plans. Another one could be to split it between 'Mathematics/Geometry/Astronomy', 'Botany', 'Miscellaneous/Other', ...).

## Acknowledgements
I'd like to thank Ari Vesalainen for providing me with valuable details on the three model runs.
