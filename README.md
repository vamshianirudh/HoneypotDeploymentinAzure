<h1>Honeypot Deployment in Azure Cloud</h1>

<h2>Description</h2>
In this project, we are going to creating a honeypot by deploying a Virtual Machine in Microsoft Azure cloud environment.
<br />


<h2>Languages and Utilities Used</h2>

- <b></b> 

<h2>Environments Used </h2>

- <b>Microsoft Azure</b> (22H2)

<h2>Walk-through:</h2>
We need to first create a free microsoft azure account with which you get your first $200(credits) for deploying virtual instance for free. You can follow the steps provided to create your first free Azure account by clicking on the link provided below.

#### [Azure Portal](https://azure.microsoft.com/en-us/free/)

Once you have successfully signed up your Azure account, you should see the home page which looks like this:

<p align="center">
<br/>
<img src="https://imgur.com/FwFeKzM.png" height="80%" width="80%" alt="Windows Azure Home"/>
<br />

After successfully launching the Windows image in the Virtual image, inorder to make a vulnerability assessment we need to make the system more vulnerable. We can make our system vulnerable by turning off some important system settings like system updates, windows firewall and uninstalling any important updates etc.

Inorder to turn off the settings which we have mentioned we need to navigate to the settings in the Windows search bar and follow as guided:



<p align="center">
<br/>
<img src="https://imgur.com/CFhG8Qf.png" height="80%" width="80%" alt="Windows Search"/>
<br />

<br/>
<img src="https://imgur.com/BrtY7bW.png" height="80%" width="80%" alt="Windows Updates and Security"/>
<br />

Our first objective is to pause the automatic updates so that the system doesn't receive any system and security updates. We can do that by extending the date of pause as long as possible, which effectively disables the updates.

<p align="center">
<br/>
<img src="https://imgur.com/8ufVqtd.png" height="80%" width="80%" alt="Advanced options"/>
<br />

You can extend the pause updates by choosing the longest date possible and also make sure to turn off the update options which are set to on by default.

<p align="center">
<br/>
<img src="https://imgur.com/IAIRcwS.png" height="80%" width="80%" alt="Pause Updates"/>
<br />

Now we have to also make sure that the pre-installed updates are uninstalled so that security patches are removed the system and to make sure the Nessus scanner works more effectively.

<p align="center">
<br/>
<img src="https://imgur.com/OGgDV7i.png" height="80%" width="80%" alt="View Update History"/>
<br />

<br/>
<img src="https://imgur.com/9OtyA8J.png" height="80%" width="80%" alt="Uninstall updates"/>
<br />

Some updates cannot be uninstalled. To make sure that we can uninstall the updates, select the individual update and see whether you can find the uninstall option at the top. If you cannot find the uninstall option after choosing the update, it means that the particular update cannot be uninstalled.

<p align="center">
<br/>
<img src="https://imgur.com/qYyNQ5z.png" height="80%" width="80%" alt="Uninstalling updates"/>
<br />

Now we need to disable the Windows Defender Firewall.

<p align="center">
<br/>
<img src="https://imgur.com/eRnU5E7.png" height="80%" width="80%" alt="Windows Defender Firewall"/>
<br />

<br/>
<img src="https://imgur.com/dVU5Dc7.png" height="80%" width="80%" alt="Windows Defender Firewall"/>
<br />

<br/>
<img src="https://imgur.com/Jn82and.png" height="80%" width="80%" alt="Windows Defender Firewall"/>

Make sure you set all the firewall profiles off. 

<p align="center">
<br/>
<img src="https://imgur.com/ZjUQyKp.png" height="80%" width="80%" alt="Windows Defender Firewall"/>
<br />

