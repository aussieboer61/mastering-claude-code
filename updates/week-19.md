# Week 19 — 2026-09-28

## Headline

**The user's view is the one that counts.** Three changes. All three are about the gap between
what the assistant can see and what the user is actually looking at: the newest link versus the
one they have open, a listing from a few minutes ago versus what they just did, and the date a
message was written versus the day it describes.

## Why

The week was mostly hands-on build work: a metal design iterated live over an afternoon,
small electronics on the bench, and a handful of errands in between.

The design went through more than ten revisions, and each one was published through a share
tool that hands back a fresh link on every upload. So every revision had a new address, and the
user kept having to ask for it, until they said they were sick of asking. When a single stable
address finally replaced them, the first version published there still carried an old section.
The assistant then reported the page as showing only the final design. That was true of the
copy it had just checked and false of the one the user was reading. Twenty-five superseded
copies were still live.

Later the same day the user sent an email the assistant had drafted. Asked to confirm, the
assistant read a mailbox listing taken a few minutes earlier, saw the message still queued, and
told the user it hadn't gone. It had. On the bench, a vendor's table of what a status light means
said a battery wasn't connected, on a board that kept running with its power cable pulled. The
user acted on that guidance before the explanation was corrected.

And while researching a present, the assistant stated a family member's birthday as fact. It had
found an old message that mentioned something happening "on their birthday" and taken the date
the message was written as the date of the birthday. The message was describing an event from
years before. The user corrected it at once.

## What changed in the guide

**Chapter 1 — CLAUDE.md.** Two new behavioural defaults.

*One address for a thing you keep revising.* An artefact the user views goes to one address for
every revision. Overwrite it in place and put the address in every reply that changes it. Old
copies keep serving old versions, so retire them in the same step if the address ever has to
change, and check every address the user has been given before calling a page clean.

*Re-read before you contradict.* When the user reports something they did or saw and the
assistant's evidence disagrees, first check how old and how direct that evidence is. Re-query
before contradicting. When a document and an observation disagree, the document is the thing to
doubt, and no remedy should be offered until the explanation fits what the user sees.

**Chapter 2 — Memory.** One new failure mode.

*A message's date is not the event's date.* A timestamp records when something was said, not
when what it describes happened. Reading one as the other manufactures precise, confident,
wrong personal facts. Those cost the most trust and get checked the least. Personal facts enter
memory only from the user's direct statement, and an assistant working one out from a message
date should ask instead.

## Archive housekeeping

Week 09 rolled off the ten-week archive into the *Older summary* in the index.
`updates/week-09.md` removed.
