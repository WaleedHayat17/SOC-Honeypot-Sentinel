🛡️ Azure SOC Honeypot & Sentinel Project



<img width="403" alt="Screenshot 2025-05-03 at 11 54 47 PM" src="https://github.com/user-attachments/assets/b8c15c9c-88ff-429e-b2f1-eaecd3eef525" />




"Where Blue Team meets the Cloud ☁️”
A hands-on cybersecurity walkthrough using Azure Virtual Machines, Microsoft Sentinel, and KQL to simulate a real-world SOC investigation.

🧠 What Is This?

Welcome to my Azure SOC Honeypot Project! This lab is all about exploring how attackers behave when they encounter a vulnerable system —and how defenders can detect and investigate that behavior using Microsoft Sentinel, Log Analytics, and KQL. Think of it as your own digital battleground: I set up the bait (a honeypot VM), tracked the incoming attacks, and then visualized them on a global map. 

I’ve included screenshots at each step 📸 so you can follow along visually and build your own version with ease!

🎯 Learning Objectives

By completing this project, you'll gain hands-on experience with:

Deploying and configuring an Azure Windows VM (honeypot)
Creating a Log Analytics Workspace and integrating Sentinel
Writing KQL queries to filter and investigate logs
Using a custom PowerShell script to enrich logs with GeoIP data
Visualizing attack data on a real-time world map
Understanding the value of a cloud-based SIEM solution

Tools & Tech Used:

Microsoft Azure 
Azure Sentinel (SIEM)
Log Analytics Workspace
Workbooks (for visualizing logs on a map)
PowerShell (custom script used for log automation)
ipgeolocation.io (API used to enrich logs with location data)
Remote Desktop Protocol (RDP)
Windows Event Viewer
KQL (Kusto Query Language)
Step-by-Step Breakdown (With Screenshots!)





<img width="370" alt="Screenshot 2025-05-03 at 9 39 14 PM" src="https://github.com/user-attachments/assets/5830c36c-73ec-4d00-8fc4-e8c709c78a7d" />




Each step includes real screenshots from my environment to guide you through the setup 👇

🔹 Step 1: Azure Setup & Free Credits
Create a free Azure account (comes with $200 credit!)
Log into portal.azure.com


<img width="1440" alt="Screenshot 2025-05-01 at 8 10 17 PM" src="https://github.com/user-attachments/assets/a0a89e94-e5f1-4275-a220-f8eee3c17507" />



🖥️ Step 2: Deploying the Honeypot VM
Created a new Windows 10 Pro VM
Exposed RDP Port 3389 (spoiler: attackers love this)
Configured Network Security Group (NSG) to allow any inbound traffic
Gave it a cool name like honeypot-vm and deployed it in (US) West 3
💡 Make sure to note your admin credentials — you’ll need them to RDP in later!


<img width="1440" alt="Screenshot 2025-05-01 at 8 13 06 PM" src="https://github.com/user-attachments/assets/6b361223-1275-4367-96c0-7fb69dcf6582" />


<img width="1440" alt="Screenshot 2025-05-01 at 8 15 59 PM" src="https://github.com/user-attachments/assets/39df8910-32fd-4030-b03d-06c44f7ddcd7" />


<img width="1440" alt="Screenshot 2025-05-01 at 8 16 05 PM" src="https://github.com/user-attachments/assets/807755e2-23a0-4d5f-8a1d-a770b7011b5b" />


<img width="1440" alt="Screenshot 2025-05-01 at 8 19 33 PM" src="https://github.com/user-attachments/assets/ad72411c-3a97-4a02-b62e-a9e580cb8bdb" />



<img width="1440" alt="Screenshot 2025-05-01 at 8 21 15 PM" src="https://github.com/user-attachments/assets/281bcda6-ae26-4179-b91a-b6da6e225b89" />





🧱 Step 3: Log Analytics Workspace
Created a Log Analytics Workspace (LAW) in the same region and resource group
Named mine something like honeypot-law
This will collect all logs from the VM 🧩



<img width="707" alt="Screenshot 2025-05-04 at 12 44 25 AM" src="https://github.com/user-attachments/assets/df4e95c4-2b67-41be-ad8e-f0b8cd5954c0" />



🛡️ Step 4: Microsoft Defender for Cloud
Enabled Defender and configured it to collect All Events
Activated Foundational CSPM and Servers protection

<img width="1440" alt="Screenshot 2025-05-01 at 8 24 25 PM" src="https://github.com/user-attachments/assets/d0b82580-8d70-4e35-9257-9c4b63c9450f" />


