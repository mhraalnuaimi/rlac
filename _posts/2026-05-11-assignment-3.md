---
title: "Assignment 3"

categories:
  - assignments
tags:
  - Assignments
  - READY FOR GRADING
---

<h1 style="text-align:center; font-size: 2.5em; margin-top: 20px;">
Exploring Word Vector Models in a Science Fiction Corpus  
By Mhara Al Nuaimi
</h1>

## Introduction
This assignment explores how word vector models represent meaning inside a large science fiction corpus. The corpus contains around one thousand public‑domain science‑fiction texts from Project Gutenberg, mostly from the late nineteenth to mid‑twentieth century. Because of this, the language reflects older writing styles, early scientific vocabulary, and themes common in early science fiction such as exploration, space travel, machines, and unknown worlds. These texts come from a period when science fiction was still defining itself, and the vocabulary reflects both scientific curiosity and imaginative speculation. Because the corpus spans decades, it also contains a mixture of early scientific terminology, pulp‑era adventure language, and the beginnings of more psychological or philosophical science fiction.

The goal of this assignment is to use pretrained Word2Vec models to explore how meaning is learned from context. Instead of reading sentences, the model learns patterns from how words appear together. This allows us to study relationships between words, themes, and concepts across a large body of texts. I used the notebook in Posit Cloud to run clustering, nearest neighbors, multi‑term similarity, vector subtraction, analogies, vector averaging, orthogonal projection, and centroid comparison. Each of these methods reveals a different aspect of how the model organizes meaning.

As Underwood explains in *The Dangers of Distant Reading*, computational tools can reveal patterns that are hard to see through close reading, but they can also flatten nuance. This idea guided my approach. I used the model to explore relationships between words, but I also kept in mind that the model does not understand meaning the way humans do, it only learns from patterns in the text. This tension between pattern and meaning shaped how I interpreted the results. I tried to balance the model’s mathematical associations with my own understanding of science‑fiction themes.

Before running the analysis, I expected the model to show strong connections between words related to space, technology, and exploration. I also expected older science‑fiction vocabulary to appear, since the corpus is from public‑domain texts. I thought words like *ship*, *planet*, *crew*, and *machine* would appear together. I also expected differences between human‑centered and machine‑centered vocabulary, because early science fiction often contrasts humans with robots or aliens. These expectations helped me understand what the model captured—and what it missed.

---

## Corpus Expectations & Background
The texts in this corpus come from a period when science fiction was still developing as a genre. Many authors focused on space travel, scientific discovery, and strange environments. Because of this, I expected the model to show strong clusters around words like *planet*, *ship*, *star*, and *machine*. I also expected older vocabulary that is not common today, especially since the corpus includes texts from the late 1800s and early 1900s. These texts often use formal or archaic language, and they sometimes include invented scientific terms or speculative technologies.

I also expected the model to reflect biases in the corpus. Since the texts are public domain, they mostly come from Western authors. This means the model might reflect older cultural assumptions, limited diversity, and specific views of technology and society. These biases can shape how the model groups words and what associations it considers “close.” For example, the model might associate certain words with gendered or racial stereotypes present in early science fiction.

Thinking about these expectations helped me interpret the results more carefully. When the model returned strange or unexpected words, I remembered that it was trained on older texts with different styles and themes. This context is essential when working with computational models, because the model’s “knowledge” is really just a reflection of the language it was trained on. Understanding the corpus helps prevent over‑interpreting the model’s associations.

---

## Models Used
The notebook includes six pretrained models:

- model_100d_w4  
- model_100d_w6  
- model_100d_w9  
- model_200d_w6  
- model_200d_w10  
- model_300d_w8  

Each model has a different window size and number of dimensions. A smaller window focuses on local context, while a larger window captures broader themes. Higher dimensions capture more detail and allow the model to represent more abstract relationships. Because of this, different models can produce different interpretations of the same word.

I mainly used the **100d_w4** model because it was the simplest and fastest to run. It focuses on tight context, which helped me see direct relationships between words. Later, I compared this model with two others to understand how abstraction changes across models. This comparison helped me see how model architecture affects meaning.

---

## Exploratory Analysis

### Clustering
Instead of including the raw clustering output (which is extremely long and messy), I summarized the clusters into thematic groups. Each cluster represents words that appear in similar narrative contexts.

**Cluster Themes (Summarized Table)**

