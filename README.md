# Configuring-Azure-Point-to-site-virtual-private-network-VPN-
In this project, I configured a point-to-site VPN connection for client devices to connect to an existing Azure virtual network I created named vnet2.

<h2>Environments Used </h2>

- <b>Azure Portal</b>
- <b>Powershell</b> 


<h2>Project walk-through:</h2>

<p align="center">
I started this project by creating the virtual network gateway. I then to the Azure portal and started the creation of a virtual network gateway: <br/>
<img src="https://i.imgur.com/azm0B9G.png" height="80%" width="80%" />
<br />
<br />
<br />
I filled in all the required fields as seen in the image below, making sure I named the gateway P2S-GW and selected an existing virtual network named vnet2 as well as disabled active-active mode as it wouldn’t be needed for this project:  <br/>
<img src="https://i.imgur.com/TSLB3z6.png" height="80%" width="80%" />
<img src="https://i.imgur.com/mgClp9A.png" height="80%" width="80%" />
<br />
<br />
<br />
I then waited for the review and creation of P2S-GW:  <br/>
<img src="https://i.imgur.com/S01SuoQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/CGH2OGy.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/MkfOKhz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Once the deployment was complete I started with generating a self-signed root certificate named P2SRootCert using Powershell ISE:  <br/>
<img src="https://i.imgur.com/ya2Y7jq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br /> 
and then I generated the VPN Client Certificate Name “P2SchlidCert”, using PowerShell ISE:  <br/>
<img src="https://i.imgur.com/fyU0Hkz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
I then ran the certmgr command in Powershell to open the manage computer certificate settings window and verified the creation of the certificates:  <br/>
<img src="https://i.imgur.com/XDaDpAt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then started exporting the root certificate by right-clicking it, selecting all tasks, then selecting export which opened the following prompts:  <br/>
<img src="https://i.imgur.com/aTgfvbY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then followed the prompts keeping the default selected:  <br/>
<img src="https://i.imgur.com/sIfABWQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br /> 
<br />
<br />
and then selected base 64 encoded X.509 (.CER):  <br/>
<img src="https://i.imgur.com/NO8Oue3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I named it Point to Site Root Cert and continued following the prompts selecting next, finish and ok:  <br/>
<img src="https://i.imgur.com/M2yIQr4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/qCUNF7N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/LI9DAbo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then went to the folder that I saved the cert in and opened it with notepad, then copied the text between BEGIN CERTIFICATE and END CERTIFICATE:  <br/>
<img src="https://i.imgur.com/UMuH7EI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/bINzLRf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
Once I copied the text I went back to the portal. I went to the virtual network gateway then under point-to-site configuration and clicked configure now:  <br/>
<img src="https://i.imgur.com/XPerKuW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
and added an address pool of 172.16.31.0/24, selected IKEv2 and SSTP for tunnelling type so that both Windows and Mac devices can connect via the gateway:  <br/>
<img src="https://i.imgur.com/tozRhaP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then pasted the text I copied from my Root Certificate (P2SRootCert) in the “Public certificate data” field and named it P2SRootCert:  <br/>
<img src="https://i.imgur.com/tozRhaP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then downloaded the VPN client:  <br/>
<img src="https://i.imgur.com/2MYcT0s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
Once downloaded I went to the zip file and extracted the folder, so that I could install the VPN Client for vnet2 on my local file to test if it worked:  <br/>
<img src="https://i.imgur.com/0is7Ejt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I selected Windows amd64 because that is what my local system runs, then selected VpnClientSetupAmd64:  <br/>
<img src="https://i.imgur.com/HyWY73U.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then selected “More info” then “run anyways”:  <br/>
<img src="https://i.imgur.com/jUmgIi7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/wrOxHWd.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
then yes:  <br/>
<img src="https://i.imgur.com/7gs3Pd2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
On my local computer, I went to the search bar, typed in “VPN settings” and then selected it:  <br/>
<img src="https://i.imgur.com/yhXwTwa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/3f4qm8H.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I then select vnet2 then “connect” on vnet2:  <br/>
<img src="https://i.imgur.com/sgB2iRE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
Then followed the prompt and selected continue:  <br/>
<img src="https://i.imgur.com/R21xspI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /> 
<br />
I successfully connected to vnet2 from my local device which was the goal of this project:  <br/>
<img src="https://i.imgur.com/SrrtgIt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
