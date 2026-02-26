---
title: "Assignment 1"
date: 2026-02-25 15:34:30 -04:00
categories:
  - assignments
tags:
  - update
  - Post Formats 
---

---


## Introduction: Violence in Harry Potter, & Why Should It Be Studied? 
The Harry Potter series, by J.K Rowling, is built around violence; duels, wars, curses and death shape both the original novels as well as the vast landscape of over a million fanfictions they inspired. Yet while readers often assume fanfiction simply imitates Rowling’s style, authors of fanfiction frequently reimagine tone, pacing, and emotional intensity. This project asks: How does the use of explicit violent language differ between Rowling’s novels and Harry Potter fanfiction, and what does this suggest about how each text portrays conflict?

In order to investigate this question, we analyzed two novels by J.K Rowling (Goblet of Fire and Deathly Hallows), in comparison to three fanfiction texts. Two computational text analysis softwares were used for this analysis: Mhara conducted an analysis in Voyant tools, Amna conducted an analysis in R (Posit Cloud), and a cross-examination of the results from both software was discussed in order to gain a wider, more in-depth understanding. Using these two analysis softwares, we examined patterns in violent vocabulary across approximately one million words of text in total. Rather than relying on selective close reading, we use distant reading to identify broader linguistic patterns that shape how violence is represented. 

## Corpus Selection & Context
Our corpus includes two Rowling novels: Harry Potter and the Goblet of Fire (195,773 words) and Harry Potter and the Deathly Hallows (200,119 words). In addition, the three fanfiction texts were: The Best of Fathers, by Guitérres De La Torre (207, 997 words), Harry Potter: Djinn Awakened, by Invaderdoom/Wishmaster1983 ( 107,151 words), and Dragonheart Caravan, by Witchdragon (240,337 words). 
One reason for the choice of selecting Rowling texts that are later novels in the series is because they contain sustained depictions of war and confrontation, allowing for meaningful comparison with fanfiction that often centers on darker or alternative plotlines. 
Another reason for the choice of these primary texts for our corpus was that they are all relatively similar in word count. It should be noted that although the text by Invaderdoom is significantly lower (~100,00 words), this was relatively close in comparison to other Harry Potter fanfiction from the original corpus pool we were selecting from, provided by Prof.Wrisley. However, we took this into account in our analysis in order to maintain a high validity in the results we are presenting, which is further explained in the ‘Methodology’ section. 

## Methodology: Building a Violence Dictionary in R
	
[Figure 1](assets/images/figure1.png)

**Figure 1. Violence dictionary for analysis in R (124 terms)**
To systematically measure violent action language, we constructed a custom ‘violence dictionary’ in R, shown in Figure 1. This violence dictionary included terms such as “attack”, “kill”, “curse”, “blood”, “wound”, “fight”, and magical combat terms like “Avada”, “Crucio”, and “sectumsempra”. The violence dictionary contains 124 words in total; enough to gauge a wide scope of violent terminology, but not so extensive that it introduces excessive noise or overgeneralizes non-violent language as violent. In some cases, multiple variations of the same violence-related word are included, such as “attack, “attacked”, “attacking”, to account for different grammatical forms and to ensure that our dictionary captures violence-related language regardless of tense or usage. 
After constructing the dictionary, we applied computational normalization to ensure fair comparison across texts of different lengths. For instance, in the heatmap produced in R (Figure 2), violence is measured as the mean frequency of dictionary terms per 10,000 words rather than across the entire novel. This step prevents longer fanfiction texts from appearing more violent simply because they contain more words overall. In other words, normalization allows us to compare texts proportionally rather than absolutely.
By defining this lexicon in advance, we created a reproducible method for identifying patterns across texts. 

Findings from R: Heatmap Analysis 
 
[Figure 2](assets/images/figure2.png)

**Figure 2. Heatmap of 15 terms from violence dictionary across the 2 Rowling and 3 Fanfiction Texts (per 10,000 words)**
The heatmap in Figure 2 reveals striking differences in violent vocabulary distribution. In Deathly Hallows, the word “death” appears at a dramatically higher rate (15.4 occurrences per 10,000 words) compared to the fanfiction texts.