| Cluster Theme | Representative Words | Interpretation |
|---------------|----------------------|----------------|
| **Time & Duration** | years, days, centuries, moments, seconds | Reflects sci‑fi narratives that track long time spans or sudden events |
| **Nature & Environment** | oaks, conifers, shrub, palmetto, branches | Shows how natural settings appear even in futuristic stories |
| **Sound & Movement** | clang, buzzers, ping, chatter, clatter | Captures action scenes, machinery, and sensory descriptions |
| **Technology & Machinery** | frigate, starships, harbors, masts, observers | Represents space travel, ships, and mechanical environments |
| **Abstract or Rare Terms** | paraparths, sangths, monocycles, Eradrome | Reflects invented sci‑fi vocabulary and unusual terms |

**Analysis:**  
The clusters show how the model groups words that appear in similar contexts. Some clusters focus on time (*years*, *days*, *centuries*), others on nature (*oaks*, *conifers*), and others on movement or machinery (*frigate*, *harbors*, *starships*). This reflects the mixed environments of early science fiction, where natural landscapes and futuristic technology often coexist. The presence of invented or rare words also highlights the imaginative vocabulary of the genre. Clustering reveals how the model organizes the corpus into thematic regions, even when the words themselves are unusual or unfamiliar.

---

### Closest Words to “brain”

**Top 30 Nearest Words (Table)**

| Rank | Word | Rank | Word | Rank | Word |
|------|------|------|------|------|------|
| 1 | brain | 11 | forearm | 21 | skin |
| 2 | body | 12 | keyboard | 22 | face |
| 3 | thoughts | 13 | grasp | 23 | voice |
| 4 | conscience | 14 | tissue | 24 | probe |
| 5 | Lens | 15 | spirit | 25 | exoskeleton |
| 6 | intellect | 16 | mechanism | 26 | knowledge |
| 7 | throat | 17 | tingle | 27 | vibration |
| 8 | adversary | 18 | memories | 28 | pattern |
| 9 | perception | 19 | sensations | 29 | weakness |
| 10 | energies | 20 | fist | 30 | coupling |

**Analysis:**  
The model links *brain* to both mental concepts (*thoughts*, *intellect*, *knowledge*) and physical sensations (*tissue*, *tingle*, *sensations*). This reflects the dual role of the brain in science fiction: both a biological organ and a symbol of intelligence. The mix of sensory and cognitive vocabulary suggests that the model sees the brain as something that connects the physical and mental worlds. This duality appears often in science fiction, where the brain is associated with telepathy, enhanced intelligence, or alien consciousness.

---

### Comparing “brain” Across Three Models

**Nearest Neighbors Comparison Table**

| Model | Top Associations | Interpretation |
|--------|------------------|----------------|
| **100d_w4** | body, thoughts, conscience, throat, perception, tissue, spirit, sensations | Concrete, physical, sensory context |
| **100d_w6** | thoughts, intellect, energies, memories, processes, tingling, nightmare, dream | Mix of physical + cognitive + emotional |
| **300d_w8** | intellect, perception, memories, recollection, knowledge, stimuli, optic | Most abstract, conceptual, cognitive |

**Analysis:**  
The models show a clear progression from concrete (100d_w4) → blended (100d_w6) → abstract (300d_w8). Larger windows and higher dimensions capture broader, more conceptual relationships. This comparison demonstrates how model architecture shapes meaning: the same word can appear more physical or more intellectual depending on the model. The 300‑dimensional model, for example, associates *brain* with *knowledge* and *recollection*, which suggests a more conceptual understanding of cognition. This aligns with the idea that higher‑dimensional models capture more abstract relationships.

---

### Multi‑Term Similarity: *alien + abduction*

**Nearest Words Table**

| Word | Word | Word | Word |
|------|------|------|------|
| stars | sunlight | sky | twilight |
| waters | repose | mist | veils |
| heavens | sea | sands | ripples |
| flames | dimness | grass | mountains |

**Analysis:**  
Instead of fear or violence, the model returns atmospheric, cosmic words. This suggests that “alien abduction” appears in calm or mysterious settings in the corpus. It also shows how the model reflects the tone of the texts rather than cultural assumptions. The model does not “know” that alien abduction is frightening; it only knows how the words appear in the corpus. This is a good example of Underwood’s warning that computational models can flatten emotional nuance.

---

### Multi‑Term Similarity: *atmosphere + oxygen + spaceship + food*

**Nearest Words Table**

| Word | Word | Word | Word |
|------|------|------|------|
| radiance | sky | sunlight | beam |
| radiation | stars | disc | barrage |
| speeds | atmosphere | nebula | ship |
| globe | violet | field | stratosphere |

**Analysis:**  
The combined vector creates a blended “space‑environment” meaning, mixing atmosphere, light, movement, and cosmic imagery. This shows how Word2Vec can merge multiple concepts into a new composite meaning. The presence of words like *nebula*, *stratosphere*, and *ship* suggests that the model understands this combination as something related to space travel and environmental conditions.

