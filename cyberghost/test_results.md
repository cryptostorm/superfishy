https://www.virustotal.com/en/file/ff9bbfd17010414d04b9f1291b7d79658a24097a56f4e525084dff5e96931136/analysis/1424658561/

https://www.virustotal.com/en/url/ab5d28f8de1eca5cf893f013e308bcbf484d4b8aeb8c1671d35c55e9226e77dc/analysis/1424666733/

Tip comes from this tweet:
https://twitter.com/badjin_rank/status/569653516102291456

https://malwr.com/analysis/YTRjYmQzNTNmMTNkNDRhOTkwZDU4OTc3NDYwNWI1NjE/

Rolling log of progress...

(05:18:04 AM) df: when you start the main .exe is says "Checking public certificate..." then says "Download required - Your system requires additional components to be downloaded blah blah blah should CyberGhost 5 download this stuff now?"'

(05:16:16 AM) df: install.log shows a C:\Program Files\CyberGhost 5\CertMaker.pdb being installed, open that up in a text/hex editor and there's this string: "removeFiddlerGeneratedCerts". i wonder if that refers to the Fiddler program @ http://www.telerik.com/fiddler that can be used to do mitm SSL


df: CertMaker.dll in C:\Program Files (x86)\Fiddler2\ .. there's also a CertMaker.dll in C:\Program Files\CyberGhost 5\ (altho slightly different file sizes/timestamps), they both contain the string "FiddlerApplication" along with a few others
df: so CyberGhost 5 is using Fiddler 2 for something, or atleast parts of Fiddler 2
df: http://www.telerik.com/fiddler/fiddlercore - "FiddlerCore allows you to integrate HTTP/HTTPS traffic viewing and modification capabilities into your .NET application, without any of the Fiddler UI."


<a href = "http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/MonitorDialupAndVPN">Monitor RAS, VPN or Dialup Connections</a>

To monitor a dialup or VPN connection, open Tools -> Fiddler Options... and click Monitor all connections.

Monitor all connections

<img>http://docs.telerik.com/fiddler/images/MonitorDialupAndVPN/MonitorAllConnections.png</img>

Or, set the "Use automatic configuration script" option in your browser.

To monitor a VPN or dialup connection that is always active (instead of a LAN connection), set the HookConnectionNamed registry value to the name of the connection from Internet Options.



Cross-Certificates

https://msdn.microsoft.com/en-us/library/windows/hardware/ff546307(v=vs.85).aspx

In addition to obtaining an SPC, you must obtain a cross-certificate that is issued by Microsoft. The cross certificate is used to verify that the CA that issued an SPC is a trusted root authority. A cross-certificate is an X.509 certificate issued by a CA that signs the public key for the root certificate of another CA. Cross-certificates allow the system to have a single trusted Microsoft root authority, but also provide the flexibility to extend the chain of trust to commercial CAs that issue SPCs.

Publishers do not have to distribute a cross-certificate with a driver package. The cross-certificate is included with the digital signature for a driver package's catalog file or the signature that is embedded in a driver file. Users who install the driver package do not have to perform any additional configuration steps caused by the use of cross-certificates.

For a list of certification authorities that provide SPCs and for more information about cross-certificates, see Microsoft Cross-Certificates for Windows Vista Kernel Mode Code Signing. Follow the instructions on the certification authority's website on how to obtain and install the SPC and corresponding cross-certificate on the computer with which you will sign a driver. In addition, you must add the SPC information to the Personal certificate store of the local computer that signs drivers. For information about this requirement, see the Installing SPC Information in the Personal Certificate Store.

Installing SPC Information in the Personal Certificate Store

In order to use an SPC to sign a driver in a manner that complies with the kernel-mode code signing policy, the certificate information must first be contained in a Personal Information Exchange (.pfx) file. The information that is contained in the .pfx file must then be added to the Personal certificate store of the local computer that signs a driver.

A CA might issue a .pfx file that contains the necessary certificate information. If so, you can add the .pfx file to the Personal certificate store by following the instructions described in Installing a .pfx File in the Personal Certificate Store.



Managing the Digital Signature or Code Signing Keys
https://msdn.microsoft.com/en-us/library/windows/hardware/ff548699(v=vs.85).aspx

The cryptographic keys that are at the heart of the Authenticode signing process must be well protected and treated with the same care as the publisher's most valuable assets. These keys represent an organization's identity. Any code that is signed with these keys appears to Windows as if it contains a valid digital signature that can be traced to the organization. If the keys are stolen, they could be used to fraudulently sign malicious code and possibly result in the delivery of code that contains Trojan or a virus that appears to come from a legitimate publisher.
