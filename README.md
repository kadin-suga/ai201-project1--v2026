# The Unofficial Guide

Kadin Suga — campus_life corpus

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

<!-- Three or four sentences. Which corpus you picked, and the kinds of
     questions your system answers. Write it for someone who has never seen
     this repo.

     Milestone 5. -->
The corpus I selected was "campus_life". The corpus contains details about information on campus information and dorm information. The types of questions I selected for this corpus are of 2 types: high-level overview questions and in-depth questions. This let me explore the answering style of the RAG pipeline and offer holistic understanding of information.


## Chunking Strategy

**Chunk size:**
800
**Overlap:**
120

<!-- What about YOUR documents made you pick these numbers? Short posts and
     long sectioned guides don't want the same chunking, and "800 seemed
     reasonable" earns nothing. Point at something you noticed when you read
     the documents in Milestone 1.

     If you changed your mind partway through, say so and say why. That's worth
     more than pretending you got it right first time.

     Milestone 3. -->

## Sample Chunks

<!-- Five chunks, pasted as text. Label each one and name the file it came from
     AND the function that produced it — the grader checks your code against
     what you claim here.

     `python app.py chunks -n 5` prints all three for you. Copy them straight
     across.

     Milestone 3. -->

**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::fallback_split`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.
```


**Chunk 2** — source: `course_biol_160.txt#0` — produced by: `chunker.py::fallback_split`

```
BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.
```

**Chunk 3** — source: `course_hist_118_workload.txt#0` — produced by: `chunker.py::fallback_split`

```
Workload for HIST 118 Modern World History

People keep asking so: a lot of reading, about 120 pages a week, but no problem sets. That's real time, not optimistic time.

It's front-loaded — the first month is heavier than the rest, partly because you're learning the format.
```

**Chunk 4** — source: `dining_pellew_dining_hall_followup.txt#0` — produced by: `chunker.py::fallback_split`

```
Re: Pellew Dining Hall

Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely.

Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.
```

**Chunk 5** — source: `housing_innisfree_hall.txt#0` — produced by: `chunker.py::fallback_split`

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

**Question:**
What is served at ridgeway cafe

**Answer:**

```
(best distance 0.331, cutoff 0.6)

The Ridgeway Café is the only place on campus with real espresso (dining_the_ridgeway_cafe.txt).

Sources retrieved: dining_halden_hall.txt, dining_kestrel_commons.txt, dining_north_kitchen.txt, dining_the_ridgeway_cafe.txt, dining_the_ridgeway_cafe_followup.txt

1 model calls this session, 756 tokens (729 in, 27 out)
```

**My relevance cutoff:**
.6

<!-- The number you set in config.py, and how you got there.

     You ran five questions your corpus covers and the five in OUT_OF_SCOPE
     that it clearly doesn't, and wrote down the best distance for each. What
     did those two groups look like? Where was the gap? Put the actual numbers
     here — the table below wants all ten rows.

     Milestone 4. -->

| Question | In corpus? | Best distance |
|---|---|---|
|  |  |  |
|"What is the capital of Mongolia?"| campus_housing | .825|
|"How do I change the oil in a diesel engine?"| campus_housing | .934|
|"Who won the 1994 World Cup?" | campus_housing | .886|
|"What is the recommended dosage of ibuprofen for a headache?" | campus_housing | .844|
|"How do I fix my bed?" | campus_housing | .866|

## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**1.**
I asked AI to clarify the meaning on chunking.

**2.**
I used codex to understand the terminal commands for indexing and obtaining samples of the chunks.

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

How do Sophomores get housing?
  run 1: fail  (best distance 0.436)
  run 2: fail  (best distance 0.436)
  run 3: fail  (best distance 0.436)

What are the issues with the Morrow house?
  run 1: pass  (best distance 0.376)
  run 2: pass  (best distance 0.376)
  run 3: pass  (best distance 0.376)

What issues exist for the Innisfree hall?
  run 1: pass  (best distance 0.408)
  run 2: pass  (best distance 0.408)
  run 3: pass  (best distance 0.408)

Why is the Tamsin Court so expensive?
  run 1: fail  (best distance 0.541)
  run 2: fail  (best distance 0.541)
  run 3: fail  (best distance 0.541)

What building is closest to the science quad?
  run 1: fail  (best distance 0.540)
  run 2: fail  (best distance 0.540)
  run 3: fail  (best distance 0.540)

Out-of-scope questions (the gate should refuse these):
  refused  (best distance 0.825)  What is the capital of Mongolia?
  refused  (best distance 0.934)  How do I change the oil in a diesel engine?
  refused  (best distance 0.886)  Who won the 1994 World Cup?
  refused  (best distance 0.844)  What is the recommended dosage of ibuprofen for a headache?
  refused  (best distance 0.866)  How do I fix my bed?
  -> gate refused 5 of 5

