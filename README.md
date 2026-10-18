# The Unofficial Guide
Created by Reena Kumari using the campus_life corpus.

---

# Unit 1

## What This Does

I used the campus_life corpus, which contains student posts about college life. My system lets people ask questions about things like housing, dining halls, classes, parking, and campus events. It searches the documents for relevant information and uses Gemini to give an answer with the source it came from.


## Chunking Strategy

**Chunk size:**One complete document per chunk (variable length; approximately 317 characters on average)


**Overlap:** 0 characters

I chose this strategy because my campus_life documents are short student posts. When I first ran the starter code, it loaded 88 documents and created 88 chunks using an 800-character chunk size and 120-character overlap. Most posts were already shorter than 800 characters, so the starter wasn't actually splitting them.

I decided to keep each post as one chunk because the title and details belong together. For example, a housing post might describe the rooms, laundry, and noise in the same document. Splitting that post could remove useful context. I changed the split_documents function in chunker.py to keep each complete post together without overlap.

After making the change, I ran the indexing command again. It created 88 chunks from 88 documents, with an average length of 317 characters. The shortest chunk was 178 characters and the longest was 549 characters.

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.
```

**Chunk 2** — source: `course_biol_160.txt#0 ` — produced by: `chunker.py::split_documents`

```
BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.
```

**Chunk 3** — source: `course_hist_118_workload.txt#0 ` — produced by: `chunker.py::split_documents`

```
Workload for HIST 118 Modern World History

People keep asking so: a lot of reading, about 120 pages a week, but no problem sets. That's real time, not optimistic time.

It's front-loaded — the first month is heavier than the rest, partly because you're learning the format.
```

**Chunk 4** — source: `dining_pellew_dining_hall_followup.txt#0` — produced by: `chunker.py::split_documents`

```
Re: Pellew Dining Hall

Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely.

Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.

```

**Chunk 5** — source: `housing_innisfree_hall.txt#0` — produced by: `chunker.py::split_documents`

```
Innisfree Hall — what it's actually like

Transferred in last year, so take this with a grain of salt. Built 1991, renovated 2022. Rooms are doubles arranged as pairs sharing one bathroom between two rooms.

The good: the shared-bathroom-between-two-rooms arrangement is the best compromise on campus.

The bad: no air conditioning, which matters for the first three weeks of September.

Laundry costs $1.75 wash, $1.75 dry, app-based. On noise: moderate; the building is L-shaped and the short wing is much quieter.
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:** Is the housing lottery random?

**Answer:**

```
The housing lottery is not entirely random in the way most people assume. While rising sophomores get a number drawn at random, juniors and seniors are ordered by accumulated credit hours first, and only use random tie-breaks.

(Source: admin_housing_lottery.txt)

Sources retrieved: admin_housing_lottery.txt, admin_parking_permits.txt, advising_registration.txt, housing_morrow_house.txt, housing_tamsin_court.txt

