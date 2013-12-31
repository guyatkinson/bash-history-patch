# bash-history-patch

Patch to bash readline, to fix history search buffer if string is not found.


## bash42-history-display.patch

This fixes a surprising mismatch between the displayed search string and the search string buffer,
in the case where the search string, in the buffer, is not found in history.

Before the patch is applied, any characters typed which extend the search string so that
it doesn't match anything in history (in the current direction),
lead to the extra characters being invisibly appended to the search string buffer ctx->search_string, without being displayed. 
The user, even if (s)he becomes aware of what is going on, then needs to press backspace the correct number of times to remove the invisible characters,
before normal service resumes. These invisible characters, which affect the behaviour, are not within the
[Principle of least astonishment](http://en.wikipedia.org/wiki/Principle_of_least_astonishment).

After the patch is applied, any character typed which would cause the search string not to match history (in the current direction) is ignored 
(by removing it from the search string buffer).
This means that from the user's point of view,  the search string buffer and the displayed search string stay exactly in step, and only show 
a search string which matches history (in the current direction).




