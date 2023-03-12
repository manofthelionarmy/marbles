# Summary:
# Related Stuff:
[[How to Parse git diff]]
# Notes:
- There are several elements I need to tokenize:
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
- The above is a hunk header and its body or content.
- Another example:
```
diff --git a/ast/ast.go b/ast/ast.go
index 11219ea..fcd6180 100644
--- a/ast/ast.go
+++ b/ast/ast.go
  
```
- this is the unified git diff header that tells me:
	- the format of diff is `git`.
	- the `pre-image` file (or "old" file) is ast.go.
	- the `post-image` is (or "new" file) is ast.go
	- If they are the same, it means we modified the file.
	- If they aren't the same, it means we renamed the file.
- The main kind of tokens off the bat are:
	- `@@`, `-`, `+`, `,`, `INTEGER`.
	- `@@` depends on context, it can refer to the start or end of our header.
	- `-` will act like a prefix operator and depends on context. In the hunk header, it can refer to old file. In the content or body of our hunk, it refers to removal of a line.
	- `+` will act like a prefix operator, and it also depends on context. In the hunk header, it refers to the new file. In the content of the body of our hunk, it refers to the addition of a new line.
	- `,` is kind of like a binary operator in the context of the hunk header. The "left operand" is the start of the code. The "right operand" is the "total number of lines/up to number of lines".
	- `INTEGER` is the token for the numerical values within the binary operator of `,`.
 - I could make more tokens, but I do need a way to analyze the changes in the context of json according to what was written in the ticket.
		 - I could always make it easier and use a regex, and then extract some content via regexes. 