<img width="1440" alt="Screenshot 2025-05-01 at 8 25 08 PM" src="https://github.com/user-attachments/assets/e5a38440-3894-4cb0-87ac-391cf3bd4e05" />

<img width="1440" alt="Screenshot 2025-05-01 at 8 25 32 PM" src="https://github.com/user-attachments/assets/eb7916d6-5e86-4f81-a9fa-de63fd8d7818" />


🔗 Step 5: Connect VM to LAW
Linked the VM to the Log Analytics Workspace
This allows Event Viewer logs to flow directly into Sentinel


<img width="1440" alt="Screenshot 2025-05-01 at 8 27 27 PM" src="https://github.com/user-attachments/assets/331d5d03-3037-47e9-a86e-8345b57ed45f" />


👮 Step 6: Enable Sentinel
Enabled Microsoft Sentinel on the LAW
This is our main SIEM dashboard for analysis and visualization

<img width="1440" alt="Screenshot 2025-05-01 at 8 30 34 PM" src="https://github.com/user-attachments/assets/45a67911-6f45-4acd-a072-f77618051f6b" />


Step 7: Disable the VM Firewall (Temporary for Testing)

To verify if your virtual machine's firewall is active, we’ll first check network connectivity by pinging the machine’s IP. This is a quick way to see if the device is reachable and responding over the network. The ping tool is a simple but powerful command used to test that connection.

On Windows:

Open Command Prompt
Hit the Windows key, type cmd, and hit Enter.
Run the Ping Command
In the command prompt window, type the following and press Enter:
nginx
Copy
Edit
ping 20.186.58.174
On macOS or Linux:

Launch Terminal
On macOS, go to Applications > Utilities > Terminal
On Linux, press Ctrl + Alt + T
Run the Ping Command
nginx
Copy
Edit
ping 20.186.58.174
What to Look For:

The system will start sending packets to the IP address you entered. You’ll see a response time if the VM is reachable. This confirms that it’s online and the firewall may be open. If you’re getting timeouts or errors, the firewall might be blocking traffic.

To stop the ping loop:

On Windows/macOS/Linux: Press Ctrl + C
(You can also try Ctrl + Z but Ctrl + C is more standard for terminating the command.)


<img width="485" alt="Screenshot 2025-05-01 at 8 37 47 PM" src="https://github.com/user-attachments/assets/cf2a7c6e-22fa-4a1f-8584-da06493c0c86" />

Firewall Is Blocking Pings — Let’s Turn It Off

Right now, our honeypot VM is set to reject incoming ping requests, which is expected behavior if the firewall is on. To proceed with testing or setup, we’ll temporarily disable the firewall.

Here’s how to do that:

Find Your Honeypot VM
Go to your list of Virtual Machines and look for the one labeled honeypot-vm.
Copy the IP Address
Grab the public IP of that VM — we’ll need it to connect.
Connect via RDP
Use the same login credentials from step 2.
If you’re on Windows, just search for Remote Desktop Connection and open it.
On Mac, download Microsoft Remote Desktop from the App Store or use any other RDP-compatible software.
Handle Prompts
You might get a certificate warning — go ahead and accept it.
When asked about privacy settings, select No for all.
Access Firewall Settings
Click Start and type: wf.msc, then hit Enter.
This will open Windows Defender Firewall with Advanced Security.
Disable Firewall Profiles
In the left panel, click on Windows Defender Firewall Properties.
For Domain Profile, Private Profile, and Public Profile, switch Firewall State to Off.
Click Apply, then OK.
Test Connectivity

Now that the firewall is off, go back to your host machine and test if the VM is reachable:

nginx
Copy
Edit
ping -t 20.186.58.174
Use your actual VM’s IP address in place of this example. The -t option keeps the ping going until you stop it manually — use Ctrl + C to stop it.


<img width="996" alt="Screenshot 2025-05-04 at 12 54 24 AM" src="https://github.com/user-attachments/assets/a624b02e-f413-491a-a157-4b63e667aa40" />
Ping successful :)



Step 8: Automating Security Log Exports

Now that the firewall’s off and the VM is reachable, let’s set up automatic exporting for security logs using a PowerShell script.

Here’s what to do:

Open PowerShell ISE in the VM
Inside your virtual machine, hit Start, type PowerShell ISE, and launch it.
Open Microsoft Edge (Optional Step)
You can open Edge to grab the script — no need to sign in or sync anything.
Get the PowerShell Script
Copy the automation script (originally written by Josh Madakor) — this will handle the log exporting.
Create a New Script in PowerShell ISE
In PowerShell ISE, click File > New, then paste the entire script into the editor window.
Save the Script
Give it a recognizable name like log_exporter.ps1, and save it to the desktop for easy access.

