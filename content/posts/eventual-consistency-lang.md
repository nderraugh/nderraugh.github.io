+++
date = '2025-03-20T14:15:48-04:00'
draft = false
title = 'Eventually Consistent Language'
+++
# Eventual Consistency

The notion of eventual consistency (EC) in computing is a helpful construct for dealing with a world that is by nature asynchronous.  Reasoning through EC scenarios lets us plan and build around these very real world computing problems.  Data arriving at different computer nodes out of order, or delayed require us to work through the logic of different logical cases to ensure that the nodes agree on the logically correct state... eventually.  We don't get any of this for free, it requires time and effort to design systems to leverage EC, but the payoff is that we wind up creating software that is more robust, and more deliberately addresses complicated real world problems.

# Software is Composed of Words

Software, today, is most commonly written with words -- I don't mean the [processor design's natural unit of data](https://en.wikipedia.org/wiki/Word_(computer_architecture)), I mean words like 'class', 'object', 'move', 'copy', etc.  Or sometimes with tokens that represent words: 'cls', 'obj', 'mv', 'cp'.  And although the operational semantics of a piece of software can be understood, if necessary, by human operators, it is often not necessary to use every day language in order to do that.  That is high level languages you might be at least passingly familiar with, like C, C++, Java, compile down into lower level representations.  Those lower level representations might be machine code, or they might be interpreted into machine code, eventually being rendered into binary instructions that will become electrical signals that execute directly in the CPU.

Words in everyday language however are not nearly as well defined as any of the linguistic representations we use to create software.  The meaning of everyday words can change over time, or change depending on the context in which they're used, or change depending on intonation, or change based on syntax, and they can even change depending on their semantics.

# Semantics

Semantics is the study of meaning in language.  "Cool" when describing the weather has a different meaning than when describing how you feel about a helpful new kitchen gadget.

Words have meaning.  But meaning changes based on a lot of varying rules and sometimes even vary while completely ignoring any known rules, as in the case when humans get creative.

# Eventually Consistent Semantics

Is the semantic content of a word eventually consistent?

Maybe. Probably. It would seem so. At least in some cases.  Only time will tell...?

But semantic consistency, if it is possible, will be at best transitory. What is agreed upon at some arbitrary instance in time may not hold for long. They say the only constant is change, whoever "they" are.

But what does it all mean?