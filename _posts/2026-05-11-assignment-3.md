---
title: "Assignment 3"
date: 2026-05-12 11:59:00 -04:00
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
This assignment explores how word vector models represent meaning inside a large science fiction corpus. The corpus contains around one thousand public domain science fiction texts from Project Gutenberg. These texts come from different decades, mostly from the late nineteenth century to the mid twentieth century. Because of this, the language reflects older writing styles, early scientific vocabulary, and themes that were common in early science fiction such as exploration, space travel, machines, and unknown worlds.

The goal of this assignment is to use pretrained Word2Vec models to explore how meaning is learned from context. Instead of reading sentences, the model learns patterns from how words appear together. This allows us to study relationships between words, themes, and concepts. I used the notebook in posit.cloud to run clustering, nearest neighbors, multi-term similarity, vector subtraction, analogies, vector averaging, orthogonal projection, and centroid comparison.

As Underwood explains in *The Dangers of Distant Reading*, computational tools can reveal patterns that are hard to see through close reading, but they can also flatten nuance. This idea guided my approach. I used the model to explore relationships between words, but I also kept in mind that the model does not understand meaning the way humans do. It only learns from patterns in the text.

Before running the analysis, I expected the model to show strong connections between words related to space, technology, and exploration. I also expected older science fiction vocabulary to appear, since the corpus is from public domain texts. I thought words like *ship*, *planet*, *crew*, and *machine* would appear together. I also expected differences between human-centered and machine-centered vocabulary, because early science fiction often contrasts humans with robots or aliens.

This assignment helped me understand how computational models learn meaning from context and how they reflect the themes of the corpus.

---

## Corpus Expectations & Background
The texts in this corpus come from a period when science fiction was still developing as a genre. Many authors focused on space travel, scientific discovery, and strange environments. Because of this, I expected the model to show strong clusters around words like *planet*, *ship*, *star*, and *machine*. I also expected older vocabulary that is not common today.

I also expected the model to reflect biases in the corpus. Since the texts are public domain, they mostly come from Western authors. This means the model might reflect older cultural assumptions, limited diversity, and specific views of technology and society.

I also expected differences between early and later science fiction. Early texts often focus on exploration and discovery, while later ones include more complex themes like dystopia, psychology, and advanced technology. Because the corpus mixes all of these, I expected the model to blend them together.

Thinking about these expectations helped me understand the results better. When the model returned strange or unexpected words, I remembered that it was trained on older texts with different styles and themes.

---

## Models Used
The notebook includes six pretrained models:

- model_100d_w4  
- model_100d_w6  
- model_100d_w9  
- model_200d_w6  
- model_200d_w10  
- model_300d_w8  

Each model has a different window size and number of dimensions. A smaller window focuses on local context, while a larger window captures broader themes. Higher dimensions capture more detail.

I mainly used the **100d_w4** model because it was the simplest and fastest to run. It focuses on tight context, which helped me see direct relationships between words. If I had more time, I would compare the same queries across all models to see how stable the results are.

---

## Exploratory Analysis

### 1. Clustering
**Code Output:**  
### Clustering Results

