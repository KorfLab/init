Rules
=====

We no longer write computer programs line-by-line. AI does that work for us.
What are the best practices in this new era? AI allows us to be very lazy. For
example, we could prompt AI to: "make a program that does low complexity
filtering on DNA" and AI would probably do a good job. However, instead of
being lazy and being satisfied with _good_, what if we used AI to strive for
_perfect_? It was impracticle to do that in the past, but with AI doing some of
the heavy lifting, perhaps reaching for the stars is not just a stated goal
that gets us on the roof, but an actual expectation.

## ACE in Theory ##

In my research group, we write software by following a philosophy I call
**ACE**[^1]: axiom-based, component-driven engineering. The TL;DR looks like
this:

- Break up a complex problem into simple problems
- Define the truths of the simple problems
- Create simple building blocks with our truths as guardrails
- Build complex things from simple building blocks
- Ensure the complex things work as designed by replication

There is nothing new here. All of these things were in practice long before AI.
What's different about today is that we no longer write all of the code
ourselves. That release of responsibility prompts us to state our goals more
ephatically and examine our progress more rigorously.

[^1]: Of course axiom-based component-driven engineering also spells out ABCDE.
But ABCDE is too big of a mouthful. I could equally have named ACE "axiomatic
component engineering" and not have this issue. But really, I do like that it
matches ABCDE, so it stays. Further, when gaming, I often use the tag "Ace",
which is not a reference to my ability, but a shorthand of "acetylene".
However, some people were pronouncing this as "ace tylene" and I couldn't have
that, so shortened it to "ace", and now my gaming tag and coding philosophy
have neatly merged.

### Axiom-Based

In ACE, the first word is **Axiom**. It must be a very important word if it
comes first. Not only is the word important, the act of defining our axioms is
what should happen first. Axioms are our truths. For example, if we are
building tools for sequence analysis, the letters of DNA and protein are
axioms. Of course, there are many more. To make sure axioms stay true, we write
tests that prove them to be true. Note that I wrote **we write tests**. AI does
not write our axioms or our axiomatic tests: we do. One line at a time.

If your goal is to "build a complexity filter" the first thing you do is to
define the axioms yourself. If you don't know what a complexity filter is or
what it is used for, then you have no business building the software until such
time as you can state the axiomatic truths behind a complexity filter. What
_exactly_ are the axioms in this example? Sequences, window sizes, entropy
thresholds, and outputs that prove that the algorithm behaves _exactly_ as we
have specified.

### Component-Driven

Computers are very complex things. For example, nobody understands the entirety
of an operating system. And yet, operating systems are made from many simple
components, each of which can be fully understood. For example, one might know
precisely the inputs, outputs, and error conditions of a function that computes
a factorial. The input is a non-negative intger. The output is a positive
integer. That's 5th grade math. But the factorial function can easily result in
huge numbers that overflow typical integer and floating point representations.
Consequently, building a factorial function inside a computer requires a little
bit more knowledge than 5th grade math. A developer who doesn't understand
mathematical precision and numerical limits may end up making software that
falls short of our quest for perfection.

A component-driven mindset is one where you build small pieces, prove those
work as intended (axioms), and then connect them to each other to build complex
systems. We do not leave it up to AI to make important decisions for us. We do
not allow AI to take shortcuts or to hallucinate. We provide hard guard rails
on **simple components we fully understand**.

### Engineering

Even if we are not writing software one line at a time, prompting is still a
form of engineering. Vibe coding has the same rigor as vibe sciencing: none.
**Neither engineering nor science was founded on laziness**, and so it shall
remain under my watch.

The practice of engineering is an unending loop of designing, prototyping,
testing, and refining. Iteration is natural. Failure is expected. Engineering
is also inherently a team-based activity. Very few things of value are
engineered by a single person. When it comes time to write axioms and their
tests, a diverse team will perform much better than a maverick flying solo.

