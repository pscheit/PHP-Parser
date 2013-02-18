
# indentation

## indentation in emacs

emacs is a very old and stable editor, and you can have mixed feelings about this editor, but the main thing most people do agree with, is, that auto-indenting is (once understood) really good in emacs.
So I thought to port that algorithm to PHP to provide indentation as customizable as possible.

[here is a small explanation to the algorithm](http://cc-mode.sourceforge.net/html-manual/Indentation-Engine-Basics.html)

but i'll summarize it anyway

1. find syntactic Context of the (first) construct on that line.
  [Syntactic Symbols](http://cc-mode.sourceforge.net/html-manual/Syntactic-Symbols.html)
    
Conceptually, a line of code is always indented relative to some position higher up in the buffer (typically the indentation of the previous line). That position is the anchor position in the syntactic element.
A syntactic context can be more then one syntactic symbol

2. a buffer position is found whose column will be the base for the indentation calculation. It's the anchor position in the first syntactic element that provides one that is used. If no syntactic element(symbol) has an anchor position then column zero is used.

3. The syntactic elements are looked up for indentation offsets (--, ++, etc). These offsets are added together with the base column to produce the new indentation column.

So that gives us the indentation of a line relative to the previous line, which is the most used case in emacs. When a block is indented, emacs starts from the first line, indenting all files relative to the first untouched line.
For the indentation for PHP this is not a problem.
The indentation can be only as good as the syntactical analysis of the context. Thank god, we have already done this in all tokens in the stream. We just have to categorize them, to make them configurable.