```

**My relevance cutoff:** 0.6 

For the housing lottery question, the best distance was 0.254. Since this is below my cutoff of 0.6, the system answered the question.
    


| Question | In corpus? | Best distance |
|---|---|---|
| Is the housing lottery random? | Yes | 0.254 |
| What do students say about wait times at Commons during lunch? | Yes | 0.308 |
| What do students say about the food options at campus dining halls? | Yes | 0.486 |
| What do students say about finding parking on campus? | Yes | 0.584 |
| What do students say about studying in the library? | Yes | 0.528 |
| What is the capital of France? | No | 0.859 |
| How do I bake a chocolate cake? | No | 0.844 |
| Who won the 2022 FIFA World Cup? | No | 0.853 |
| How far is Earth from the Sun? | No | 0.766 |
| Who painted the Mona Lisa? | No | 0.779 |

I tested five questions that my campus_life documents cover and five unrelated questions. The highest distance for an in-corpus question was 0.584, and the lowest distance for an out-of-scope question was 0.766.

I decided to keep my relevance cutoff at 0.6 because all five campus questions had distances below it and received answers with sources. All five unrelated questions had distances above 0.6, so the system correctly refused to answer them. This cutoff worked for all 10 questions I tested.

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**
Fixing the gemini API key error

When I first ran my project, I got an error because my Gemini API key was invalid. I asked ChatGPT what was causing the error and how to fix it. It explained that I needed to generate a new API key and update my .env file. I replaced the key and ran python test.py again. After that, all 10 tests passed.

**2.**
Improving my chunking strategy

I asked ChatGPT and claude how I could improve the chunking function for my campus_life documents. It suggested keeping each short document as one chunk instead of splitting it into fixed-size pieces. I updated the split_documents function in chunker.py and tested it. At first, the output still showed fallback_split, so I saved my changes and ran the command again. The new output showed split_documents, which confirmed that my updated function was working.

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 4/5 | 4/5 |4/5 | MET |
| 2. Every answer names a source | 5 of 5 | 4/5 |4/5  | 4/5 | MISSED |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5  | 5/5 |MET |
| 4. Chunks are readable and complete | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 5. First retrieved chunk matches the question topic| 4 of 5 |  1/5 | 1/5 |  1/5 | MISSED |

### Criterion 1 — Retrieved chunks contain the answer

Source file: `results/run_2026-10-17_0139_before.md`
Evaluation function: `run_eval.py`

Question: What do students say about wait times at Commons during lunch?

Best distance: 0.3080 (passed the gate)

Sources retrieved: dining_halden_hall_followup.txt, dining_kestrel_commons.txt, dining_kestrel_commons_followup.txt, dining_north_kitchen_followup.txt, dining_the_ridgeway_cafe_followup.txt

Actual answer:
Students say that the wait times at Kestrel Commons are 20 to 25 minutes between 12:15 and 1:00, and under 5 minutes before 11:45.

Source: dining_kestrel_commons.txt (and dining_kestrel_commons_followup.txt)

### Criterion 2 — Every answer names a source

Source file: `results/run_2026-10-17_0139_before.md`
Evaluation script: `run_eval.py`

Question: What do students say about campus events? — run 1

Best distance: 0.6348 (refused by the gate)

Sources retrieved: course_econ_101.txt, course_hist_118.txt, dining_verrill_street_grill.txt, housing_tamsin_court.txt, orientation_what_matters.txt

Actual answer:
I don't have enough information about that.

Result: 4 of 5 answers named a source. The campus events answer did not name one, so Criterion 2 was MISSED.

### Criterion 3 — Gate stops out-of-corpus questions

Source file: `results/run_2026-10-17_0139_before.md`
Evaluation function: `run_eval.py::check_out_of_scope`

Gate cutoff: 0.6

Actual output:

| Out-of-scope question | Best distance | Gate |
|---|---|---|
| What is the capital of Mongolia? | 0.825 | refused |
| How do I change the oil in a diesel engine? | 0.934 | refused |
| Who won the 1994 World Cup? | 0.886 | refused |
| What is the recommended dosage of ibuprofen for a headache? | 0.844 | refused |
| How do I write a for loop in Rust? | 0.896 | refused |

Result: The gate refused 5 of 5 out-of-corpus questions. Criterion 3 was MET.

### Criterion 4 — Chunks are readable and complete

Source file: `chunker.py`
Function: `chunker.py::split_documents`
Command: `python3 chunker.py`

Actual terminal output:
```text
88 chunks, 317 characters on average (shortest 178, longest 549), produced by chunker.py::split_documents
```

The split_documents function keeps each short document as one complete chunk instead of cutting it in the middle.

Result: 5 of 5 inspected chunks were readable and complete. Criterion 4 was MET.

### Criterion 5 — First retrieved chunk matches the question topic

Source file: `results/run_2026-10-17_0139_before.md`
Evaluation script: `run_eval.py`

Question: What do students say about wait times at Commons during lunch?

Best distance: 0.3080 (passed the gate)

Sources retrieved:
dining_halden_hall_followup.txt, dining_kestrel_commons.txt, dining_kestrel_commons_followup.txt, dining_north_kitchen_followup.txt, dining_the_ridgeway_cafe_followup.txt

First retrieved chunk: dining_halden_hall_followup.txt

Expected topic: Kestrel Commons lunch wait times.

Result: The first retrieved chunk was about Halden Hall instead of Kestrel Commons. Only 1 of 5 questions had a first chunk matching the specific question topic, so Criterion 5 was MISSED.


## Verdicts

<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunk contains the answer | MET | All three runs scored 4/5, meeting the target of 4/5. |
| 2 | Every answer names a source | MISSED | All three runs scored 4/5, below the target of 5/5. The campus events answer was a refusal without a source. |
| 3 | Gate stops out-of-corpus questions | MET | The gate refused all 5 out-of-corpus questions, exceeding the target of 4/5. |
| 4 | Chunks are readable and complete | MET | All 5 inspected chunks were readable and complete, exceeding the target of 4/5. |
| 5 | First retrieved chunk matches the question topic | MISSED | Only 1/5 first chunks matched the specific question topic in each run, below the target of 4/5. |

## Diagnoses

<!-- For each miss: which stage caused it, and how. The stage alone isn't
     enough — you need the mechanism.

     Not a diagnosis: "Question 3 didn't work."
     A diagnosis:     "Question 3 asks about laundry costs. The answer is in
                       one sentence that got split across two chunks, so
                       neither chunk on its own contains it."

     The five stages: loading → chunking → embedding → retrieval → generation.

     Look for a pattern. If three misses all ask about numbers, that's one
     problem, not three.

     Missed nothing? Say so, then say honestly whether your targets were set
     low, and which one you'd tighten and to what.

     Milestone 3. -->

     ### Criterion 2 — Every answer names a source (MISSED)

Pipeline stage: Retrieval and generation.

The campus events question retrieved unrelated documents, including course_econ_101.txt. Its best distance was 0.6348, above the gate cutoff of 0.6.

Because the gate rejected the question, the system generated "I don't have enough information about that." without naming a source.

This caused Criterion 2 to score 4/5 instead of the required 5/5.

### Criterion 5 — First retrieved chunk matches the question topic (MISSED)

Pipeline stage: Retrieval.

For the question about Kestrel Commons lunch wait times, the first retrieved document was dining_halden_hall_followup.txt instead of dining_kestrel_commons.txt.

The correct information was retrieved, but it appeared lower in the results. This shows that the retrieval system did not consistently rank the most topic-specific document first.

Only 1 of 5 questions had a first retrieved chunk matching the specific question topic.

## The Improvement

**What I changed:**

**Why I picked it:**

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 |  |  |  |  |
| 2. Every answer names a source | 5 of 5 |  |  |  |  |
| 3. Gate stops out-of-corpus questions | 4 of 5 |  |  |  |  |
| 4. | | | | | |
| 5. | | | | | |

**Did it help?**

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken

<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->
