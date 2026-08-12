# Post-Mortem: The Domain Translation Gap

I've spent over 14 years building complex healthcare IT systems — specifically in the Epic Radiant and clinical configuration space. In healthcare, when stakeholders fight over a system design, clinical safety or federal compliance is the ultimate trump card. You build technical gates, force written sign-offs, and use compliance as a shield. That playbook is a massive strength, but it doesn't fully translate to local government, where the trump card isn't compliance — it's political optics and departmental turf. This exercise exposed a real domain gap.

A rogue Planning Director operating outside project governance isn't a bug — it's a feature. I underestimated how much those politics distort standard project management.

## The Building Department Blind Spot

That gap created a massive blind spot in my discovery framework.

When I sequenced the first 30 days, I engineered it entirely around surviving the politics. I grabbed Business Licensing for a quick, isolated win. I put Fire up front to lock down life-safety rules. I saved Planning for last to build leverage before facing the hardest stakeholder.

But in doing that, I completely dropped the Building Department out of the sequence.

In municipal permitting, Building is the operational center of gravity. They are politically neutral, but they are absolutely workflow-central. I was so intensely focused on managing the stonewalling and the turf wars that I sidelined the people who actually process the bulk of the day-to-day work. I proposed building a house without talking to the foundation pourers.

## What I Would Change

If I ran this exact project tomorrow, Building would be my Week 1 priority.

You can't solve a political problem just by optimizing the technical sequence, and you can't let the loudest stakeholder dictate the critical path. You don't build leverage just by outmaneuvering the difficult departments — you build it by anchoring the system's baseline data model with the highest-volume, most neutral users.

Once you establish the operational reality with Building, you hold the objective high ground. When Planning or Fire inevitably try to drag the scope out of bounds later on, you have a solid, agreed-upon structural core to defend.

Fourteen years of configuration teaches you how to build bulletproof infrastructure and force difficult decisions into writing. But this case study was a necessary reminder: mapping the political architecture is just as critical as mapping the database. And you have to anchor your design in the operational center, not just the political extremes.
