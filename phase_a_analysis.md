# Phase A: Ethical Analysis

**Research Task 7 — The Ethics of Synthetic Representation**
Pratham Vasani | Syracuse University School of Information Studies

This analysis is grounded in the artifact I produced in Task 6: three synthetic
speech pipelines generating a spoken narrative about the 2024 Syracuse women's
lacrosse season. The source script was the coach-advisory narrative I wrote in
Task 5, phonetically rewritten for text-to-speech. Everything below reasons
outward from that build. The hypotheticals are my own construction, not
documented incidents.

Task 6 repository: https://github.com/Pratham-cybersecurity/Task_06_Deep_Fake

---

## 1. Returning to What I Built

### What the artifact was

I built three pipelines in a sandboxed Linux environment:

| Tool | Type | My listening note | Measured |
| --- | --- | --- | --- |
| espeak-ng | classic parametric | "very robotic" | F0 std 8.5 Hz — roughly 5× flatter pitch variation than the neural options |
| gTTS | cloud neural (Google API) | "somewhat AI-sounding" | mid-range spectral flatness |
| Piper | local neural (ONNX, CPU) | "smooth, most natural" | best spectral flatness score of the three |

A fourth tool, Coqui TTS, failed to install — it requires Python below 3.12 and
the environment runs 3.12.3. I documented the failure rather than discarding it.

The content was true. The statistics in the narrative came from data I had
scraped and verified myself in Task 5, and the LLM cross-check in that task had
confirmed the factual claims. The voice was nobody's — a generic synthetic
voice, not a clone of a real speaker. Every output file carried SYNTHETIC in its
filename, and the README disclosed the nature of the files at the top.

By every reasonable standard, nothing I built was harmful.

### What strikes me now

**The most convincing output came from the tool with the fewest gatekeepers.**

This is the finding I keep returning to, and it inverted what I expected going
in. I assumed the cloud service would produce the best audio, because that is
where the compute and the training data and the money are. It did not. Piper —
free, open source, running locally on a CPU in about seventeen seconds, with no
account, no API key, no terms of service, and no record of what I generated —
produced the output I found most natural, and it scored best on the acoustic
measure too.

That matters ethically in a way the quality difference alone does not. gTTS runs
through Google. Google can log requests, rate-limit an account, refuse a
customer, or shut down a pipeline that is being abused. Those are weak controls,
but they are controls, and they attach to a party with a legal address. Piper has
none of them. The version I ran has no idea what it said, no memory that it ran
at all, and no mechanism by which anyone could find out. The governance
conversation around synthetic media tends to assume the capability sits with
large vendors who can be regulated, pressured, or sued. My own results suggest
the frontier of *convincing* has already moved past the frontier of
*accountable*.

**I never hit a refusal, and the shape of that absence is informative.**

Task 7 asks what the vendors' refusals reveal about what they consider
dangerous. My honest answer is that I encountered none — and I think the reason
is more interesting than a refusal would have been.

None of these tools guard the thing I was actually doing. I gave them arbitrary
text and they spoke it. What TTS vendors do guard, when they guard anything, is
voice *cloning*: the workflow that requires a reference sample of a specific
real person. That is where consent checks, verification steps, and enterprise-only
gating tend to appear.

The implied model of harm is identity theft. The vendors are protecting the
person whose voice might be stolen. What nobody is protecting is the listener,
because a synthetic voice that belongs to no one in particular can say anything
at all, with no friction whatsoever. The deception vector is wide open; only the
impersonation vector is watched. I did not expect that, and it changed how I
think about where the risk actually sits.

**Disclosure lived in the filename, which means it lived nowhere.**

I checked provenance with exiftool. None of the three tools embedded C2PA content
credentials. None embedded a watermark of any kind. The audio files were
acoustically indistinguishable, at the metadata level, from a recording of a
human being.