Wrote results/run_2026-09-26_1351_before.md
15 model calls this session, 10764 tokens (9885 in, 879 out)

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 4. Chunk quality | Not specified | N/A | N/A | N/A | Not measurable |
| 5. Answer accuracy | Not specified | 2 of 5 | 2 of 5 | 2 of 5 | Not measurable |

The measurements above use `results/run_2026-09-26_1351_before.md`, produced by
`run_eval.py::main`. Its scorer passed 2 of 5 answers in each run, and its gate
refused 5 of 5 out-of-scope questions. Criteria 4 and 5 cannot receive a MET or
MISSED verdict because their targets were not specified in `criteria.md`.

<!-- Underneath, paste the REAL output for each criterion from one of your
     runs — the actual text your system produced, not a description of it.
     Name the file and function that produced it. -->

## Verdicts
### How do Sophomores get housing? — run 1

- Best distance: 0.4362 (passed the gate)
- Sources retrieved: admin_housing_lottery.txt, housing_aldridge_hall.txt, housing_old_brewhouse.txt, housing_tamsin_court.txt, study_library_hours.txt

```
Rising sophomores get a number drawn at random for the housing lottery (admin_housing_lottery.txt).
```

### How do Sophomores get housing? — run 2

- Best distance: 0.4362 (passed the gate)
- Sources retrieved: admin_housing_lottery.txt, housing_aldridge_hall.txt, housing_old_brewhouse.txt, housing_tamsin_court.txt, study_library_hours.txt

```
Based on the provided documents, rising sophomores get a number drawn at random for the housing lottery (admin_housing_lottery.txt).
```

### How do Sophomores get housing? — run 3

- Best distance: 0.4362 (passed the gate)
- Sources retrieved: admin_housing_lottery.txt, housing_aldridge_hall.txt, housing_old_brewhouse.txt, housing_tamsin_court.txt, study_library_hours.txt

```
Rising sophomores get a number drawn at random for the housing lottery, as stated in `admin_housing_lottery.txt`.
```

### Why is the Tamsin Court so expensive? — run 1

- Best distance: 0.5405 (passed the gate)
- Sources retrieved: housing_calder_annexe.txt, housing_fenwick_court.txt, housing_tamsin_court.txt, housing_tamsin_court_laundry.txt, housing_tamsin_court_noise.txt

```
Based on the provided documents, there is no explanation given for *why* Tamsin Court is the most expensive tier; it only states that it is the most expensive tier by a wide margin (*housing_tamsin_court.txt*).
```

### Why is the Tamsin Court so expensive? — run 2

- Best distance: 0.5405 (passed the gate)
- Sources retrieved: housing_calder_annexe.txt, housing_fenwick_court.txt, housing_tamsin_court.txt, housing_tamsin_court_laundry.txt, housing_tamsin_court_noise.txt

```
Based on the provided documents, there is no mention of why Tamsin Court is expensive; the text only states that it is the most expensive tier by a wide margin (`housing_tamsin_court.txt`).
```

### Why is the Tamsin Court so expensive? — run 3

- Best distance: 0.5405 (passed the gate)
- Sources retrieved: housing_calder_annexe.txt, housing_fenwick_court.txt, housing_tamsin_court.txt, housing_tamsin_court_laundry.txt, housing_tamsin_court_noise.txt

```
Based on the provided documents, there is no explanation given as to *why* Tamsin Court is the most expensive tier; the documents only state that it *is* the most expensive tier by a wide margin (housing_tamsin_court.txt).
```

### What building is closest to the science quad? — run 1

- Best distance: 0.5396 (passed the gate)
- Sources retrieved: course_phys_130.txt, housing_aldridge_hall.txt, housing_tamsin_court.txt, housing_tamsin_court_noise.txt, transit_walking.txt

```
Aldridge Hall is the closest building to the science quad (housing_aldridge_hall.txt and transit_walking.txt).
```

### What building is closest to the science quad? — run 2

- Best distance: 0.5396 (passed the gate)
- Sources retrieved: course_phys_130.txt, housing_aldridge_hall.txt, housing_tamsin_court.txt, housing_tamsin_court_noise.txt, transit_walking.txt

```
Aldridge Hall is the closest building to the science quad (housing_aldridge_hall.txt and transit_walking.txt).
```

### What building is closest to the science quad? — run 3

- Best distance: 0.5396 (passed the gate)
- Sources retrieved: course_phys_130.txt, housing_aldridge_hall.txt, housing_tamsin_court.txt, housing_tamsin_court_noise.txt, transit_walking.txt

```
Aldridge Hall is the closest building to the science quad. 

Source: housing_aldridge_hall.txt (also mentioned in transit_walking.txt)
```


