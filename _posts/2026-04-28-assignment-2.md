---
title: "A2: Two Tools, One Corpus"
authors: "Shama & Mhara"
layout: single
date: 2026-04-24

categories:
  - posts
  - assignments
tags:
  - Stylo
  - TF-IDF
  - Assignment 

---
Our assignment was essentially a question dressed up as a project: if you hand the same pile of books to two different computational tools, do they see the same library, or two different ones? The pile in question is a small but surprisingly varied corpus of 18 science fiction and speculative fiction texts pulled from Project Gutenberg, and the two tools are a matched pair that weight the same words very differently.

- **Stylo** (an R package) leans on the most frequent words in a text, the quiet scaffolding of *the*, *and*, *of*, *was*, and uses the rates at which writers use those words to work out who wrote what.
- **TF-IDF** works on the same word pool but reweights it, downweighting words that appear across many texts and spotlighting whatever vocabulary is *peculiar* to each one.

The cliche is that Stylo catches authorship and TF-IDF catches topic. We wanted to see whether that holds up on a corpus of pulp space opera, Martian princesses, and, for some reason, a non fiction essay collection by H.G. Wells. Hanging over all of it is Ted Underwood's warning in "The Risks of Distant Reading" that a model is not a tool you plug in, it is "a new way of representing and interpreting the world" (Underwood 145). If he is right, Stylo and TF-IDF should disagree in ways that matter.

## A quick note on the corpus

The 18 texts lean heavily into American pulp sci fi from the 1940s through the early 1960s, with one older British voice for contrast. All author notes below are drawn from Wikipedia, and summed up into bullet points with the help of an LLM (Claude)

**Leigh Brackett** (3 novels, including *Enchantress of Venus* and *The Black Amazon of Mars*)

- Published 17 stories in *Planet Stories*, the magazine she is most identified with alongside Ray Bradbury
- Her planetary romances lean on a recurring decadent, dying Mars and a wet, jungle Venus
- A central theme is the clash of planetary civilisations, often used as a critique of colonialism
- Also co wrote the screenplay for *The Empire Strikes Back*

**Philip K. Dick** (3 stories, all from 1953)

- Born 1928, died 1982; began publishing science fiction in 1952 at age 23
- Wrote more than 40 novels and around 121 short stories over his career
- Known for alternate realities, altered states, authoritarian governments, and slippery questions of identity
- Later adapted into *Blade Runner*, *Total Recall*, and *Minority Report*

**Andre Norton** (3 novels)

- Real name Alice Mary Norton; "Andre" was a career decision in a male dominated genre
- Published more than 300 titles across 70 years of writing
- Named an SFWA Grand Master in 1984 and won the World Fantasy Lifetime Achievement Award in 1998
- The Andre Norton Award for YA science fiction and fantasy was created in her honour in 2005

**H.G. Wells** (3 works)

- English, 1866 to 1946, sometimes called the "father of science fiction"
- Produced *The Time Machine*, *Moreau*, *War of the Worlds*, and others in a famous six year burst from 1895 to 1901
- Critic John Clute calls him "the most important writer the genre has yet seen"
- Also wrote widely in non fiction: social commentary, politics, popular science, biography, which is the tradition *The Salvaging of Civilization* sits in rather than his fiction

**Marion Zimmer Bradley** (3 works)

- Started writing at 17; holds a BA from Hardin Simmons University
- First Darkover novel, *The Planet Savers*, published in 1958 in *Amazing Stories*
- Co founded the Society for Creative Anachronism in 1966
- Often credited with bringing a female perspective into sword and sorcery fiction at a time when the genre ignored one

**Henry Kuttner** (3 stories, including *The Black Kiss*, co written with Robert Bloch)

- Born 1915, died 1958; first sale was "The Graveyard Rats" to *Weird Tales* in 1936
- Married C.L. Moore in 1940, and most of his 1940 to 1958 output was co written with her
- Shared multiple pseudonyms with Moore, most famously "Lewis Padgett"
- Ray Bradbury called him a "neglected master" and a "pomegranate writer, popping with seeds, full of ideas"

On paper the corpus spans 65 years. In practice almost everything clusters into a mid century American magazine band, with Wells sitting on the edge like a Victorian uncle at a pulp convention.

## Tool 1: Stylometry with Stylo

### What it does