So the entire disclosure regime on my artifact rested on two things: the word
SYNTHETIC in the filename, and a paragraph in a README that lives in a different
place from the file. Renaming a file takes one keystroke. Downloading a file
separates it from the README permanently. I had built what I thought was a
disclosed artifact, and what I had actually built was an undisclosed artifact
with a sticky note attached by the weakest possible adhesive.

This is the observation I would most want a reader to take from my Task 6 work,
and I did not fully see it while I was inside the build.

**What the process log does not capture.**

Two things. First, how *cheap* it felt. Seventeen seconds of CPU time. The
narrative had taken me hours of scraping, verification, cross-checking against a
second model, and rewriting for phonetic clarity — and the synthesis step, the
part that produces the thing an audience would actually encounter, was
instantaneous and free. The effort in my pipeline was almost entirely in *being
truthful*. A person who skipped that part would reach a comparable-sounding
artifact in under a minute.

Second, I noticed myself grading the outputs on naturalness as if that were a
neutral engineering metric. It is not. "Most natural" is a synonym for "most
likely to be mistaken for a person," which is a synonym for "most dangerous in
the wrong hands." I spent Task 6 optimizing for the property that makes the
capability hazardous, and I did not register the tension until I sat down to
write this.

**Would I build it again?**

The artifact, yes. It was honest, the content was verified, and the voice was
nobody's.

The thing I would not do again is publish audio that is disclosed only by
filename. If I repeated Task 6, I would put the disclosure *inside* the audio —
a spoken line at the head of the file stating that the voice is synthetic. It is
crude, it costs three seconds of runtime, and unlike metadata or a filename it
survives re-encoding, re-uploading, renaming, and excerpting by anyone who does
not deliberately cut it out. That single change is the main thing my own build
taught me, and it shows up as a hard requirement in the policy in Phase B.

---

## 2. Reasoning Across the Axes

Each hypothetical below is invented. They are deliberately small and local,
because the small local version is the one that is actually likely, and because
inventing them myself forced me to follow the consequences rather than borrow a
conclusion.

### Axis 1 — Truth: the same pipeline carrying false content

*Hypothetical.* A booster with a grievance against a coach wants her gone. He
takes my exact Task 6 pipeline — Piper, the same ONNX model, the same seventeen
seconds — and feeds it a script that is structured identically to mine. Same
register: measured, analytical, statistics-forward. But the numbers are invented.
The narrative states that the team's shooting percentage collapsed in the second
half of the season, that a named starter's minutes were cut after a disciplinary
incident, that the program's retention rate is the worst in the conference. He
posts it to a parents' forum as "audio from the athletics review meeting."

*What changes.* Mechanically, nothing. That is the finding. The pipeline does not
know, cannot know, and has no place where knowing could be inserted. There is no
step in my Task 6 build where a truth check could live. The cost of generating a
lie is exactly the cost of generating a verified fact: seventeen seconds. In
Task 5 and Task 6 combined, I spent perhaps twenty hours on verification and
seventeen seconds on synthesis. The asymmetry is brutal, and it runs the wrong
way — the honest actor pays almost all the cost.

What also changes is harder to name. My artifact borrowed the *authority* of
spoken delivery. A person speaking sounds like someone who could be questioned,
who is accountable for what they said, who knows things. Text does not carry that
assumption; speech does. When I used that register for content I had verified, I
was borrowing authority I had actually earned in Task 5. The booster borrows the
same authority having earned nothing. The register is doing identical work in
both cases — the difference is entirely invisible at the point of consumption.

I am not fully certain where the wrong sits here. The lie would be wrong if it
were written in a forum post. What synthesis adds is not the falsehood but the
*credibility transfer*, and I find it genuinely hard to say how much moral weight
that carries on its own.

### Axis 2 — Consent: someone else's voice

*Hypothetical.* Same booster, one step further. The coach gives postgame
interviews that are posted publicly; there are hours of clean audio of her voice.
He pulls thirty seconds, runs a cloning tool, and generates the same fabricated
narrative in her voice. Now it is not an anonymous synthetic speaker describing
the program — it is the coach, apparently, admitting to it herself.