Similarly, “kill” and "killed” occur more frequently in Rowling’s later novels than in most fanfiction works.
However, fanfiction texts display higher relative frequencies of bodily harm terms such as “hurt”, “pain”, and “wound”. This suggests that while Rowling’s novels emphasize mortality and large-scale war, fanfiction often focuses on the physical and emotional experience of injury. In other words, Rowling’s violence tends to be narratively monumental, whereas fanfiction violence appears more intimate and embodied.

Findings from R: Word Clouds 

[Figure 3](assets/images/figure3.png)

**Figure 3. Word clouds displaying the normalized frequency of violence-dictionary terms in selected texts. (Word size reflects mean occurrences per 10,000 words, with larger words indicating higher relative frequency.)**

[Figure 4](assets/images/figure4.png)

**Figure 4. Word clouds comparing the relative frequency of violence-dictionary terms in fanfiction texts and Rowling’s original texts.**

Color intensity (blue to red gradient) represents relative prominence within each corpus. (Word size reflects normalized frequency,mean occurrences per 10,000 words, with larger words indicating higher frequency.) 

The word clouds in Figure 3 and Figure 4 further illustrate differences in emphasis. 
In both Rowling novels, “Voldemort” and “death” dominate the visual field, reinforcing the centrality of war and existential stakes. The clustering suggests a narrative structured around a singular antagonist and ultimate confrontation.
However, a key difference is that fanfiction word clouds distribute violent terms more widely across actions such as “hurt”, “attack”, “fight”, and “weapon”. This broader lexical range implies a more continuous presence of action rather than violence reserved for climactic events. Fanfiction appears to normalize combat as part of ongoing narrative texture.
Findings from Voyant Tools: Trends Graph
Voyant allowed us to visualize how violent words behave across the entire corpus and to look at how these words appear in actual sentences. Instead of focusing on normalized counts like in R, Voyant helped us see how violent language rises and falls throughout each text and how it is used in context.

<iframe style='width: 600px; height: 344px;' src='https://voyant-tools.org/tool/Trends/?view=Trends&query=hate&query=kill&query=killing&query=blood&query=scream&query=shout&query=hurt&query=hurting&query=wound&query=shouted&query=shouting&query=curse&query=killed&query=attack&query=attacked&query=fought&query=cursed&query=fight&chartType=line&corpus=35f7c6a1aba63b64ab58e37088c3034d'></iframe>

**Figure 5. Voyant Tools Trends graph showing the frequency of selected violent words across the full timeline of each text.**

Fanfiction maintains consistently higher levels of violent vocabulary, while Rowling’s novels show sharp spikes during major conflict scenes.

The first visualization we examined was the Trends graph. We entered a set of violent words such as “kill”, “attack”, “blood”, “curse”, “hurt”, and “fight” into the tool. The graph immediately showed a clear separation between Rowling’s novels and the fanfiction texts. The fanfiction lines stayed consistently higher across the entire timeline, while the Rowling lines only rose during certain sections. For example, Goblet of Fire showed a noticeable increase in violent vocabulary in some parts of the novel, which likely corresponds to major conflict scenes, but outside of those moments the frequency dropped sharply. In contrast, the fanfiction texts rarely dipped at all. This suggests that fanfiction treats violence as a steady part of the narrative, while Rowling uses it more selectively and ties it to specific emotional or plot‑driven events.

Findings from Voyant Tools: Cirrus Word Cloud

[Figure 6](assets/images/figure6.png)

**Figure 6. Voyant Cirrus word cloud showing the most frequent words across the corpus.**

Character names and dialogue verbs dominate, showing that violent vocabulary is not the most common language overall.

 The Cirrus word cloud in Voyant added another layer to this comparison. Even though our project focused on violence, the word cloud did not show violent words as the most frequent ones. Instead, it highlighted names like Harry, Draco, and Hermione, along with common verbs such as said and asked. This shows that violent language is not the dominant vocabulary in either Rowling or the fanfiction texts. It only becomes visible when we isolate it through targeted searches. This shows how basic visualizations can hide deeper patterns, because certain kinds of language only become visible when we use more focused or computational tools. If we relied only on the word cloud, we might assume violence was not a major theme at all. But the Trends graph revealed that violent language plays a much larger role once it is isolated and examined directly.