Stylo's premise is a little unnerving: authorship shows up best not in a text's flashy vocabulary but in its plumbing. Writers are weirdly consistent in how often they use tiny connective words like *the*, *and*, *of*, *was*, *that*, *which*, and Stylo does basically nothing but count those rates. It runs a distance metric across the corpus (we used **Classic Delta**, Stylo's default) and draws either a **Cluster Analysis (CA)** dendrogram or a **Bootstrap Consensus Tree (BCT)** that averages multiple runs. We ran CA at 100, 300, and 500 most frequent words (MFW), plus a BCT spanning 100 to 500.

### Results

At **100 MFW**, the tree is almost suspiciously clean:

- Dick's three stories cluster together at the top.
- Norton's three novels cluster together at the bottom.
- Wells's two fiction novels pair off in their own branch.
- Brackett and Kuttner tangle in the middle.
- Zimmer Bradley's tiny *Jackie Sees a Star* (only 10KB) floats near Dick, separated from her own novels.
- *The Salvaging of Civilization* falls off the bottom, exiled on its own branch.

<figure>
  <img src="{{ '/assets/images/stylo-ca-100mfw.jpg' | relative_url }}"
       alt="Stylo CA at 100 MFW">
  <figcaption>Figure 1: Stylo CA at 100 MFW</figcaption>
</figure>

Push the MFW count up, though, and things loosen. At **300** and especially **500 MFW**, Brackett's *The Blue Behemoth* drifts off to sit next to Kuttner's *The Ego Machine*, which itself keeps creeping towards Zimmer Bradley's novels, as if Kuttner were quietly trying to colonise half the tree. Dick and Norton, by contrast, held their internal shape perfectly, each cluster stayed as tightly packed as it was at 100 MFW, but the dendrogram rendered them in flipped positions, with Norton at the top where Dick had been and Dick at the bottom where Norton had been. They did not break, they just traded seats, which in a dendrogram is partly a rendering choice rather than a real change in stylistic distance.

<figure>
  <img src="{{ '/assets/images/stylo-ca-500mfw.jpg' | relative_url }}"
       alt="Stylo CA at 500 MFW">
  <figcaption>Figure 2: Stylo CA at 500 MFW</figcaption>
</figure>

The BCT (below) smooths those shifts into one circular picture. Dick and Norton still read as stable islands, Brackett and Kuttner share a neighbourhood rather than occupying separate ones, Wells's novels drift towards *The Black Kiss*, and *The Salvaging of Civilization*, mysterioulsy, ends up near Norton.

<figure>
  <img src="{{ '/assets/images/stylo-bct-delta.jpg' | relative_url }}"
       alt="Stylo BCT, 100 to 500 MFW">
  <figcaption>Figure 3: Stylo BCT, 100 to 500 MFW</figcaption>
</figure>

### Analysis

Three things stood out.

**1. Stylo mostly does what the textbook promises:** Dick, Norton, and the Wells fiction novels clustered neatly by author, with the cleanest signal at lower MFW where function words dominate. The small rhythms of *the* and *and* really are a better fingerprint than topic vocabulary. Dick and Norton also flipped positions in the tree as MFW grew but kept their internal shape from 100 through 500 MFW, this means that the identified author pattern is consistent and not just a coincidence caused by the specific settings used in the analysis..

**2. The method is not magic:** Length and genre leak into the results. *Jackie Sees a Star* is too short for reliable frequency counts, so it drifts with the noise. *The Salvaging of Civilization* is non fiction, so it refuses to cluster with fictional narratives.Stylo is not malfunctioning. Both results show that a dendrogram does not actually read texts; it analyzes them by counting common words like *the* and *and.*


**3. The Brackett and Kuttner blur is the most interesting finding:** Both wrote for pulp magazines in overlapping decades, Brackett mostly in *Planet Stories* and Kuttner in *Weird Tales*, and both share a Bradbury connection. If Stylo were a perfect authorship detector, it would split them. The fact that it cannot is the better answer: a shared commercial tradition can produce a shared stylistic footprint with the authors, which is something we could not have claimed from reading alone.

By the end of the Stylo pass, we have a reasonable map of **who writes like whom**. The follow up question, which we take to TF-IDF next, is whether that map of **style** has anything at all to do with a map of **content**. The suspicion and assumpiton going in, is that it will not.

## Tool 2: TF-IDF

### What it does

TF-IDF looks at the texts in a different way from Stylo. It works on the same word pool but reweights it, so words that appear across many texts get pushed down and words that stand out in any one text get lifted up. This means it cares more about what the books are about. We examined the TF-IDF results at 100, 500, and 2000 most frequent words, using the values given to us, to observe how the structure of the corpus changed as the vocabulary pool grew.

### The Results

At 100 MFW, the groups were loose but still clear. *The Salvaging of Civilization* sat far away from everyone else in the upper right corner, while Wells's two fiction novels stayed mixed in with the pulp cluster rather than off on their own. Dick formed a small tight group, and Brackett and Kuttner overlapped because they use a lot of the same adventure words. Zimmer Bradley moved around a bit, mostly because *Jackie Sees a Star* is very short.

<figure>
  <img src="{{ '/assets/images/MFW100.jpg' | relative_url }}"
       alt="Stylo BCT, 100 to 500 MFW">
  <figcaption>Figure 4: TF-IDF, MFW: 100 </figcaption>
</figure>


At 500 MFW, the picture became sharper. Dick stayed close together, Brackett and Zimmer Bradley moved toward each other, and Kuttner's *The Ego Machine* shifted toward Dick, which suggests it uses more technical words. Norton stayed steady but moved a little toward Wells because they share some general words about society and the future.

<figure>
  <img src="{{ '/assets/images/MFW500.jpg' | relative_url }}"
       alt="Stylo BCT, 100 to 500 MFW">
  <figcaption>Figure 5: TF-IDF, MFW: 500 </figcaption>
</figure>


At 2000 MFW, the content patterns became very strong. Brackett, Zimmer Bradley, Norton, and part of Kuttner formed one big group that looks like a shared genre space. Dick stayed in his own small group, and Wells stayed far away from everyone.

<figure>
  <img src="{{ '/assets/images/MFW2000.jpg' | relative_url }}"
       alt="Stylo BCT, 100 to 500 MFW">
  <figcaption>Figure 6: TF-IDF, MFW: 2000 </figcaption>
</figure>


TF-IDF ended up showing a map based on topics and themes instead of writing style.

### Analysis

Two things stood out when we looked at the three plots together as before.

**1. TF-IDF finds the same outliers as Stylo, but for different reasons:** *Jackie Sees a Star* and *The Salvaging of Civilization* sit in the far corners of every plot we made, no matter the MFW setting. Stylo pushed them out because of length and genre. TF-IDF pushes them out because of vocabulary, which is a different reason. When both tools agree that a text does not belong, that is a stronger result than either tool on its own.

**2. The Wells fiction novels are the one place both tools agree in a positive way:** *The Island of Doctor Moreau* and *The War of the Worlds* sit together on the right side in every plot. Stylo grouped them based on small word patterns. TF-IDF groups them based on the probable older science vocabulary they share. When two very different tools agree on a real cluster, not just an outlier, it is probably a strong finding.

## Bringing The Two 

Putting the Stylo and TF-IDF results together shows that the two tools are not looking at the same thing. Stylo builds a picture based on writing habits, while TF-IDF builds a picture based on topics. Because of this, the two maps look very different. Stylo shows Dick and Norton as very steady writers, Brackett and Kuttner as a blended pair, and Wells as someone who sits on the edge. TF-IDF shows something else. It groups Brackett, Zimmer Bradley, Norton, and part of Kuttner together because they all write similar adventure stories. It keeps Dick in his own space because his stories use a lot of Cold War and technology words. It pushes Wells far away because his language comes from a different time.

The most interesting part is that both tools mix Brackett and Kuttner, but for different reasons. Stylo mixes them because they write with similar patterns. TF-IDF mixes them because they use similar story words. This shows how much their shared magazine world shaped both their style and their content.

The tools disagree the most on Zimmer Bradley and Wells. Stylo treats Zimmer Bradley as unstable because of text length, while TF-IDF places her with Brackett. Stylo keeps Wells near the fiction cluster, while TF-IDF pushes him far out. These differences support Ted Underwood's idea that models do not simply read texts. They create new ways of seeing them.

## Conclusion

This project showed us that Stylo and TF-IDF do not read the corpus in the same way, and this helped us understand the readings more clearly. Stylo focused on small writing habits, while TF-IDF focused on topic words, so each tool created a different picture of the same books. This was only readable once we did the background research on the corpus: knowing that Brackett and Kuttner shared a pulp world, that Salvaging of Civilization is non fiction, and that Jackie Sees a Star is too short to give a stable signal. Our results proved this. Stylo made the corpus look like a set of writing styles, while TF-IDF made it look like a set of themes. The tools agreed on some things, like Dick and Norton being steady writers, but they disagreed on others, like Zimmer Bradley and Wells. This showed how much the method changes the outcome. Adam Crymble makes a similar point in "Building the Invisible College," where he highlights Ewa Swenson's argument that the real skill is not running a tool but knowing "how to recognize problems, identify and characterize them, understand their nature. And then to determine which tool may be appropriate for the problem" (Crymble 119). Comparing Stylo and TF-IDF side by side on the same corpus was a small version of exactly that. The project also supported the class idea that distant reading is not about finding one correct answer. It is about learning how each method highlights some parts of the text and hides others. In the end, the assignment helped us understand that every tool gives one angle on the corpus, and that we need to compare these angles to see the bigger picture.

## Works Cited

Crymble, Adam. "Building the Invisible College." *Technology and the Historian: Transformations in the Digital Age*, 2021, pp. 107-136.

Underwood, Ted. "The Risks of Distant Reading." *Distant Horizons: Digital Evidence and Literary Change*, 2019, pp. 144-174.

## Sources for corpus info

- [Leigh Brackett (Wikipedia)](https://en.wikipedia.org/wiki/Leigh_Brackett)
- [Philip K. Dick (Wikipedia)](https://en.wikipedia.org/wiki/Philip_K._Dick)
- [Andre Norton (Wikipedia)](https://en.wikipedia.org/wiki/Andre_Norton)
- [H. G. Wells (Wikipedia)](https://en.wikipedia.org/wiki/H._G._Wells)
- [Marion Zimmer Bradley (Wikipedia)](https://en.wikipedia.org/wiki/Marion_Zimmer_Bradley)
- [Henry Kuttner (Wikipedia)](https://en.wikipedia.org/wiki/Henry_Kuttner)
- [Planet Stories (Wikipedia)](https://en.wikipedia.org/wiki/Planet_Stories)

## Tools used

- [Claude, April 2026](https://claude.ai/)
- **Stylo**
- **TF-IDF**


