# Second Closet Development Process

At the Second Closet Engineering Team, we try our best to follow the [AGILE SCRUM methology](https://www.mountaingoatsoftware.com/agile/scrum). 

- Our sprints run at a lenght of 2 weeks.
- We use [CLUBHOUSE](https://app.clubhouse.io/secondcloset/dashboard) to track our development progress

## Important Dates

### Monday

**SPRINT PLANNING (2-4 hours)** 

GOAL: Estimate and schedule the tickets that we can commit to the 2 week timeline.

---

### Tuesday

GOAL: Prepare Release Notes if there is a scheduled Release for Tomorrow

---

### Wednesday

**Release Protocol**

1. Merge last `release candidate` branch into `master`
2. Deploy the branch into PROD

**Prepare for next release (If upcoming Friday is the End of the Sprint)**
1. Cut a release candidate branch
2. Rest of unfinished tickets from the sprint is merge into this `release candidate` branch

---

### Thursday 

**BACKLOG GROOMING (2-4 hours)**

GOAL: Discuss the next major feature (EPIC) and break it down to smaller tickets that is manageable by one-two people.

If the discussion for the next feature is not complete, then schedule another session tomorrow.

---

### Friday

**STAGING DEPLOY**
1. Merge all leftover branches into the `release-candidate` branch.
2. Deploy release candidate branch into PREPROD.

**RETROSPECTIVE and DEMO**

GOAL: Demo the major changes in the first half of the meeting. In the second half, discuss the previous sprint and bring up 
the good and room for improvement.
