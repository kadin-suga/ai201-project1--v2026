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

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
<!-- e.g. "One of my questions is about a topic only two documents mention, so
     I expect that one to be hard." -->

Question 1:
python app.py ask "What issues exist for the Innisfree hall"
  (best distance 0.363, cutoff 0.6)

Based on the provided documents, the issues for Innisfree Hall are:
* There is no air conditioning, which matters for the first three weeks of September (housing_innisfree_hall.txt).
* The building has moderate noise levels, and the wrong ratio of washers to dryers causes dryers to back up on Sunday evenings, leading to waits if you do laundry after 6pm on Sundays (housing_innisfree_hall.txt, housing_innisfree_hall_noise.txt, and housing_innisfree_hall_laundry.txt).

Sources retrieved: dining_halden_hall.txt, dining_pellew_dining_hall.txt, housing_innisfree_hall.txt, housing_innisfree_hall_laundry.txt, housing_innisfree_hall_noise.txt

1 model calls this session, 809 tokens (690 in, 119 out)

Contains: Yes


Question 2:
python app.py ask "What issues exist for the Morrow house" 
  (best distance 0.362, cutoff 0.6)

The issues for Morrow House include a known damp problem on the ground floor (which caused two rooms to be taken offline in 2024), laundry dryers backing up on Sunday evenings due to a poor ratio of washers to dryers, and noise levels that are loud until about 1am on weekends with no enforced quiet hours. 

Sources: `housing_morrow_house.txt`, `housing_morrow_house_laundry.txt`, and `housing_morrow_house_noise.txt`.

Sources retrieved: course_hist_118_workload.txt, housing_morrow_house.txt, housing_morrow_house_laundry.txt, housing_morrow_house_noise.txt, study_library_hours.txt

Contains: Yes

Question 3:
python app.py ask "Which housing is the best to stay at"                    
  (best distance 0.449, cutoff 0.6)

Based on the provided documents, there is no single housing option stated as "the best." Instead, each document highlights different positive and negative aspects of various buildings, such as:

* **Tamsin Court** offers the most independent housing and a full kitchen, but is the most expensive and isolating. (*housing_tamsin_court.txt*)
* **Aldridge Hall** is the closest building to the science quad, but its elevator goes out roughly one week per semester. (*housing_aldridge_hall.txt*)
* **Innisfree Hall** features a shared-bathroom-between-two-rooms arrangement considered the best compromise on campus, but lacks air conditioning. (*housing_innisfree_hall.txt*)
* **Morrow House** is the cheapest housing tier, but has a known damp problem on the ground floor. (*housing_morrow_house.txt*)
* **Old Brewhouse** is the most characterful building, but has uneven heating and old laundry machines. (*housing_old_brewhouse.txt*)

Sources retrieved: housing_aldridge_hall.txt, housing_innisfree_hall.txt, housing_morrow_house.txt, housing_old_brewhouse.txt, housing_tamsin_court.txt

Contains: Yes

Question 4:
python app.py ask "Who draws from the random lottery system for housing"
  (best distance 0.293, cutoff 0.6)

Rising sophomores get a number drawn at random for the housing lottery. 

Source: `admin_housing_lottery.txt`

Sources retrieved: admin_housing_lottery.txt, admin_parking_permits.txt, advising_registration.txt, housing_morrow_house.txt, housing_tamsin_court.txt

Contains: Yes

Question 5:
python app.py ask "How are sophomores and junior housing separated"
  (best distance 0.454, cutoff 0.6)



Based on the documents, rising sophomores get a number drawn at random in the housing lottery, whereas juniors and seniors are ordered first by accumulated credit hours, with tie-breaks done randomly. 

Source: admin_housing_lottery.txt

Sources retrieved: admin_housing_lottery.txt, housing_aldridge_hall.txt, housing_innisfree_hall.txt, housing_old_brewhouse.txt, housing_tamsin_court.txt

Contains: Yes

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
<!-- Why all five and not four? What about your setup makes that achievable —
     or what would have to go wrong for it not to be? -->

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
<!-- What did your distances look like when you set the cutoff in Milestone 4?
     Was there a clean gap, or did the two groups overlap? -->

---

## 4. Something about your chunks

<!-- YOU WRITE THIS ONE.

     How would you know if your chunks were the right size? Name something
     countable or observable.

     Examples of the right shape — don't copy these, they should come from
     what you actually saw in Milestone 3:
       - "At least 4 of 5 sampled chunks read as a complete thought, with no
          sentence cut in half at either end."
       - "No chunk is shorter than 200 characters, since anything below that
          in my corpus turned out to be a heading with no content under it." -->



**Why this target:**



---

## 5. Your choice

<!-- YOU WRITE THIS ONE TOO.

     Pick something you actually care about getting right. It could be about
     speed, about refusals, about a particular kind of question your corpus
     handles badly, about source attribution being correct rather than merely
     present — anything, as long as it names a number or an observable
     outcome. -->



**Why this target:**



---

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