In a bioinformatics context, we expect our programs to be run by scientists, on
various *nix platforms, using a CLI in some kind of automated workflow. Our
target audience is smart, usually in a rush, and probably under-educated in the
nuances of the IT world they find themselves in. As such, the software must
work on multiple systems, be packaged with tutorials that cover typical usage
scenarios, and follow community standards for input/output. In order to achieve
these goals, we must **build/deploy our software on multiple systems**.

What _exactly_ does "multiple systems" mean? It means more than one computer,
for certain. Developing all of your code on one computer ensures it will break
on another. "Multiple" also means different people, different languges, and
different AI agents. If two languages/people/environments/etc produce different
outputs, the spec is too brittle. The time to work at the "multiple" level is
from the beginning, not stapled on as an afterthought.

## ACE In Practice ##

I want to provide exercises that put you in the ACE mindset. These examples are
under development and will be featured in the reboot of MCB185 (Winter 2027).

------------------------------------------------------------------------------

## Legacy Rules ##

Before ACE we had 5 Rules. These rules are still in effect, but today there is
less emphasis on how to program and more emphasis on how to organize.

- Rule #1: Create Small Data
- Rule #2: Develop in Parallel
- Rule #3: Beautifully Simple
- Rule #4: Refactoring Happens
- Rule #5: Be a Scientist, not a Robot

### Rule #1: Create Small Data

>Measure twice, cut once

