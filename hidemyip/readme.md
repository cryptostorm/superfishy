So this stuff came right off one of the source documents on the #koromida infection, but I've not yet dug into it very much yet
https://www.hide-my-ip.com/download.shtml
https://malwr.com/analysis/YzNjZjNiYTZiMTljNGUzYWJjNDIxNDE3NGQ3ZTA3OTg/

(note: not casting aspersions, because no solid data yet - but again, this came right out of the original #koromida docs from CERT, if memory serves...)

Dr. Web flags as "backdoor-trojan" but until someone dives into the decompile, I'd not put much weight on that tbh.

You want to know something weird? This strings dump is verbatim - exactly - what we saw in the cyberghost strings dump. Pretty hard not to notice, what with the ancient Borland refenrence and whatnot. What are the chances?

"This program must be run under Win32
`.itext
`.data
.idata
.rdata
@.rsrc
AnsiChar
string(
AnsiString
TObject
FastMM Borland Edition (c) 2004 - 2008 Pierre le Riche / Professional Software Development
An unexpected memory leak has occurred.
The unexpected small block leaks are:
The sizes of unexpected leaked medium and large blocks are:
bytes:
Unknown
AnsiString
UnicodeString
Unexpected Memory Leak"