*What changes.* Everything, and I want to be precise about why, because "it is
worse" is not an analysis.

Three distinct wrongs stack here, and they are separable. First, there is a new
victim. In the truth axis, the harm lands on listeners who are deceived. Here it
also lands on the coach, who has been made to say something. Second, the
falsehood becomes self-authenticating: the artifact is its own evidence. A
fabricated claim that the coach admitted something is refutable; a recording of
the coach admitting it is the refutation problem. Third, and worst, it is
*unfalsifiable from her side*. She can deny it. Denial is what a guilty person
does too. She cannot prove a negative about a recording of her own voice, and the
burden has silently moved onto her.

There is also a compounding effect that only becomes visible once this is
possible at all. The more common voice cloning becomes, the more plausible
"that's a fake" becomes as a defense — which means a genuine recording of genuine
misconduct becomes deniable. The technology damages the coach in the case where
it is used against her, and damages her accusers in the case where it is not. It
degrades the evidentiary value of recorded speech as a category, for everyone,
including people who never encounter a synthetic clip.

This is the boundary where I think the tool becomes a weapon, and notably it is
the *only* boundary the vendors meaningfully guard. Having reasoned through it, I
think they are guarding the right line — and guarding it far too thinly, given
that thirty seconds of public interview audio is all the raw material required.

### Axis 3 — Context: disclosure stripped

*Hypothetical.* Nobody acts in bad faith at all. A parent finds my actual Task 6
file — honest content, synthetic voice, SYNTHETIC in the filename, README
disclosure sitting in a GitHub repository two clicks away. She downloads it. Her
phone saves it as `audio_2026_09.mp3`. She forwards it to a team group chat,
where the messaging app re-encodes it. Someone clips the middle ninety seconds
and posts it to a parents' Facebook group with the caption "this is what they're
saying about the team." Within three hops, an artifact I built with every
disclosure I knew how to apply is circulating as an anonymous recording of an
unidentified person.

*What changes.* No one lied. Every individual step was an ordinary thing a person
does with a file. And the disclosure is gone, completely, because every layer of
it was external to the audio itself.

My exiftool check in Task 6 said there was no C2PA and no watermark, and at the
time I filed that as a limitation of the tools. Reasoning through this scenario,
it is not a limitation — it is the whole problem. The filename is not part of the
file. The README is not part of the file. Both are annotations *about* the
artifact, and artifacts travel without their annotations as a matter of routine.
Re-encoding would have destroyed embedded metadata even if it had existed, which
is exactly what the C2PA verification question in Task 6 was probing.

The lesson I take is that disclosure has to be *in the signal*. Anything that can
be separated from the waveform will be separated from the waveform, not by
attackers but by ordinary users behaving normally. This is the single most
actionable thing my own build taught me, and it is why the policy in Phase B
requires spoken disclosure inside the audio rather than treating metadata or
labeling as sufficient.

### Axis 4 — Scale: seventeen seconds, repeated

*Hypothetical.* A district-wide school board election. A single person with a
laptop generates four hundred personalized voice messages overnight —
neighborhood-specific, each naming a local school, each in a slightly different
synthetic voice, each claiming a candidate plans to close that particular
building. No two are identical, so nothing pattern-matches as a mass message.
They go out as voicemails the morning before the vote.

*What changes.* My Piper run took seventeen seconds on an ordinary CPU. Four
hundred messages is under two hours, and it parallelizes trivially. There is no
API to rate-limit, no account to suspend, no vendor to subpoena. The marginal cost
of the four hundredth message is electricity.

Scale does something qualitatively different from volume here. Three things:

It defeats refutation by timing. A correction takes a human being hours to
write and days to circulate. The generator's output is bounded only by disk
space. Truth cannot be manufactured fast enough to meet it.

It defeats detection by individuation. Mass messaging is caught because it is
identical. These are not identical. Every existing platform defense against
coordinated inauthentic behavior keys on repetition, and cheap generation removes
repetition as a signal.