Before you start on a project, the most important thing to do is to build a
minimal dataset for development and testing. We call this "small data" (as
opposed to "big data". We may also call it "dev data", "test data", or "debug
data". Small Data is probably not a single file: it should represent positive
and negative controls. Small Data is sometimes created by hand, sometimes
created synthetically, and sometimes sampled from real data. We use Small Data
for multiple purposes:

- Minimize debugging time
- Functional tests
- Tutorials

Bioinfomatics software development and experiments take much more time than you
expect. The iterative debugging stage can be very long. In order to reduce the
downtime between debugging sessions, we need data that can be processed very
quickly, and whose outputs are uncomplicated.

Software changes over time. Even if we make no changes to our code, our
software depends on other software, which may change silently. In order to
ensure that our software continues to produce the same output as before, we
must perform "functional tests" that automatically compare the current output
to the previous, expected output. Small Data is used during automated testing.

When it comes time to distribute our software, there should be a tutorial that
shows how to use the software. Small Data is useful again here.

Making Small Data can take some time. For example, let's imagine your project
involves RNA-seq on the human genome. What is the proper test set? Not the
entire human genome and 10 RNA-seq libraries. The test set should fit neatly
into the git repository where the code lives. Ideally, the entire repo is
small. Over 100M is bad. Under 10M is good. Creating Small Data for an RNA-seq
project means making a miniaturized version of the human genome and curating
some reads that align to that part of the genome. Obviously, the region of the
genome matters. You probably want some areas with high coverage and some areas
with low coverage. It may take a week or more to create a proper set of files.
And later, you may have to make a better one. It will be worth it in the long
run. This part of our work is sort of like making reagents and calibrating
instruments. It's a pain but must be done to speed up debugging time and
improve reproducibility.

Some examples of Rule #1 Small Data are in the `init/data` directory.

### Rule #2: Develop in Parallel

>Working in one setting ensures irreproducibility

Two very important words in science are _rigor_ and _reproducibility_. Science
should be repeatable. One way to ensure that your work can be replicated by
others is to simultaneously develop your software on multiple computers in
parallel (e.g. laptop, desktop, cluster, cloud service, VM).

If you're wondering how you can you run an analysis inside the minimal VM on
your laptop when it lacks the 5 TB of data files required by the analysis...
see Rule #1. If you are using only one computer, you are probably guaranteeing
that whatever you're doing is not reproducible. As scientists, that's sort of
unforgivable. Personally, I bounce between different systems on a daily basis.

How does one Develop in Parallel in practice?

- Use GitHub to manage your code and Small Data
- Use Mini-forge (conda) to manage your software environment (where possible)
- Never, never, never hard-code paths

All of the code you write should be managed in GitHub repositories. Generally,
there is no need to make them private. GitHub isn't the place where you publish
your data after you complete your experiments. It's where you work ever day. If
you're a programmer of some kind, which you must be to be in the lab, your
programming activity is part of your CV. Your GitHub profile and activity are
therefore part of your CV.

Big Data should **not** be stored in git repos. For this reason, your programs
and data should be in very different places on whatever computer you're using.
Of course, you should never hard-code paths. Use a softlink or environment
variable to abstract your Big Data locations on different machines.

### Rule #3: Beautifully Simple

A programming project has many facets.

- Beautiful - it is visually appealing
- Clear - it is easy to explain to others
- Clever - it is intellectually appealing
- Correct - it solves the problem as intended
- Documented - it has documents for developers
- Efficient - it doesn't use much memory
- Extensible - it can be used for other projects
- Fast - it doesn't take long to run
- Friendly - it has documents for users, including a tutorial
- Novel - it is the first of its kind
- Robust - it has unit, functional, and integration tests
- Simple - it is not complex

Biologists focus on their program being correct. They have a specific problem
to solve and want a solution to that problem. Being so focused on their
problem, they tend to lose sight of the bigger picture that involves other
users and other developers.

Computer scientists focus their efforts on being clever, efficient, and novel.
Their goal is to prove how smart they are. They might not care about users or
other developers.

Software engineers focus on building robust and extensible systems. They may
spend so much effort engineering the perfect abstraction that they miss their
target audience.

Scientific programming exists in an environment with transient users and
developers. Code must be developed in such a way that new users and new
developers can deploy and extend the project. If you can describe your software
as "beautifully simple" then you will have solved most of the difficult
problems. Beautifully simple code is easy to understand. This makes it easy to
debug and extend. When making programming choices, don't program for yourself,
but rather the less experienced person who comes after.

Beautifully simple also applies to writing papers and to scientific
communication in general. When you have the choice between _fenestrated_ and
"it looks like it has windows", choose the simpler language. Your goal in
writing is to communicate to an audience that probably did not learn English as
a first language. If you think scientific writing is supposed to demonstrate
your _erudition_, you are wrong. Scientific writing is like code. It's not for
you, but for a less educated audience.

### Rule #4: Refactoring Happens

>Sometimes you don't know how to start until you get to the end

No code is correct the first time it is written. Oftentimes, we only know how
to start a project after we have gotten to the end. For this reason, it's a
good idea to push some small part of the project as far as possible before the
refactoring begins. Don't spend too much time up front engineering the perfect
solution. Odds are, you didn't understand the question perfectly and you're
going to have to do a ground-zero rewrite. The more over-engineering you do at
the start, the more painful it will be to tear it all down later.

This doesn't mean you're encouraged to write shitty code. You should always
strive to write code you are proud of. If you can't show your code to the PI
and say "isn't this great?" then re-write it and make it great.

### Rule #5: Be a Scientist, not a Robot

>Copy-paste-modify is the enemy of expertise

As a novice at anything, we often learn by copying others. Then by modifying
what we have copied. But this practice eventually results in doing things "the
easy way" instead of "the right way".

- Do you find yourself copy-pasting code from one program to another?
- Have you forgotten how to write a simple windowing algorithm?
- Do you have to look up the syntax of a `lambda` function every time?
- Are you just the go-between from a web page to your text editor?
- Have you become a copy-paste robot?
- Have you become a slave to AI?

Well stop doing it. Stop the copy-paste-modify practice. Stop looking up
everthing on the Internet. Stop asking ChatGPT for answers. Stop using code
completion. Use your brain to write every character of every line yourself, and
when you get stuck ask a _person_ for help. Yes, this will take longer. But
you're here to learn, not to act like a robot.

What makes a scientist a scientist? Two things:

1. Asking questions
2. Performing experiments

As a member of my lab, I expect you to act like a scientist. This means
constantly asking questions and performing experiments that address those
questions. Imagine you need to run an RNA-Seq job on the cluster. You might ask
yourself, "how many CPUs should I put in the SBATCH script and how much RAM
should I specify?" Have you considered making those questions into an
experiment that you perform?
