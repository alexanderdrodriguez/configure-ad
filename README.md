<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<p>To start this Active Directory tutorial we are going to create two Virtual Machines in Microsoft Azure.
</p>
<p>
</p>
<br />
<p>Section 1: Select the “Virtual Machines” option in Azure -> Select “Create Virtual Machine” -> Create a new Resource Group -> Name the VM “DC-1” -> Select “Windows Server 2022” as the Image -> Select “2vcpus, 16 GiB memory” for the “Size” option -> Create a username and password for the administrator account section -> Click “Review + create”</p>
<img src="https://i.gyazo.com/e6a9e290e25895dc34d4e02d354ce40b.png">
<img src="https://i.gyazo.com/d2fee5c127c16f240c64fc22addabeb3.png">
<img src="https://i.gyazo.com/30ddb13bc9a509331963818d763f0be1.png">
<img src="https://i.gyazo.com/d0aa64b7d15ae739868fcbe3c515a09f.png">
<img src="https://i.gyazo.com/142bdf7bba1856b23b5d6bc7287ff0ce.png">
<img src="https://i.gyazo.com/82b68c920f205e3635850a113b6d3ea7.png">
<p>
<p>Section 2: Once the VM is finished being created go to “Virtual Machines” -> Select “Networking” -> Select the Network Interfaces name -> Select “IP configurations” -> Select the Private IP address number -> Change the “Assignment” from “Dynamic” to “Static”</p>
<img src="https://i.gyazo.com/5189f0830049f96b8ea7a0c4355cba4e.png">
<img src="https://i.gyazo.com/086ace2f525faa3a7f8350d446a8af5f.png">
<img src="https://i.gyazo.com/4b7e95fe3c54d9c14de1beba915c441f.png">
<img src="https://i.gyazo.com/79edeede8dc27f725e7c5c4366bc94eb.png">
<img src="https://i.gyazo.com/82b2f02c71057357183691c34bb9c097.png">
<p>Section 3: Select the “Virtual Machines” option in Azure ->  Select “Create Virtual Machine” -> Select the same Resource Group you used to create the “DC-1” VM -> Name the VM “Client-1” -> Select “Windows 10 Pro” as the Image -> Select “2vcpus, 16 GiB memory” for the “Size” option -> Create a username and password for the administrator account section -> Click “Review + create” -> Review both of the VMs properties information when “Client-1” is done being created to ensure that they are in the same “Virtual network/subnet</p>
<img src="https://i.gyazo.com/42530219f21d00948f71f5b2f10e4639.png">
<img src="https://i.gyazo.com/aad925bf3119f50a3fc73bcaf1c0179a.png">
<img src="https://i.gyazo.com/c9fd3e9c824d2313dd47dadd523fb070.png">
<img src="https://i.gyazo.com/33a58fc9bda355e1392c241498ba7c69.png">
<img src="https://i.gyazo.com/925f7743bc5da56465ef21a801465dda.png">
<p>Section 4: Login to the “Client-1” VM using Remote Desktop Connection and the VMs public IP address and administrator account details -> Open command prompt in the “Client-1” Windows 10 VM -> Ping DC-1’s private IP address with the command ping -t <ip address> -> Login to the “DC-1” VM using Remote Desktop Connection and the VMs public IP address and administrator account details -> Search “Windows firewall” into the Windows 10 search bar and select the option “Windows Defender Firewall” -> Click “Advanced settings” -> Select Inbound Rules -> Sort by “Protocol” -> Enable both of the options that have “ICMP Echo Request” in its name -> Check Client-1 to see that the ping is now replying</p>
<img src="https://i.gyazo.com/e4c5cb0d06a36fdfe7ba92f475f3c8c9.png">
<img src="https://i.gyazo.com/95b326db5c13069115cd39fc63ac9bdb.png">
<img src="https://i.gyazo.com/4c957e955bd196a3e22fdff5f76616c1.png">
<img src="https://i.gyazo.com/1bc4737ed9f42402654a510e5b10ffbf.png">
<img src="https://i.gyazo.com/f23a167b54da56e650c42865ffd9f0fa.png">
<img src="https://i.gyazo.com/d7b8aa39253ad6bb9373f95fc04f9ccf.png">
<img src="https://i.gyazo.com/5836b6c5fee146d1da607f5e5d952524.png">
<img src="https://i.gyazo.com/643d195d5c376f8ab07b4cd87357a027.png">
<img src="https://i.gyazo.com/fab7aa0cbeb4d33b8af0c3e972d875d6.png">
<img src="https://i.gyazo.com/2eac7fe96eeca8178cd97d05b119856f.png">
<img src="https://i.gyazo.com/927900553ef274cf44e4c87f9ef8610d.png">
<img src="https://i.gyazo.com/2c426c65fb8632beccf55065a8649382.png">
<p>Section 5: Open the DC-1 virtual machine -> Go to Server Manager and select “Manage” and then “Add Roles and Features” -> Click next until you get to “Server Roles” -> Select only “Active Directory Domain Services and then next -> Click next until you get to “Confirmation” and then select “Install” -> Once it is done being installed select the flag at the top of the Server Manager Dashboard -> Click “Promote this server to a domain controller” -> Select “Add a new forest” -> Write “mydomain.com” as the Root domain name and select Next -> Use Password1 as the DRSM password then click next -> Continue to click next and then click install (Note: The VM will now restart to complete the installation) -> Log back into DC-1 but you must now login as username: mydomain.com\labuser and the password remains the same</p>
<img src="https://i.gyazo.com/002cce0a04acb7e5a6acb87c204f7ca9.png">
<img src="https://i.gyazo.com/7429f203fbc6e96d232e8deeacb1a6b0.png">
<img src="https://i.gyazo.com/bcb02728fb6abd8997b017e222f27564.png">
<img src="https://i.gyazo.com/2b0d4d16cd68c28a531de8cb8daf243d.png">
<img src="https://i.gyazo.com/4f1c4c9992ab8fcad64e04f8bff16408.png">
<img src="https://i.gyazo.com/bc41685accdbfdf8d9d1543264f3f2e2.png">
<img src="https://i.gyazo.com/5251ce4b4b683d7641e4d5621f67d192.png">
<img src="https://i.gyazo.com/0a6eaf91ad9611e6f276fb3f0c97e916.png">
<img src="https://i.gyazo.com/6535686817371af63bd9e08269112ccd.png">
<img src="https://i.gyazo.com/7c31f9fc22750ba9950d9373c4622e9b.png">
<img src="https://i.gyazo.com/18e067bced007e3dbc2b110157a3a2c9.png">
<img src="https://i.gyazo.com/0c9324f96fac859e4854f71d05ef3e70.png">
<img src="https://i.gyazo.com/0a7b004bb24c08d2d76d671f8609377f.png">
<img src="https://i.gyazo.com/d1121eca0c6e5236b2091507f94fff19.png">
<img src="https://i.gyazo.com/6417933072f0b01223a8b29c684f3b9a.png">
<img src="https://i.gyazo.com/7ac566fa9cc2172d7c16210b3e7775e0.png">
