# Bash-CRLF-selfheal v1.0 - Written by Kenneth Lutzke.
Bash oneliner that will self-heal the script it is placed in, if the script is saved with CRLF (Windows) line endings/terminators.

See bash-CRLF-selfheal.sh line 3 in this repo for the oneliner.

CRLF line-endings can often happen if the script is copy/pasted through an editor in Windows, which will make the script fail and unable to execute, resulting in weird errors such as (but not limited to):

```
bad interpreter: /bin/bash^M: no such file or directory
script.sh: line XX $'\r': command not found
: invalid optionscript.sh: line XX: set: -
script.sh: line XX: syntax error near unexpected token `$'in\r''
... and many others...
```
	
In short, this script does what dos2unix does, just in-line, on itself, and without the need for dos2unix to be installed.
Works and has been tested on both Linux and MacOS, and should in theory work everywhere else too (where bash and native bash tools are present).

When the oneliner is placed as the first line of code (after the #!/bin/bash), it will re-write the script it is placed in itself, should it have been saved with CRLF line-endings.
This oneliner should be placed within the first 100 lines of a script, but should be the first actual line of code, meaning that you could place this after 95 lines of comments, but before any other lines of code or variables.

The script will then work as follows:

If saved with normal unix line-endings:
- No change, everything will work as normal.

If saved with CRLF line endings:
- The script will not work if executed with './script.sh' as the #!/bin/bash line will also be affected by the CRLF, and the environment (bash/zsh/other) will not know how this script should be executed.
What normally happens next, is that the user will try to execute the script with 'bash script.sh', and now the #!/bin/bash is ignored, the selfheal oneliner is executed, this will re-write (permanently overwrite) the script to unix-style line endings, then automatically execute the script again, and run like normal, all without the user noticing.

Therefore implementing this oneliner in your bash scripts, and at the same time always instructing users to execute your scripts with 'bash script.sh' instead of './script.sh' will avoid this CRLF headache altogether - At least it has for me.

Furthermore, as a safeguard, this line will look for itself, and only if successful re-write the script, in order to avoid accidentally overwriting other files.

This oneliner was written as I kept getting feedback that my scripts were not working, only to find out they had been copied through Windows, and now contained CRLF line endings.
I therefore share this in case others are in the same boat, and hope that this will save you a lot of frustration when handing out your scripts.

No license (seriously, it's a oneliner), but feel free to keep my name in the oneliner, and if we ever meet, you are welcome to sponsor the first beer :)

-Kenneth Lutzke

Tags: bash CRLF ^M line terminator Windows dos2unix problem issue error