<img width="1440" alt="Screenshot 2025-05-01 at 10 09 11 PM" src="https://github.com/user-attachments/assets/5583442b-cf62-428c-a0c6-3379c2b33a47" />


Step 8 (continued): Set Up API for Location Logging

To enhance your log exporter, you’ll need an API key from ipgeolocation.io — this lets the script map IP addresses to physical locations.

Create an Account on ipgeolocation.io
Go to:
🔗 https://ipgeolocation.io
They offer 1,000 free API calls per day
If you need more, they have a $15/month plan with a 150,000 call cap
Copy Your API Key
After signing up and logging in, you’ll see your API key in the dashboard. Copy it.
Insert API Key into the Script
In the PowerShell script you saved earlier, find line 2 and replace the placeholder with your real key:
powershell
Copy
Edit
$API_KEY = "<your_actual_api_key>"
Save the Updated Script
Click File > Save in PowerShell ISE to save your changes.
Run the Script
Hit the green play button in PowerShell ISE to start the script — this will begin generating and exporting log data continuously.

<img width="995" alt="Screenshot 2025-05-04 at 1 01 16 AM" src="https://github.com/user-attachments/assets/d1b5589e-7dd2-4cd2-9ad0-1039330947ef" />
The script pulls event data straight from Windows Event Viewer and sends the IPs to the IP Geolocation service. From there, it grabs the latitude and longitude and saves everything into a new log file called failed_rdp.log, which gets stored at:
C:\ProgramData\failed_rdp.log



Grabbed the failed_rdp.log file from the VM
Uploaded it to Log Analytics as a custom log
This lets us analyze enriched GeoIP data alongside other logs

<img width="1440" alt="Screenshot 2025-05-01 at 9 09 51 PM" src="https://github.com/user-attachments/assets/4c02c0b9-d693-4da9-a08f-47a00de10211" />


Step 9: Creating a Custom Log in Log Analytics Workspace

Now that the failed_rdp.log file is being generated, we’ll bring that data — including the geolocation info — into Azure Sentinel by setting up a custom log.

On the VM, hit Start, search Run, and open it.
Type in:
makefile
Copy
Edit
C:\ProgramData
Find the file named failed_rdp, open it, and hit CTRL + A to select everything, then CTRL + C to copy it.
On your host machine, open Notepad and paste the contents.
Save the file to your desktop as:
lua
Copy
Edit
failed_rdp.log
⚠️ Important: Make sure it's saved as a .txt file, not .rtf — I ran into formatting issues when using rich text.
In Azure, go to:
Log Analytics Workspaces → your workspace (e.g., honeypot-law) → Custom Logs → click + Add Custom Log
Sample
Select the failed_rdp.log file from your desktop
Click Next
Record Delimiter
Just review the log structure and hit Next
Collection Paths
Type: Windows
Path:
lua
Copy
Edit
C:\ProgramData\failed_rdp.log
Details
Give the log a name like:
nginx
Copy
Edit
FAILED_RDP_WITH_GEO
Add a short description if you’d like
Then click Create

<img width="1440" alt="Screenshot 2025-05-01 at 9 47 23 PM" src="https://github.com/user-attachments/assets/4e825bc9-fa15-4402-8839-1b5c7ed9d7bc" />



Step 10: Run a Query & Extract Fields from the Custom Log

Head over to your Log Analytics Workspace — in this case, honeypot-law — and go to Logs.

Now that your custom log is live, you can start running KQL (Kusto Query Language) queries to filter and pull out data like latitude, longitude, destination host, and more.

Just a heads-up: as of March 31st, 2023, Microsoft no longer supports creating new custom fields the old way — everything now runs through KQL. If you're interested in the details, check this out:
🔗 Microsoft’s announcement on custom fields and KQL

To try it out, copy and paste the sample query into the editor and hit Run.

FAILED_RDP_WITH_GEO_CL 
| extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData)
| where destination != "samplehost"
| where sourcehost != ""
| summarize event_count=count() by timestamp, label, country, state, sourcehost, username, destination, longitude, latitude
Kusto Query Language (KQL) is what we use to pull and analyze log data from Azure Log Analytics or Azure Data Explorer. It’s a powerful tool that makes it easy to filter, break down, and even visualize your data. Once you get the hang of it, writing queries feels pretty natural, it's designed to be readable and straightforward, even when doing more complex stuff.