```
[,1]           [,2]         [,3]         [,4]            [,5]      
 [1,] "paraparths"   "oaks"       "rung"       "tweak"         "WINDOW"  
 [2,] "microsecond"  "alfalfa"    "clang"      "Mavrocordatus" "TWELVE"  
 [3,] "decade"       "covert"     "buzzers"    "Quiggs"        "tootle"  
 [4,] "Recapture"    "branches"   "keened"     "Unnecessary"   "CAPTURED"
 [5,] "moments"      "decaying"   "ping"       "Trains"        "PROBLEM" 
 [6,] "sangths"      "eishn"      "thud"       "Arthurs"       "SHADOWS" 
 [7,] "Moments"      "thorny"     "chatter"    "foxholes"      "MURDERER"
 [8,] "Months"       "conifers"   "cymbals"    "Eradrome"      "PLAN"    
 [9,] "bombings"     "shrub"      "sonorous"   "gaff"          "SATAN"   
[10,] "“Years"       "palmetto"   "clangour"   "pigeonhole"    "CAME"    
[11,] "days"         "cottonwood" "belling"    "Stress"        "DAY"     
[12,] "socialisms"   "chinked"    "clatter"    "Kulichenko"    "LION"    
[13,] "vociferously" "poplars"    "soundless"  "Sherdlap"      "TERRA"   
[14,] "Centuries"    "thickest"   "clashing"   "“Yew"          "LARGER"  
[15,] "seconds"      "dense"      "monocycles" "“Having"       "XLVIII"  
      [,6]              [,7]             [,8]         [,9]         
 [1,] "shadings"        "Fifties"        "198"        "consignment"
 [2,] "forecasts"       "Broad"          "63"         "forkful"    
 [3,] "qualifications"  "northbound"     "35"         "noodles"    
 [4,] "executions"      "Edgware"        "1639"       "mash"       
 [5,] "densities"       "Piccadilly"     "Nuremberg"  "peppermint" 
 [6,] "sonnets"         "Beckenham"      "Ægatian"    "incense"    
 [7,] "documents"       "Goudhurst"      "131"        "potash"     
 [8,] "impressions"     "Frith"          "173"        "lozenges"   
 [9,] "errors"          "Enterprize"     "Saggiatore" "logged"     
[10,] "adornments"      "Ringwood"       "960"        "violets"    
[11,] "exceptions"      "Urshot"         "608"        "hamburgers" 
[12,] "nightmares"      "Hendon"         "602"        "acrid"      
[13,] "impossibilities" "Arcade"         "404"        "eats"       
[14,] "interludes"      "tranquillities" "Pensions"   "tanker"     
[15,] "erasures"        "Esher"          "633"        "tacky"      
      [,10]         
 [1,] "Federations" 
 [2,] "galaxies"    
 [3,] "frigate"     
 [4,] "harbors"     
 [5,] "wagons"      
 [6,] "masts"       
 [7,] "skeeterboats"
 [8,] "cogged"      
 [9,] "paddlers"    
[10,] "starships"   
[11,] "figures"     
[12,] "observers"   
[13,] "pterosaurs"  
[14,] "cradles"     
[15,] "ponies"
```


**Analysis:**  
The clustering results show groups of words that appear in similar contexts. Some clusters focus on time words like *years*, *days*, and *centuries*. Others include nature words like *oaks*, *conifers*, and *shrub*. There are also clusters with movement or object words like *frigate*, *harbors*, and *starships*.

This shows that the model organizes words based on how they appear in stories. The clusters are not perfect categories, but they show how the model picks up on patterns in the text. The mix of literal and descriptive words in the same cluster shows that the model blends meanings when words appear in similar narrative settings.

This also reflects the science fiction corpus. Many stories mix natural environments with futuristic settings. The model captures this blend. It also shows how the model groups words that appear in similar scenes, even if they are not related in meaning. This is one of the limits that Underwood warns about. The model sees patterns, but it does not understand why the words appear together.

---

### 2. Closest Words to “brain”
**Code Output:**  
Looking for: brain
Top 30 closest words:
 [1] "brain"       "body"        "thoughts"    "conscience"  "Lens"       
 [6] "intellect"   "throat"      "adversary"   "perception"  "energies"   
[11] "forearm"     "keyboard"    "grasp"       "tissue"      "spirit"     
[16] "mechanism"   "tingle"      "memories"    "sensations"  "fist"       
[21] "skin"        "face"        "voice"       "probe"       "exoskeleton"
[26] "knowledge"   "vibration"   "pattern"     "weakness"    "coupling"


**Analysis:**  
The model connects *brain* with both thinking and physical sensations. Words like *thoughts*, *intellect*, and *knowledge* show the mental side. Words like *tissue*, *sensations*, and *tingle* show the physical side. This means the model understands the brain as something that links the mind and the body.

This result matches my expectations. Science fiction often connects the brain to both intelligence and physical experience. The model reflects this dual role.

---

### 3. Multi-Term Similarity: alien + abduction
**Code Output:**  
Closest to: alien + abduction
 [1] "stars"     "sunlight"  "sky"       "twilight"  "waters"    "repose"   
 [7] "mist"      "veils"     "heavens"   "sea"       "seas"      "downpour" 
[13] "puffs"     "sands"     "ripples"   "Flames"    "dimness"   "grass"    
[19] "mountains" "winter"


**Analysis:**  
I expected words related to fear or danger, but the model returned atmospheric words like *stars*, *mist*, and *twilight*. This suggests that the model connects alien abduction with mysterious or cosmic settings rather than violence.

This result surprised me. It shows that the model learns meaning from context, not from assumptions.

---

### 4. Multi-Term Similarity: atmosphere + oxygen + spaceship + food
**Code Output:**  
Closest to: atmosphere + oxygen + spaceship + food
 [1] "radiance"     "sky"          "sunlight"     "beam"        
 [5] "distance"     "radiation"    "stars"        "disc"        
 [9] "barrage"      "speeds"       "atmosphere"   "nebula"      
[13] "ship"         "globe"        "violet"       "field"       
[17] "stratosphere" "dot"          "curve"        "vibration"


**Analysis:**  
This combination creates a blended idea that feels like a space environment. Words like *nebula*, *stars*, and *stratosphere* show the space theme. Words like *ship* and *speeds* show movement and technology.