**Findings from Voyant Tools: Contexts tool**

[Figure 7](assets/images/figure7.png)

**Figure 7. Voyant Contexts (concordance) view for the word kill. Rowling’s examples show hesitation or moral conflict, while fanfiction examples show more direct and assertive uses of violent language.**

The Contexts tool in Voyant helped us understand how violent words were used in actual sentences. When we searched for the word kill, the difference in tone between Rowling and the fanfiction texts became very clear. In Rowling’s novels, the examples often showed hesitation, fear, or guilt. One line read something like “He didn’t want to kill anyone,” and another described a character insisting that killing was wrong. These examples show that Rowling frames violence as something serious and emotionally heavy. In the fanfiction texts, the tone was much more direct. Characters said things like “I’m going to kill you” or “I decided to kill him,” which sounded more confident and intense. This suggests that fanfiction uses violence as a way to show power or raise the stakes in a scene. This difference reflects what Kestemont and Herman describe as the “dangers of oversimplification in which scholars caricaturize rather than characterize reading modes,” showing how computational approaches can flatten the nuance behind how violence is expressed (Kestemont and Herman). The contrast between the two styles shows how different authors approach the same universe with different goals.

## Comparison of Findings from Posit Cloud and Voyant Tools
When we compared the Voyant findings with the Posit Cloud heatmap, the results were largely supportive of one another. The heatmap showed that fanfiction had higher frequencies across a wider range of violent words, while Rowling’s novels only had high numbers for a few terms like death or dead. This matched the Voyant Trends graph, which showed fanfiction maintaining a steady level of violent vocabulary throughout the text. Using both tools together made the results feel more reliable because they showed the same pattern in different ways. Voyant highlighted the trends and the context around the words, while Posit Cloud provided the exact counts and a clearer visual comparison.

## Limitations
While these tools helped reveal important patterns, it is also important to acknowledge the limitations of this approach. Focusing only on selected violent terms risks oversimplifying how conflict appears in the texts. Violence can be described metaphorically or indirectly, and those moments would not be captured by our dictionary. There are also synonyms or related actions that we did not include, which means some forms of violence may be undercounted. Pechenick, Danforth, and Dodds warn that large‑scale corpora can mislead interpretation because “the Google Books corpus suffers from a number of limitations which make it an obscure mask of cultural popularity,” and that computational methods often “boil down to an advanced form of ‘word counting’ that might beat a human in processing scope but rarely in hermeneutic quality.” (Pechenick et al.) A spike in violent words does not automatically mean a scene is more important, and a low count does not mean a text is peaceful. These tools help identify patterns, but they do not replace the nuance of close reading.

## Conclusion
Taken together, the results from Voyant Tools and Posit Cloud reveal two distinct approaches to conflict in the Harry Potter universe. Rowling uses violence as a moral and emotional moment. Characters think about it, hesitate, or feel guilty when they are faced with it. Fanfiction uses violence as a stylistic choice. It is part of the action and part of how characters express themselves. Neither approach is better, but they show how fans reshape the original story to explore new ideas or emphasize different themes. Using both tools together made it possible to see these differences clearly and understand how each type of text handles conflict in its own way.

## Contribution Statement
Both group members contributed equally to the project. Amna conducted the R/Posit Cloud analysis, created the violence dictionary, and produced the heatmap and word cloud visualizations. Mhara conducted the Voyant Tools analysis, including the Trends graph, Cirrus word cloud, and Contexts tool interpretation. Both members collaborated on selecting the corpus, interpreting the results, writing the essay, and revising the final draft. 

## Works Cited
Kestemont, Mike, and Luc Herman. “Can Machines Read (Literature)?” Umanistica Digitale, no. 5, 2019, pp. 1–14.

Pechenick, Eitan Adam, Christopher M. Danforth, and Peter Sheridan Dodds. “Characterizing the Google Books Corpus: Strong Limits to Inferences of Socio‑Cultural and Linguistic Evolution.” PLOS ONE, vol. 10, no. 10, 2015, e0137041.

READY FOR GRADING
