# Task 07 — The Ethics of Synthetic Representation

**Pratham Vasani** | Syracuse University School of Information Studies
Faculty Sponsor: Ingrid Erickson
Submitted: October 2026

---

## The task

Research Task 7 asks for two things. Phase A is an ethical analysis of the
synthetic-media capability exercised in Task 6, grounded in the artifact I
actually built and extended outward through thought experiments of my own
construction rather than documented incidents. Phase B is a governance document
written for a specific organization — concrete enough that a real employee could
read it on a Monday and act on it — followed by an honest account of where that
policy fails.

The task deliberately scopes the reasoning to what I built and what I can
imagine, not to the research literature on deepfake harms. Every hypothetical in
Phase A is invented. None refers to a real incident or a real victim.

## What Task 6 produced, in brief

In Task 6 I built three text-to-speech pipelines in a sandboxed Linux
environment, synthesizing a 335-word narrative about the 2024 Syracuse women's
lacrosse season that I had written and fact-verified in Task 5:

- **espeak-ng** — classic parametric synthesis. Audibly robotic; measured pitch
  variation roughly five times flatter than the neural options.
- **gTTS** — Google's cloud neural service. Noticeably synthetic but acceptable.
- **Piper** — local open-source neural TTS, ONNX, running on CPU in about
  seventeen seconds. The most natural-sounding of the three, and the best on
  spectral flatness, beating the cloud service.

A fourth tool, Coqui TTS, failed to install on Python 3.12 and was documented as
a finding rather than discarded. An exiftool check confirmed that none of the
three working tools embedded C2PA content credentials or any watermark. No
commercial detector was run against the outputs, because the environment had no
browser upload capability; that gap is stated rather than papered over, here and
in Phase A.

Task 6 repository: https://github.com/Pratham-cybersecurity/Task_06_Deep_Fake

## The organizational context, and why

The Phase B policy is written for **Maplewood Unified School District**, a
constructed K-12 district of roughly 9,400 students and 1,100 staff across eleven
schools.

I chose a school district for three reasons.

Automated voice calls to families are already routine infrastructure there —
attendance, closures, emergencies — so synthetic voice is a genuine operational
temptation rather than a hypothetical one. The district has already trained its
families to trust a recorded voice from a district number, which means it has
built the exact asset that synthetic media can destroy.

Minors are involved, which gives the policy something it must refuse outright
rather than manage with disclosure. A policy that can only ever say "yes, with a
label" is the failure mode the task warns about, and a student population forces
the question.

And emergency notification supplies the sharpest refusal in the whole document. A
district that uses synthetic voice for convenience on Tuesday has spent
credibility it needs on the Thursday when it calls to say a school is in
lockdown. That trade-off is concrete, consequential, and not resolvable by
disclosure — which made it the most useful thing I could have had to reason
against.

I avoided a corporate marketing setting deliberately, on the brief's warning that
standard settings produce standard policies.

## Map to the documents

| File | What it is |
| --- | --- |
| [`phase_a_analysis.md`](phase_a_analysis.md) | Phase A. Return to the Task 6 artifact; five axes with invented hypotheticals; full mitigation survey. |
| [`phase_b_policy.md`](phase_b_policy.md) | Phase B. The governance document itself, addressed to Maplewood Unified. |
| [`limitations.md`](limitations.md) | Stress test of the policy — well-intentioned failure modes, bad-faith failure modes, unresolved questions. |

Phase A moves in three parts: what the artifact looks like from outside the
build, then five axes extending outward from it (truth, consent, context, scale,
and an accountability axis I added), then a survey of six mitigation categories
with what each promises and where it breaks. The policy takes positions on
permitted uses, prohibited uses, consent workflow, disclosure, provenance,
review, refusal, and incident response.

## What surprised me

**The best-sounding output came from the tool with the least accountability.** I
expected Google's cloud service to win on quality. Piper beat it — free, local,
running on a CPU in seventeen seconds, with no account, no API key, no logging,
and no party anywhere who could be asked what it generated. The governance
conversation around synthetic media assumes the capability sits with large
vendors who can be regulated or pressured. My own results suggest the frontier of
*convincing* has already moved past the frontier of *accountable*, and I did not
go into Task 6 expecting to find that.

**I never hit a refusal, and the reason turned out to be the finding.** The task
asked what vendor refusals reveal about perceived danger. I encountered none —
because these tools do not guard arbitrary text-to-speech. What gets guarded is
voice *cloning*, which needs a reference sample of a real person. The implied
model of harm is identity theft: vendors protect the person whose voice might be
stolen. Nobody is protecting the listener, because a synthetic voice belonging to
no one can say anything at all with no friction. The impersonation vector is
watched; the deception vector is wide open.

**My disclosure was weaker than I thought while building it.** I labeled every
output SYNTHETIC in the filename and disclosed in the README, and considered the
question handled. Working through the context axis, I realized that the filename
is not part of the file and the README is not part of the file. Three ordinary
user actions — download, forward, clip — strip both, with nobody acting in bad
faith. That observation is why Section 4.1 of the policy requires disclosure
spoken *inside* the audio, and it is the main thing I would do differently if I
rebuilt the Task 6 artifact.

**Writing the refusals was harder than writing the permissions,** and I think
that is the real lesson of the exercise. Permitted uses write themselves. Saying
no to a superintendent who wants a snow-day call in eleven languages at 5 a.m.
requires defending a position against a sympathetic case, and the defense has to
hold when the person reading it is tired and under pressure. Most of my drafting
time went into Section 2 and Section 7, and I now suspect those two sections
carry nearly all of the policy's actual protective value.

**And I wrote a policy that forbids my own education.** The student prohibition
in Section 2.2 refuses all synthetic replication of minors with no consent
pathway. I believe it is correct. It also means a student at Maplewood could not
do the project that taught me everything this analysis rests on. I noticed that
only while writing the limitations section, and I have not resolved it — it is
recorded there as an open question rather than smoothed over.

## Scope note

This repository contains written reasoning and a written policy. Per the task
requirements, it contains no synthetic media and no synthetic media of any real,
identifiable person. The Task 6 artifacts remain in the Task 6 repository, linked
above.

Maplewood Unified School District is fictional. The policy is written to be
adoptable by a real district of comparable size.