This result shows how Word2Vec can mix several ideas into one new meaning.

---

### 5. Vector Difference: brain – body
**Code Output:**  
Words similar to the difference ( brain  -  body ):
 [1] "Vibration"     "brain"         "quantum"       "research"     
 [5] "experiments"   "newscasters"   "subtler"       "indexing"     
 [9] "recording"     "metallurgical" "involved"      "phono"        
[13] "read"          "subnucleonic"  "probe"         "knowledge"    
[17] "physiological" "peripheral"    "accomplished"  "records"


**Analysis:**  
Subtracting *body* from *brain* highlights what the model sees as unique to the brain. The closest words relate to science, thinking, and learning. Words like *research*, *experiments*, and *knowledge* show this.

This result shows that the model understands the brain as something connected to analysis and information.

---

### 6. Analogy: alien is to barbaric as human is to ?
**Code Output:**  
Alien analogy: alien is to barbaric as human is to ?
 [1] "human"            "alien"            "intelligent"     
 [4] "sapient"          "individual"       "Eddorian"        
 [7] "animal"           "adult"            "organic"         
[10] "sentient"         "auditory"         "external"        
[13] "Human"            "Arisian"          "nonsapient"      
[16] "android"          "finite"           "extraterrestrial"
[19] "microscopic"      "rational"


**Analysis:**  
The model suggests that if *alien* relates to *barbaric*, then *human* relates to intelligence and awareness. Words like *sapient*, *sentient*, and *rational* show this.

This analogy reflects how science fiction often contrasts humans with aliens.

---

### 7. Orthogonal Projection: Unique part of “animal” not shared with “human”
**Code Output:**  
Words representing the unique part of ' animal ' not shared with ' human ':
 [1] "animal"   "elephant" "antelope" "dog"      "cat"      "egg"     
 [7] "panther"  "deer"     "owl"      "armful"   "body"     "banth"   
[13] "herd"     "crab"     "eyelid"



**Analysis:**  
The model highlights animals, species names, and instinctive traits. Words like *herd*, *egg*, and *panther* show that the model sees animals through their physical and natural qualities.

---

### 8. Centroid Comparison: Space vs. Combat Themes
**Code Output:**  
Distance between 'space' theme and 'combat' theme: 7.235
Words equidistant from both themes (thematic middle ground):
 [1] "1939"        "cars"        "roadway"     "badlands"    "speeds"     
 [6] "hell"        "Series"      "vicarage"    "helans"      "kingdoms"   
[11] "Ole"         "theatres"    "hoot"        "somersaults" "profit"


**Analysis:**  
The distance shows that space and combat are not close in the model. The middle words like *cars*, *roadway*, and *theatres* are neutral settings. They do not belong strongly to either theme.

This means the model sees space and combat as separate ideas, but they can still connect through shared environments.

---

## Discussion: What the Model Captures and What It Misses
This assignment helped me understand how Word2Vec learns meaning from context. The model captures patterns in how words appear together, but it does not understand definitions or deeper ideas. Underwood warns that distant reading can oversimplify meaning because it focuses on patterns instead of interpretation. I saw this when the model grouped unrelated words together simply because they appeared in similar contexts.

Underwood also explains that computational models can hide important differences between texts. I noticed this when the model treated “alien + abduction” as a calm atmospheric scene instead of something frightening. This shows how the model reflects the language of the corpus rather than the emotional meaning behind the words.

Even with these limits, vector analysis is still useful. It helps reveal patterns that are difficult to see through close reading alone. It also helps compare themes across a large corpus. But as Underwood suggests, computational tools should support interpretation, not replace it.

---

## Conclusion
This assignment showed how word vector models represent meaning in a large science fiction corpus. The model captures patterns in language, but it does not understand meaning the way humans do. Underwood reminds us that distant reading can flatten complexity, and I saw this in my results. The model can show relationships between words, but it cannot explain why authors use certain language or how readers interpret it.

Even so, vector analysis is a helpful method because it reveals hidden patterns and supports broader analysis. It works best when combined with human interpretation, which adds context and meaning that the model cannot provide.

---

## Works Cited

Underwood, Ted. *Distant Horizons: Digital Evidence and Literary Change*. University of Chicago Press, 2019.

*Project Gutenberg Science Fiction Corpus*. Course corpus.

*Word Vectors and SciFi Authors Notebook*. Posit Cloud, course materials.

Mikolov, Tomas, et al. “Efficient Estimation of Word Representations in Vector Space.” arXiv:1301.3781, 2013.

**word2vec** R package. CRAN.

**READY FOR GRADING**


