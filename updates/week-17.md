# Week 17 — 2026-09-14

## Headline

**The check that reported success.** Five new changes and two folded-in entries. The spine
through them is a verification that ran, passed, and never touched the thing it was supposed
to verify — a document checked by searching its text instead of looking at it, an archive
searched to prove a thing never happened, a refusal read as a ban on the wrong subject, a
file "delivered" to somewhere nobody could open it, and a rule applied to a match set nobody
counted.

## Why

The week's evidence came from ordinary work across a handful of sessions.

An invoice went out to a customer. Before attaching it, the assistant pulled the text out of
the PDF and searched it for the things that should not be there. It reported the document
clean three times. The rendered page carried an internal note giving the customer the markup
and the supplier's invoice number, a near-empty second page holding nothing but duplicated
payment boilerplate, and one clause printed twice inside a single paragraph. Rendering the
pages to images and looking at them found every fault in seconds — including on the page a
text search had reported as containing no matches at all.

A schematic was produced and handed over with a tool that says it sends a file to the user.
The user works over a remote shell and cannot browse that machine's filesystem, so nothing
arrived. He had already established the rule — put it on the share service, give me the web
address — and had to restate it, by his own count, for roughly the fiftieth time. The rule
was written down in two places. What was missing from it was the name of the tool that keeps
being mistaken for delivery.

A request to take two devices off a shared network for a couple of hours was implemented as a
firewall rule matching a hardware address. The pattern matched ninety-five addresses. For
about a minute the rule was also cutting off other people's devices, until the match count
was noticed and the rule narrowed to two addresses.

A property listing site returned a 403 with a message about a problem with the browser. That
looked like the host being blocked. It was not: the same page, on the same machine, loaded by
a real browser engine, returned 200. The refusal was about the client — headers, the
connection's fingerprint, the absence of everything a browser does — and the fix was one tool
tier up, not a proxy. The same investigation found the other end of the range too: the
strongest commercial anti-bot systems are not beaten by a headless browser either.

And a sweep of an entire message archive returned nothing on a subject the person involved
had described out loud, in conversation. The empty result was reported as a finding about
what had happened, rather than as a finding about the archive. Two further readings were
built on it, and both had to be withdrawn.

## What changed in the guide

**Chapter 9 — Tool discipline.** Three new failure modes.

*Extracted text is not the rendered document.* Text extraction discards the two things most
likely to be wrong about a document: where content landed, and how many times it appears.
Render the pages to images and read them, and check the page count as well as the content. A
text search is a good second pass for a specific leak and a bad first pass for "does this
look right".

*A bot wall is a verdict on the client, not on you.* A challenge page has almost never
blocked your address — it has declined your client. Move up the tool tier and read the error
text as a description of what was rejected. Pin the browser executable if the installed
bundle and the library's expected version differ. And know where the ceiling is, because
grinding at a wall a browser genuinely cannot pass is the failure this rule exists to
prevent, not a licence for it.

*An archive records what people wrote down.* A corpus search is excellent for dates,
sequence and exact wording, and close to useless for establishing that something did not
happen, because the things that matter most are the things nobody types. Report a sweep as
"not recorded in X", with the corpus named; ask whether the thing would ever be written down
before concluding from silence; and treat the user's own account as outranking the absence
of text.

**Chapter 1 — CLAUDE.md.** Two new behavioural defaults.

*Deliver through the surface the user can actually open.* A harness affordance that sends a
file to the user is not automatically delivery. Establish the openable channel once and route
every viewable artefact through it. Where a rule like this already exists and keeps being
missed, name the offending tool in the rule, not just the destination.

*Count the matches before you apply the rule.* Any selector that matches by pattern rather
than by name should have its match set printed and counted against the intended target count
before it is applied. Two targets means two matches; anything else is a stop sign. This is
the companion to *name the set before a batch mutation* — there the risk is a vague
description resolved generously, here it is a precise-looking selector that is broader than
it reads.

**Folded in from mid-week commits.** Two entries had landed in the guide during the week
without a week file or an index row:

- **Chapter 1 — *Patching symptoms on a target you can't see*** (20 Sep). On headless or
  remote hardware bring-up, a failure signature that repeats identically across two or three
  fix attempts is evidence about the target, not noise to route around. A storage read whose
  capacity flickered between zero and its real size was treated as a reader quirk for hours;
  the same card then failed to boot outright. Name the most likely root cause out loud —
  including a hardware fault — after the second identical failure, and test that hypothesis
  before trying another config guess.
- **Chapter 1 — *Bare URLs, never markdown links*** (15 Sep). A terminal's link detection
  grabs markdown link syntax together with the address, closing parenthesis included, so the
  link is silently broken. Write the bare URL on its own line; a label goes before or after,
  not wrapped around it. This overrides any tool instruction that says to cite sources as
  markdown hyperlinks.

## Archive housekeeping

Week 07 rolled off the ten-week archive into the *Older summary* in the index;
`updates/week-07.md` removed. `updates/week-06.md` was also removed — its row moved to the
Older summary in the week-16 round, but the file itself was left behind.