And it changes what listeners assume by default. This is the effect I find most
troubling, and the hardest to mitigate, because it does not require any individual
message to succeed. Once a population has learned that voices in voicemail might
be fabricated, the rational response is to discount all of them. My honest Task 6
artifact gets discounted along with the fabrications. The genuine emergency
notification from the district gets discounted too. Bad-faith use does not just
add false signal — it consumes the credibility that true signal depends on, and
the honest user pays for the liar's activity.

### Axis 5 — Accountability distance

I am adding this axis because working through the other four kept surfacing
something none of them quite named.

*Hypothetical.* The district sends every family an automated call: "This is
Superintendent Reyes. Due to the water main break, all schools are closed
tomorrow." It is true, it is authorized, and the voice is synthetic — generated
from a script an assistant typed, because Reyes was in a meeting. A parent calls
the district to ask whether buses will run Thursday, and there is no one who
actually said the thing she is calling about.

*What changes.* Nothing false was communicated, no one's consent was violated,
nothing was stripped or faked. And yet something has been removed: the property
that a spoken statement has a speaker who can be asked a follow-up question.

Human speech carries an implicit warranty — the person saying it knows what they
said, stands behind it, and is available. Synthesis separates the statement from
any such person, cheaply and by default. Every use of this technology, including
entirely honest ones, spends down that warranty a little. My Task 6 artifact was
truthful and disclosed and I still could not have answered a question about it as
the speaker, because there was no speaker.

I do not think this makes honest synthetic speech wrong. But it makes it *costly
in a currency the user does not pay* — the cost lands on the general reliability
of spoken communication, and it is borne by everyone. That is the structure of a
commons problem, and commons problems are exactly the thing individual good
intentions do not solve. It is the strongest argument I have found for why
governance here cannot be left to the judgment of well-meaning individuals, and
it shapes the review requirements in Phase B.

---

## 3. The Mitigation Landscape

I tested two of these directly in Task 6. Those come first, because my own
results are better evidence than anything I could summarize.

### Provenance and content credentials

*The promise.* C2PA and similar cryptographic signing schemes attach
tamper-evident metadata to a file at creation, recording what produced it and
what has happened to it since. A verifying client checks the signature and shows
the chain of custody.

*What I found.* I checked all three of my Task 6 outputs with exiftool. None of
them embedded C2PA credentials. None embedded a watermark. The hypothesis I went
in with was that provenance metadata would survive or not survive re-encoding;
the actual result was that there was nothing to survive. Not one of three
independent tools — one of them Google's — wrote any provenance marker at all.

*Where it breaks.* Provenance is opt-in at the point of generation, and the tools
most likely to be used adversarially are precisely the ones that will not opt in.
An open-source model running locally can have its signing stripped by editing the
code. Even where credentials exist, they survive only until re-encoding, and
messaging platforms re-encode by default. And verification requires a client that
checks — most people listen to audio in apps that display no provenance interface
at all. C2PA's real function, as far as I can tell from my own results, is to let
honest institutions prove their own outputs are theirs. That is worth something.
It is not a defense against a bad actor, and it was completely absent from my
artifact despite my having deliberately gone looking for it.

### Detection

*The promise.* Automated classifiers identify synthetic audio from acoustic
artifacts invisible to listeners.

*What I found, honestly.* I did not run one. The sandboxed environment had no
browser and no upload capability, so I could not submit my files to Hive or
Deepware. I documented this as a gap in Task 6 rather than quietly skipping it,
and I am repeating it here because an unverified claim about detector accuracy
would be exactly the kind of borrowed authority this analysis is about.

What I do have is adjacent and still useful. I measured acoustic properties
across the three tools: espeak-ng's pitch variation was about five times flatter
than the neural options, and Piper scored best on spectral flatness. Those are
the kinds of features a detector keys on — and the measurements show the signal
shrinking as the tools improve. espeak-ng would be trivially detectable by
anything, including a human ear. Piper, free and local, sat at the far end of my
measurements.

