---
title: "Marked by Dust - ADHoc Intel Walkthrough"
date: 2025-10-31T20:00:47+05:30
draft: false
params:
  slug: ""
layout: "post"
tags: ["OSINT" , "CTFROOM"]
authors: ["Lordsudo"]
---

# 🕯️ Marked by Dust
**Category:** OSINT  

> *“Time has buried many secrets, but even in the dust, a precise place remains.”*

The Question says:
> Every place has its special words; find the ones that belong to this artifact

---

# **Prologue — The Forgotten Door**

It began with silence.  
No coordinates, no hints — only an image.  
A sun-scorched door of ancient wood, framed in cracked earth, its texture heavy with history. It stared back at the solver like a memory half-recalled, daring them to look closer.

![Door Image](https://gist.github.com/user-attachments/assets/cef64f76-855c-44e4-9b5a-415db4b16047)

No text, no metadata, only dust and shadow.  
Yet even the dust remembers.  

---

# **Act I — Unearthing the Past**

The curious know that the first step in OSINT is to *listen* to the image.  
Reverse image search — the modern archaeologist’s brush — peels away the years.  

![Reverse Search](https://gist.github.com/user-attachments/assets/6b3aba76-e998-439d-9681-accbf29eae4c)

Within moments, recognition takes form:  
the **Great Mosque of Djenné**, Mali’s crown of sun-dried earth and faith.  
Its surface ripples with the rhythm of centuries, rebuilt and reborn in every season.  

A sacred place. A landmark of humanity.  
And yet, the riddle whispers again:  
> “Every place has its special words…”  


Coordinates emerge easily enough — a quick glance at the mosque’s **Wikipedia** entry reveals its exact position:  

![Wikipedia](https://gist.github.com/user-attachments/assets/ec96cbd6-b4a4-4dbe-81b9-02a5b6bbfb14)

> 13°54′19″N 4°33′20″W

But the question asks for *words*, not numbers.  
And in riddles, phrasing is never an accident.

---

# **Act II — The Grid of the World**

The hint comes to mind like a faint echo:  
> “Everything is part of a grid.”  

A curious phrase — one that pulls the mind toward a system built not on degrees or decimals, but *words*.  
**what3words** — a global lattice that divides the planet into tiny squares, each marked by a unique trio of words.  


Feed the mosque’s coordinates into the grid, and the map breathes life into language:  

![what3words](https://gist.github.com/user-attachments/assets/3370c139-97dd-4385-809f-a5ab15484359)


> `///validated.reports.meanders`  

Three words.  
Three syllables that stand as a digital signature for one of Earth’s oldest living monuments.  

The riddle is complete.  
From image to location, from numbers to words — a full circle of discovery, wrapped in dust and logic.

---

# **Epilogue — The Architect’s Voice**

When I forged *Marked by Dust*, I wanted silence to be its language.  
An image without context, a riddle without noise. The kind that makes players stop, stare, and listen — not to words, but to the **echo of curiosity**.  

The artifact, that ancient door of Djenné, was never chosen at random. It stood as a symbol — of endurance, of memory, of civilization surviving beneath centuries of sand. I wanted players to realize that even what time buries can still be found, if one knows where to look.  

Every layer of the challenge was deliberate:  
- the **reverse image search** to spark recognition,  
- the **coordinates** to ground their findings in reality,  
- and finally, the **grid** — the whisper of what3words — to remind them that even in a world mapped by numbers, language still carries precision.  

The lesson was simple, yet timeless:  
that *information never dies*. It merely waits beneath the dust for someone curious enough to uncover it.  

And when they finally found the three words — their special words — they weren’t just solving a puzzle.  
They were speaking to a place that has outlasted empires.

---

# 🜃 Conclusion

One image. One trail. A thousand grains of knowledge buried in time.

> In the vast desert of information, only those who see patterns in the dust can uncover what others overlook.

Every pixel, every word, every hint — each was a fragment of truth waiting to be unearthed. Marked by Dust wasn’t just about finding a location; it was about learning to read the silence between clues.

Patience, precision, and curiosity — these are the tools of the true OSINT hunter.

*The dust remembers. The question is — do you? 🜂*

---