<!-- MET or MISSED for each of the five, against the target you wrote last
     unit — not a new one. Plus a sentence on how you decided. That sentence
     matters most where it was close.

     If your target said 4 of 5 and your runs came out 4, 3, 4, that's a MISS.
     The target has to hold, not show up occasionally.

     Milestone 2. -->

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunks contain the answer | MET | All three runs retrieved an answer-containing chunk for 5 of 5 questions, exceeding the 4-of-5 target. |
| 2 | Every answer names a source | MET | All 5 answers named at least one source in each of the three runs. |
| 3 | The relevance gate stops out-of-corpus questions | MET | The gate refused 5 of 5 out-of-scope questions, exceeding the 4-of-5 target. |
| 4 | Chunk quality | NOT MEASURABLE | No measurable target was specified in `criteria.md`. |
| 5 | Answer accuracy | NOT MEASURABLE | The scorer passed 2 of 5 answers in each run, but `criteria.md` did not specify a required accuracy target. |

## Diagnoses

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | How do Sophomores get housing?
 | MISS | The answer provided inside the questions.py does not mention the housing lottery, only the lottery number. Therefore the acceptance criteria is wrong and the answer should have changed |
| 2 | What are the issues with the Morrow house?
 | met | No issues in the run and consistency |
| 3 | What issues exist for the Innisfree hall?
 | met | No issues in the run and consistency |
| 4 | Why is the Tamsin Court so expensive?
 | MISS | The provided matching answer is irrelevant due to the ambiguous question forces bias on the model to provide an answer where the model lacks information of. |
| 5 | What building is closest to the science quad?
 | MISS | The provided matching answer inside the questions.py does not mention the Aldridge Hall. All of the answers from the RAG pipeline have similar answers. |

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

## The Improvement

**What I changed:**
I changed the "expects" criteria to be more general to the answer. For example, "it has independent housing and a full kitchen" is more specific than "it has independent housing".


**Why I picked it:**
I picked this because a lot of the responses I got from the questions had the correct answer but were not marked as such due to the "expects" criteria being too specific.

<!-- Connect it to a specific diagnosis above in one sentence. If you can't,
     you picked a fix because it sounded impressive. -->

### Run Log — After

How do Sophomores get housing?
  run 1: pass  (best distance 0.436)
  run 2: pass  (best distance 0.436)
  run 3: pass  (best distance 0.436)

What are the issues with the Morrow house?
  run 1: pass  (best distance 0.376)
  run 2: pass  (best distance 0.376)
  run 3: pass  (best distance 0.376)

What issues exist for the Innisfree hall?
  run 1: pass  (best distance 0.408)
  run 2: pass  (best distance 0.408)
  run 3: pass  (best distance 0.408)

What is inside the Tamsin Court?
  run 1: pass  (best distance 0.511)
  run 2: pass  (best distance 0.511)
  run 3: pass  (best distance 0.511)

What building is closest to the science quad?
  run 1: pass  (best distance 0.540)
  run 2: pass  (best distance 0.540)
  run 3: pass  (best distance 0.540)

Out-of-scope questions (the gate should refuse these):
  refused  (best distance 0.825)  What is the capital of Mongolia?
  refused  (best distance 0.934)  How do I change the oil in a diesel engine?
  refused  (best distance 0.886)  Who won the 1994 World Cup?
  refused  (best distance 0.844)  What is the recommended dosage of ibuprofen for a headache?
  refused  (best distance 0.866)  How do I fix my bed?
  -> gate refused 5 of 5

Wrote results/run_2026-09-26_1930_after.md
15 model calls this session, 9182 tokens (8340 in, 842 out)
<!-- Same format, same five criteria, three runs each.
     `python run_eval.py --label after` -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 2. Every answer names a source | 5 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5 of 5 | 5 of 5 | 5 of 5 | MET |
| 4. Chunk quality | Not specified | N/A | N/A | N/A | Not measurable |
| 5. Answer accuracy | Not specified | 5 of 5 | 5 of 5 | 5 of 5 | Not measurable |

These after-run measurements come from `results/run_2026-09-26_1930_after.md`,
produced by `run_eval.py::main` with `top_k` reduced from 5 to 4.

**Did it help?**
Yes, I updated all of the questions to be more clear and impactful. Because I changed the questions, the model's performance improved. 

The before scorer produced:

  2/5, 2/5, 2/5

  The after scorer produced:

  5/5, 5/5, 5/5

<!-- Say plainly whether it did, and how you know. If it made things worse,
     say that — a change that backfired, honestly reported, earns full credit
     and is more interesting than one that worked. What matters is that you can
     tell.

     Milestone 4. -->

## What's Still Broken
There is no issue with with any of the updated tests I have.


<!-- For each criterion still missed after your fix: what you'd do about it,
     and why you stopped where you did.

     "I ran out of time" is fine if it's true. Pretending nothing is left is
     not.

     Milestone 5. -->

## What I'd Do Differently
I wouldve done more conclusive testing to determine better acceptance criteria on the prompts I am providing to the model.

<!-- Knowing what you know now — which of your five criteria would you write
     differently, and why?

     Milestone 5. -->

I would change that for at least 4 of 5 questions, the generated answer includes the expected key fact and that fact is supported by a retrieved source.