*Where it breaks.* Detection is structurally behind. A detector trains on the
outputs of existing generators; a new generator immediately invalidates part of
that training set. My own measurements show the gap narrowing across three tools
I happened to pick in a single afternoon. Detectors also produce both error types,
and both are costly: a false positive brands a real recording as fake, and a
false negative launders a fabrication. And even a perfect detector is only useful
if someone runs it, which almost no one does in the moment of listening.

### Disclosure norms

*The promise.* Label synthetic content and the audience can discount it
appropriately.

*Where it breaks.* My context axis is the whole argument. My artifact was
disclosed twice over and was three ordinary user actions away from being
undisclosed, with nobody acting in bad faith. External labels — filenames,
captions, platform tags, README paragraphs — are separable from the file, and
separable things get separated. Disclosure also only reaches the attentive: a
label reaches the reader who reads it, which is not the person scrolling a group
chat.

The version that actually works is in-signal disclosure — a spoken line inside
the audio. It survives re-encoding, forwarding, and renaming. It is defeated by
deliberate editing, which means it stops honest ambiguity but not attack. That
limited scope is exactly right for what disclosure should be asked to do: it is a
tool for preventing accidents, not crime.

### Legal and regulatory approaches

*The terrain.* Broadly, four shapes: disclosure mandates requiring synthetic
political content to be labeled; election-adjacent restrictions creating
blackout windows near voting; non-consensual imagery statutes, historically
aimed at sexual content and being extended toward voice and likeness generally;
and platform obligations pushing detection and labeling duties onto
distributors.

*Where it breaks.* Jurisdiction is the immediate problem — generation is global
and law is territorial, and a local school board election can be targeted from
anywhere. Enforcement is retrospective: a takedown arrives after the vote.
Disclosure mandates bind the people who would have disclosed anyway. And
definitions are genuinely hard to draft — a statute broad enough to cover my
booster's fabrication may also cover ordinary audio editing, dubbing, accessibility
tooling, and satire.

### Platform policy

*The promise.* Platforms have committed to labeling synthetic media, requiring
disclosure from uploaders, and removing deceptive manipulated content.

*Where it breaks.* The gap between commitment and enforcement is the whole story.
Labeling depends on detection, which is behind. Self-disclosure depends on
uploaders volunteering. Enforcement is reactive and slow relative to the
timescale on which a fabrication does its damage — my scale hypothetical does its
work overnight. Coverage is uneven, and content that is removed from one platform
persists on others. Platform policy is a real constraint on scaled, persistent,
public campaigns, and close to no constraint at all on a clip that circulates in
private group chats — which is where my context axis put it.

### Professional and organizational norms

*The promise.* Journalism has broadly committed to not synthesizing voices or
footage in news content. Entertainment has negotiated consent and compensation
terms for digital replicas. Advertising and education are developing disclosure
practices. Political consulting has the weakest norms, which is an unfortunate
distribution given where the stakes are highest.

*Where it breaks.* Norms bind members and the worst actors are not members. They
are also unevenly distributed exactly opposite to risk. Most importantly for this
task, norms are usually stated at a level of generality that does not decide
cases — "we will use AI responsibly" does not tell an employee whether they may
generate a superintendent's voice for a snow-day call. That gap is the reason
Phase B is written as an operational document rather than a statement of
principles.

### Summary

Nothing here is a solution and I do not think any combination of them adds up to
one. What they do, at best, is raise cost and narrow opportunity for
opportunistic misuse while doing almost nothing against a determined adversary.

Task 7 asks whether that makes them pointless. I do not think so, but the reason
is narrower than I expected when I started. The mitigations are worth having
because most harm is not the work of determined adversaries — it is the work of
ordinary people cutting corners, and of honest artifacts drifting out of context
the way my own would have. Mitigations are effective against accidents and
casual misuse, which is most of the actual volume, and ineffective against
attacks, which is most of the actual severity. A governance document should be
built with that distinction in front of it, rather than pretending the same tools
serve both. That is the premise the policy in Phase B is written on.
