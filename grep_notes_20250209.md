grep command

```
-i, --ignore-case
      Ignore  case  distinctions  in  patterns and input data, so that characters that differ only in
      case match each other.

-v, --invert-match
      Invert the sense of matching, to select non-matching lines.

-c, --count
      Suppress  normal output; instead print a count of matching lines for each input file.  With the
      -v, --invert-match option (see below), count non-matching lines.

-E, --extended-regexp
       Interpret PATTERNS as extended regular expressions (EREs, see below).

-w, --word-regexp
       Select only those lines containing matches that  form  whole  words.   The  test  is  that  the
       matching  substring  must  either  be  at  the beginning of the line, or preceded by a non-word
       constituent character.  Similarly, it must be either at the end of the line or  followed  by  a
       non-word  constituent  character.   Word-constituent  characters  are  letters, digits, and the
       underscore.  This option has no effect if -x is also specified.

-n, --line-number
      Prefix each line of output with the 1-based line number within its input file.
```

Regular expressions can be used with grep.
