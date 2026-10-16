# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks should include at least one chunk that contains the information needed to answer the question.


**Why this target:**
My campus_life corpus contains 88 short documents covering different student-life topics, including dining, housing, parking, and studying. I chose 4 out of 5 because most of my test questions should have relevant information in these documents, but some questions may be harder to answer if the information is limited or spread across documents.



---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
I chose all 5 because every answer should include a source so students can verify the information. My system stores the original document filenames with the retrieved chunks, so including a source in every answer should be achievable. If an answer does not name a source, it could mean the source information was not passed correctly or the system failed to display it.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

**Why this target:**
My corpus contains information about campus life, so the system should refuse questions about unrelated subjects instead of making up answers. I chose 4 out of 5 because the relevance gate relies on similarity distances, and sometimes an unrelated question might still match a campus document by accident.

---

## 4. Something about your chunks
At least 4 out of 5 chunks I look at should be easy to understand on their own and should not end in the middle of a sentence or idea.

**Why this target:**

Most documents in my campus_life corpus are short student-life posts, so I want each chunk to preserve enough context to understand what the document is discussing. I chose 4 out of 5 because nearly all sampled chunks should be readable without needing another chunk to understand them. A chunk that ends halfway through a sentence could cause the system to miss important information.

---

## 5. The first retrieved result matches the question topic

For at least 4 of my 5 test questions, the first retrieved chunk should discuss the same campus-life topic as the question.

**Why this target:**

My test questions cover different campus-life topics, including dining, parking, studying in the library, and campus events. I want the highest-ranked result to match the question's topic instead of simply containing similar words. I chose 4 out of 5 because most questions should retrieve a relevant top result, although some topics may overlap.


<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