---

### Vector Difference: *brain – body*

**Nearest Words Table**

| Word | Word | Word | Word |
|------|------|------|------|
| vibration | quantum | research | experiments |
| subtler | indexing | recording | metallurgical |
| subnucleonic | probe | knowledge | physiological |
| peripheral | accomplished | records | involved |

**Analysis:**  
Subtracting *body* from *brain* highlights scientific and cognitive vocabulary. The model sees the brain as associated with research, knowledge, and analysis. This aligns with science‑fiction themes that connect the brain to intelligence, experimentation, and advanced technology. The presence of words like *quantum* and *subnucleonic* suggests that the model associates the brain with scientific investigation.

---

### Analogy: *alien : barbaric :: human : ?*

**Nearest Words Table**

| Word | Word | Word | Word |
|------|------|------|------|
| human | intelligent | sapient | individual |
| sentient | rational | organic | adult |
| animal | android | extraterrestrial | microscopic |

**Analysis:**  
The model associates *human* with intelligence and awareness, reflecting common sci‑fi contrasts between humans and aliens. The presence of words like *sapient* and *sentient* shows how the model captures conceptual relationships. This analogy also reveals how the model encodes cultural assumptions: humans are associated with intelligence, while aliens are associated with danger or otherness.

---

### Orthogonal Projection: Unique part of “animal” not shared with “human”

**Nearest Words Table**

| Word | Word | Word | Word |
|------|------|------|------|
| elephant | antelope | dog | cat |
| egg | panther | deer | owl |
| herd | crab | eyelid | body |

**Analysis:**  
The model highlights species names and instinctive traits, showing how it distinguishes animals from humans. This reflects the biological focus of the word *animal*. The presence of words like *herd* and *egg* suggests that the model associates animals with reproduction and group behavior.

---

### Centroid Comparison: Space vs. Combat Themes

**Middle‑Ground Words Table**

| Word | Word | Word | Word |
|------|------|------|------|
| cars | roadway | badlands | speeds |
| hell | theatres | kingdoms | profit |
| 1939 | vicarage | hoot | somersaults |

**Analysis:**  
The model sees *space* and *combat* as distinct themes. The middle‑ground words are neutral settings, not strongly tied to either theme. This suggests that the corpus treats space exploration and combat as separate narrative domains. The presence of words like *cars* and *roadway* suggests that the middle ground is more mundane or earth‑based.

---

## Discussion: What the Model Captures and What It Misses
This assignment helped me understand how Word2Vec learns meaning from context. The model captures patterns in how words appear together, but it does not understand definitions or deeper ideas. Underwood warns that distant reading can oversimplify meaning because it focuses on patterns instead of interpretation. I saw this when the model grouped unrelated words together simply because they appeared in similar contexts. For example, the clustering results included invented or rare words alongside common ones, which shows how the model treats all words as equal units in a vector space.

Underwood also explains that computational models can hide important differences between texts. I noticed this when the model treated “alien + abduction” as a calm atmospheric scene instead of something frightening. This shows how the model reflects the language of the corpus rather than the emotional meaning behind the words. The model does not understand fear; it only understands co‑occurrence patterns.

Even with these limits, vector analysis is still useful. It helps reveal patterns that are difficult to see through close reading alone. It also helps compare themes across a large corpus. For example, the centroid comparison showed that space and combat are distinct themes, which might not be obvious from reading individual texts. Vector analysis can also reveal how different models interpret the same word differently, which helps us understand how model architecture affects meaning.

But as Underwood suggests, computational tools should support interpretation, not replace it. The model can show relationships between words, but it cannot explain why authors use certain language or how readers interpret it. Human interpretation is still necessary to understand the deeper meaning behind the patterns.

---

## Conclusion
This assignment showed how word vector models represent meaning in a large science fiction corpus. The model captures patterns in language, but it does not understand meaning the way humans do. Underwood reminds us that distant reading can flatten complexity, and I saw this in my results. The model can show relationships between words, but it cannot explain why authors use certain language or how readers interpret it.

Even so, vector analysis is a helpful method because it reveals hidden patterns and supports broader analysis. It works best when combined with human interpretation, which adds context and meaning that the model cannot provide. This assignment helped me understand both the power and the limitations of computational models, and it showed me how digital tools can complement traditional literary analysis.

---

## Works Cited

Underwood, Ted. *Distant Horizons: Digital Evidence and Literary Change*. University of Chicago Press, 2019.

*Project Gutenberg Science Fiction Corpus*. Course corpus.

*Word Vectors and SciFi Authors Notebook*. Posit Cloud, course materials.

---

**READY FOR GRADING**
