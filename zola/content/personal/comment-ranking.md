+++
title = "Ranking Source Code Comment Delimiters"
date = 2020-07-30
description = "I present a definitive ranking of source code..."
template = "personal.html"
[extra]
category = "Programming"
+++

I present a definitive ranking of source code comments.  I included some of my
favorites and least favorites. I rougly went off of the
[Rosetta Code](https://www.rosettacode.org/wiki/Comments) list, but didn't put
in many of the exotic languages. The ones I did put in were arbitrary, so if
your favorite language isn't in these rankings please let me know so I can
judge it.

## Multiline Comments
1. `#| |#` - (two way tie) looks weird but easier to type
1. `{- -}` - (two way tie) good but a little hard to type
3. `/* */` - only if it's nestable
4. `--[[ ]]--` - consistent with `--` but too many characters
5. `%{ }%` - easy to change between line and nested, still ugly
6. `<!-- -->` - Clocking in at a whopping 7 characters, the HTML gets points
  docked for its ridiculous overindulgence. Not to mention its asymmetry.
7. `(* *)` - Parentheses and asterisks are already the most overused of
  characters. You have the whole keyboard to work with! Consider the ambiguity
  of parsing something like `(* try (simpl in *) *)`?
8. `""" """` - is it a string? a comment? who knows??? 

## Single Line Comments
1.  `#` - "The comment that will probably work"
2.  `--` - elegant look but 2nd place because it has two characters
3.  `;` - feels like you're hacking, good use of homerow
4.  `//` not bad, but just is a little ostentatious, you know?
5.  `%` is typeset so many different ways, looks crunched in monospace
6.  `!` - drawing your attention needlessly
7.  `"` or `'` - leaves things... _shudders_ unmatched
8.  `C` - what are we using, punch cards?
9.  `dnl` - discard to next line, more like discard this comment scheme.
10. `REM` - seriously?
11. `⍝` - oh, APL.

Honorable mention goes to: BibTeX where everything is a comment unless you say otherwise.