<img width="1440" alt="Screenshot 2025-04-30 at 2 57 11 AM" src="https://github.com/user-attachments/assets/fa40695b-7b10-4dae-9b9e-3325239255c2" />

Step 11: Build a Global Attack Map in Microsoft Sentinel

Jump into Microsoft Sentinel and head to the Overview to see any active events.

Go to Workbooks → click Add workbook, then hit Edit to start customizing it.

First, clear out the default widgets (click the three dots on each and select Remove).

Next, hit Add → Add query.

Paste in the KQL query from earlier (or use a new one if you're tweaking things), then Run Query.

Failed_RDP_Geolocation_CL
| parse RawData with * "latitude:" Latitude ",longitude:" Longitude ",destinationhost:" DestinationHost ",username:" Username ",sourcehost:" Sourcehost ",state:" State ", country:" Country ",label:" Label ",timestamp:" Timestamp
| where DestinationHost != "samplehost"
| where Sourcehost != ""
| summarize event_count=count() by Sourcehost, Latitude, Longitude, Country, Label, DestinationHost

Once your results load, switch the visualization type to Map using the drop-down.

Now configure your map:

🧭 Layout Settings
Location info using: Latitude/Longitude
Latitude: latitude
Longitude: longitude
Size by: event_count

🎨 Color Settings
Coloring Type: Heatmap
Color by: event_count
Aggregation for color: Sum of Values
Color palette: Green to Red

📊 Metric Settings
Metric Label: label
Metric Value: event_count
Once everything looks right, click Apply, then Save and Close.

Name it "Failed RDP International Map" and save it in the same region and resource group (honeypot-lab).

You can refresh the map periodically to keep track of new failed RDP attempts showing up around the world.

<img width="1440" alt="Screenshot 2025-05-01 at 10 01 00 PM" src="https://github.com/user-attachments/assets/4784bc7b-9153-4cf6-920e-041de7af169a" />
The Event Viewer highlights all the failed RDP login attempts on the system. These show up under Event ID: 4625, which specifically flags unsuccessful logon events — basically, someone tried to connect via Remote Desktop and didn’t get in.


<img width="1440" alt="Screenshot 2025-05-01 at 10 08 57 PM" src="https://github.com/user-attachments/assets/1ac67e68-fa90-4469-bf6d-58256ea7bdc1" />
The data is pulled and processed using a custom PowerShell script that taps into a third-party API, this is what adds the extra details like location info to the logs.




<img width="1440" alt="Screenshot 2025-04-30 at 3 24 10 AM" src="https://github.com/user-attachments/assets/a17490bb-e361-48fc-8592-5f9a60e7a3b2" />
Note: The map is focused solely on failed RDP login attempts, it won’t display other types of attacks your VM might be hit with. However, after letting it run for 24 hours, you’ll start to see a noticeable difference on the attack map, with more red zones lighting up as failed attempts from around the world get logged and visualized.
<img width="1440" alt="Screenshot 2025-05-01 at 10 07 31 PM" src="https://github.com/user-attachments/assets/52771e49-b14d-4862-b18b-f19ac1043022" />

Step 12: Shutting Down Resources

IMPORTANT: Don’t skip this part!
Head over to “Resource groups” and find the one you created (honeypot-lab).
Type in the resource group name to confirm you want everything removed.
Make sure to check the box that says “Apply force delete for selected Virtual machines and Virtual machine scale sets.”
Then go ahead and click Delete.
<img width="1440" alt="Screenshot 2025-05-01 at 10 13 04 PM" src="https://github.com/user-attachments/assets/a95f7473-04fb-4bc1-bfb4-660c3ec84919" />

<img width="1440" alt="Screenshot 2025-05-03 at 9 21 06 PM" src="https://github.com/user-attachments/assets/4f1e9ed5-c5bf-4ab2-9935-c8eeb004467c" />
If you don’t remove the resources, they’ll keep running and start using up your free credits, which can lead to unexpected charges. Don’t forget to cancel your subscription as well to avoid any ongoing costs. (Yes, Azure does charge if the subscription is still active, even if no resources are running.)

🎉 Final Thoughts

This lab really helped me understand what it’s like to think like a Blue Teamer in a real-world environment. Seeing actual attack attempts come in was both scary and fascinating, and building visual dashboards made it feel alive.

If you're trying to break into cybersecurity or just want to get your hands dirty with SIEM tools, this is the perfect place to start 

📸 Screenshots

All screenshots for each step are included in the project folder to guide you along the way!

Questions or Feedback?

Shoot me a message, always happy to connect with fellow cyber defenders! 🛡️
(You can also fork this and try your own twist. Make it yours.)
