[How to read git diff](https://stackoverflow.com/a/2530012)
[How to read git diff 2](https://stackoverflow.com/a/31615438)
[What are git hunks, in regards to git and git diff](https://stackoverflow.com/a/37620752)
[What are git hunks, derived from gnu diffutil](https://stackoverflow.com/a/44400027)
# Summary:
# Related Stuff:
# Notes:
> When comparing two files, diff finds sequences of lines common to both files, interspersed with groups of differing lines called <mark style="background: #FFB86CA6;">hunks</mark>.

> intersperse: 
> 1 **:** to insert at intervals among other things

>2 **:** to place something at [intervals](https://www.merriam-webster.com/dictionary/intervals) in or among

- This means the differences between two files will be displayed at intervals, and these intervals pertain to the files. This is what we normal see when we run `git diff`. These are what <mark style="background: #FFB86CA6;">hunks</mark> are.
- Each hunk shows one area where the files differ.
- It appears a git patch consists of several elements:
		- git diff header
		- extended header lines
		- two line unified diff header
		- hunks (which is the rest of the patch).
- A hunk header has two formats:
```
@@ -1,8 +1,9 @@
```
or:
```
@@ -18,6 +19,8 @@ int cmd_http_fetch(int argc, const char **argv, ...
```

- Breaking it down:
```
@@ -1,8 +1,9 @@
```
- The prefix `-` in `-1,8` means "old". `1`  in `1,8` means this is the line number in the code. `8` means up to 8 lines. Putting it all together, a change was made on the old file at line 1 and it use to have up to 8 lines. 
- The prefix `+` in `1,9` means "new". `1` in `1,9` means this is the line number where the change occured. `9` means up to `9` lines. Putting it all together, this incoming change took place on line 1 and includes up to 9 lines. 
-  The second format includes the function name to give us developers more readability to know which function got modified.
- Continuing on with the hunk, this is its "content" or "body":
``` c
    #include "cache.h"
     #include "walker.h"
     
    -int cmd_http_fetch(int argc, const char **argv, const char *prefix)
    +int main(int argc, const char **argv)
     {
    +       const char *prefix;
            struct walker *walker;
            int commits_on_stdin = 0;
            int commits;
```
- The `-` prefix we see means this line got removed.
- The `+` prefix we see means a line got added.
- This translates to a function was renamed a new line was added called `const char *prefix;` 
- Recall the hunk header: these changes add up and match the hunk header details. These changes start at line 1. The old file had the content up to line 8, while the new file had content up to line 9. The function was renamed, a new line was added (so 8 + 1 = 9). This definitely checks out.
- I wonder if there is a way to keep track of what line that change occured while parsing.
- After some observation, I found a determinable way to calculate the line numbers on incoming changes for a hunk within a patch.
```
@@ -1,10 +1,14 @@
 package ast

-import "monkey/token"
+import (
+       "bytes"
+       "monkey/token"
+)

 // Node is a node in our AST
 type Node interface {
        TokenLiteral() string
+       String() string
 }

```
- On the right hand side of the 2 `,`'s' within the header are `10` and `4`. The difference between the two is `4`. Meaning wherever the next hunk occurs, it's incoming change will be incremented by 4, hence the incoming change starts at line 36 (32 + 4):
```
@@ -32,6 +36,15 @@ func (p *Program) TokenLiteral() string {
        return ""
 }

+// String returns a string value of our statments
+func (p *Program) String() string {
+       var out bytes.Buffer
+       for _, s := range p.Statements {
+               out.WriteString(s.String())
+       }
+       return out.String()
+}
+

```
- Continuing with the example, the difference of the numbers to the right of the `,`'s is 9 (15 - 6 = 9). Add the previous difference (4) to 9 (4 + 9) and we get 13. That means the next line will be incremented by 13, hence the old file starts at line 46, and the new file starts at 59 (46 + 13 = 59):
```
@@ -46,6 +59,19 @@ func (ls *LetStatement) TokenLiteral() string {
        return ls.Token.Literal
 }

+func (ls *LetStatement) String() string {
+       var out bytes.Buffer
+       out.WriteString(ls.TokenLiteral() + " ")
+       // TODO: need to implement the string for identifier
+       out.WriteString(ls.Name.String())
+       out.WriteString(" = ")
+       if ls.Value != nil {
+               out.WriteString(ls.Value.String())
+       }
+       out.WriteString(";")
+       return out.String()
+}

```
- So the formula could be: 
	- diff = prevDiff + newDiff, with prevDiff having an initial value of 0.
	- newDiff is calculated by `new_up_to_line`  - `old_up_to_line`.
	- with prevDiff set to diff after the calculation.
	- we then do:
		- diff + `old_start_at_line` to get the `new_start_at_line`. 
	- The diff can be negative, and this will still correctly calculate the `new_start_at_line`. Example, if we removed lines and didn't add new ones or if `new_up_line` > `old_up_to_line`.
- Hopefully this pattern I noticed can be used to help figure out what objects/parts of the json schema are being modified. I could calcualte the line by subtracting the current line of the incoming change by the current total diff:
  - line_of_old_code = line_of_new_code - diff.
  - Here, I can map new changes to the new ones, hopefully.
  - Other than that, now that I know how to read the diff, maybe this will become easier to parse and do semantic analysis on the changes to see what exactly they are doing and apply the rules in this "linter".