Finally we need to make sure that the network the virtual machine is on the same network as the Nessus machine that we are about to create. Configure the following settings on your virtual machine and change your adapter setting to "Host-only Adapter" (as it is only option that's working for me):

<p align="center">
<br/>
<img src="https://imgur.com/a1pi2S9.png" height="80%" width="80%" alt="Network Adapter Settings"/>
<br />
 <br/>
<img src="https://imgur.com/HlfI4u6.png" height="80%" width="80%" alt="Network Adapter Settings"/>
<br />
</p>

<h3>Installing Nessus</h3>

Installing Nessus is pretty intuitive as it can get. By clicking on the link provided, you will be redirected to the Nessus Essentials Registration page where you must complete the registration to download the Nessus. After downloading the Nessus and completing the setup wizard, activation code will be sent to your registered email. Use the activation code and let the rest of plugins for Nessus download. 

Note: We will be downloading the Nessus on your personal machine to run vulnerability scans, not your virtual machine which you have setup.

#### [Nessus Essentials Registration](https://www.tenable.com/products/nessus/nessus-essentials?action=register)

<h3>Configuring Nessus for Scanning</h3>

Once the setup is done, we need to configure the Nessus to perform on target ip or network. Choose the "Create New Scan" option from the My Scans and add the Virtual Machine IP to run the scan. 

Nessus does provide a wide range of scan options even with the free edition so feel free to try around different scans. But for the current project, we are focusing on the "Basic Network Scan" scan to be run on the lab environment.

<p align="center">
<br/>
<img src="https://imgur.com/jteO85q.png" height="80%" width="80%" alt="Nessus Configuration"/>
<br />

 <br/>
<img src="https://imgur.com/QLNOXta.png" height="80%" width="80%" alt="Nessus Configuration"/>
<br />

The target IP address should be provided to Nessus in order to perform a vulnerability scan.

<p align="center">
<br/>
<img src="https://imgur.com/dqDBDGv.png" height="80%" width="80%" alt="Nessus Configuration"/>
<br />

You can also find two other options right next the Settings which being Credentials and Plugins

Credentials gives you an option to perform a vulnerable target by providing it's login credentials. It basically gives you a more comprehensive assessment of the target and provides more vulnerabilities which other wise cannot be found.

Plugins provide additional functionality based the type of scan you wanna perform. For example, you can choose Cisco Database plugin family to add more functionality to your scans if you are performing it on a Cisco database etc.

After saving the target IP address, we can now run a vulnerability scan on the target device.
</p>

<h3>Nessus Initial Scan</h3>

Now that we have successfully configured our scan, we can now start our scan by clicking on the play button.
<p align="center">
<br/>
<img src="https://imgur.com/iAOIkKg.png" height="80%" width="80%" alt="Nessus Initial Scan"/>
<br />

After a successful scan, we should see something like this.

<p align="center">
<br/>
<img src="https://imgur.com/CVN8IfU.png" height="80%" width="80%" alt="Nessus Initial Scan"/>
<br />

Nessus provides you vulnerabilities based on their severity and if we notice carefully, we found have a medium severity vulnerability. Let's take a deeper dive into the vulnerability by clicking on it.

Nessus provides you a brief description about the issue and also solution for the vulnerability that is been discovered. It also shows the availability of exploits for the discovered exploit.

<p align="center">
<br/>
<img src="https://imgur.com/hhRqTcE.png" height="80%" width="80%" alt="Nessus Initial Scan"/>
<br />

<h3>Configuration of Credentials for Credential Scan</h3>

As discussed earlier, with credentials Nessus can perform a more comprehensive scan on the target network. Follow the pictures to configure the credentials for credential scan:

<p align="center">
<br/>
<img src="https://imgur.com/tNaOlau.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

Since we are performing credential scan on a Windows VM, choose the windows machine and provide the required credentials of the admin account. There are multiple authentication methods you can use when using the credential scan. For now, choose the "Password" option and save once you have entered the credentials.

<p align="center">
<br/>
<img src="https://imgur.com/u3Dsvqm.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

However, you may receive an notification when you try to run a scan saying "The account used does not have necessary privileges". This is because in windows a non-default administrator is not added to the local group administrators and does not have the appropriate rights to access the system rights. For the credential scan to work, we need to configure some additional settings in the Windows VM as follows:

<p align="center">
<br/>
<img src="https://imgur.com/ApPHx0T.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

<p align="center">
<br/>
<img src="https://imgur.com/ShKHI03.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

We need to change the startup type to "Automatic", which will allow you to remotely connect to registry database and perform different operations.

<p align="center">
<br/>
<img src="https://imgur.com/duYRj8x.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

<br/>
<img src="https://imgur.com/Xhx1Zey.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

<br/>
<img src="https://imgur.com/JilpD5c.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

Go to Registry Editor and follow this path: 

HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > Policies > System

Right click on the empty space inside the System folder and choose "DWORD (32-bit world) Value" and name it "LocalAccountTokenFilterPolicy". Make sure you rename exactly the same because any variations will cause the Windows to ignore the registry value.

Now double click on the newly created DWORD value and to make sure it's turned on, change the value data from 0 to 1.

The "LocalAccountTokenFilterPolicy" registry value which allows non-administrative accounts to access administrative resources on the system when using remote procedure call.

<p align="center">
<br/>
<img src="https://imgur.com/S0l3kdH.png" height="80%" width="80%" alt="Configuring Credential Scan"/>
<br />

Once you have made all the necessary changes, restart the device to make sure the changes have been applied. With this we can now perform a credential scan on the target.

<h3>Performing Credential Scan</h3>

Just like the Basic Network Scan, click on the play button and wait for some time to Nessus to actually complete the scan. 

As we can see, there are mutiple vulnerabilities are discovered and a critical vulnerbility has beend discovered as well. This shows that with credential scan will provide you a more in depth scan into our target.

<p align="center">
<br/>
<img src="https://imgur.com/kZLqAt7.png" height="80%" width="80%" alt="Performing Credential Scan"/>
<br />

<p align="center">
<br/>
<img src="https://imgur.com/PWgBxV7.png" height="80%" width="80%" alt="Performing Credential Scan"/>
<br />

<h3>Introducing Vulnerable Software</h3>

Inorder to download any vulnerable software into our VM, we need to have internet access. For we need to change adapter settings to "Bridged Adapter" and change back to "Host-only" once you are done with downloading the vulnerable software.

I have decided to download the older version of 7zip for our demonstration.Let's also introduce the famous "Log4j" vulnerability by installing a 2019 Minecraft server into our system. Once the outdated software has been downloaded and installed, perform another round of scan and we can see that new vulnerabilities are introduced into our machine.

As we can see that Nessus has detected the vulnerabilities associated with the older version of software we have installed into the target system.

<p align="center">
<br/>
<img src="https://imgur.com/hPFBtaB.png" height="80%" width="80%" alt="Vulnerable Software Scan"/>
<br />

There's an excellent feature provided by Nessus, where you can download a report of all the discovered vulnerabilties. This report can be used as an comprehensive document about the discovered vulnerabilities.

<p align="center">
<br/>
<img src="https://imgur.com/oCStvCu.png" height="80%" width="80%" alt="Vulnerable Software Scan"/>
<br />

<p align="center">
<br/>
<img src="https://imgur.com/9yhm2HY.png" height="80%" width="80%" alt="Vulnerable Software Scan"/>
<br />

<h3>Remediation of Discovered Vulnerabilities</h3>

Now that we have discovered all the vulnerbilities, we need to follow the remediations provided by the Nessus. The remediations can viewed when you click on the particular vulnerability you wanna address. The basic security configurations like turning on the windows updates, deleting or updating any vulnerable software etc., should do the trick.
</p>

<h3>Conclusion</h3>
With a final scan run on the target, we can confirm that all the discovered vulnerabilities have been patched up and there are no vulnerabilities other than "info" based ones. That concludes the end of this project.
<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
