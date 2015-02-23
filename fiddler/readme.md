
It seems unlikely that the fiddler toolset is really malware in any meaningful sense - it's marketed quite obviously (and genuinely) as a testing framework for optimising browser performance and whatnot. That's a big market, sorely in need of these sorts of tools. Doesn't seem nefarious.

However, when one reads through such materials - having been around people who do bad things with tech in various amazingly creative ways - one cannot help but think... "oh heavens, this won't end well."

It won't.

All indications are that cyberghost is using unlicensed fiddler2 code, and a faked-up cert/key set to do code/device signing as root on installed machines... so it's not really fair to blame the fiddler folks for that. And we shouldn't. This is nice tech, built for a real purpose and supported as such. It's a shame it can go wrong so quickly... but these things happen.

So it goes...


https://malwr.com/analysis/YzMwM2VmMTcwMzU2NDk2MmI5YzYzYjJlZmI1ZWU0MDQ/


Here's the fiddler2 framework we're pretty sure is being used in the cyberghost binaries:
http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/ConfigureDotNETApp



To temporarily connect a .NET application to Fiddler, use the GlobalProxySelection class to set a proxy:

GlobalProxySelection.Select = new WebProxy("127.0.0.1", 8888);
Or, specify a proxy inside the yourappname.exe.config file.

If the .NET application is running in your current user account, add the following content inside the configuration section:

<configuration>
 <system.net>
  <defaultProxy>
   <proxy bypassonlocal="false" usesystemdefault="true" />
  </defaultProxy>
 </system.net>
</configuration>
See MSDN for more on this topic.

If the .NET application is running in a different user account (for example, a Windows service), edit the machine.config file:

<!-- The following section is to force use of Fiddler for all applications, including those running in service accounts -->  <system.net>
 <defaultProxy>
  <proxy autoDetect="false" bypassonlocal="false" proxyaddress="http://127.0.0.1:8888" usesystemdefault="false" />
 </defaultProxy>
</system.net>
Or, manually specify the proxy on an individual WebRequest object:

    objRequest = (HttpWebRequest)WebRequest.Create(url);
    objRequest.Proxy= new WebProxy("127.0.0.1", 8888);
Note: Important: Regardless of other settings, .NET will always bypass the Fiddler proxy for URLs containing localhost. So, rather than using localhost, change your code to refer to the machine name. For instance:

This URL will not appear in Fiddler:

http://localhost/X509SignCodeService/X509SigningService.asmx
This URL will appear in Fiddler:

http://mymachine/X509SignCodeService/X509SigningService.asmx
