

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
