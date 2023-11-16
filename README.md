# Windows-Forensics-2
I will look at Windows file systems and forensic artifacts in the file systems, guiding us to specific locations harboring artifacts. These artifacts serve as evidential breadcrumbs, elucidating instances of program execution, file and folder interactions, user knowledge, and external device engagements. An additional emphasis is placed on foundational techniques for salvaging deleted files.
Facilitating our endeavors are Eric Zimmerman's tools, adept at parsing information embedded in these artifacts. Registry Explorer and ShellBags Explorer, employed previously, continue as steadfast aids. Introducing Autopsy into our toolkit enhances our capabilities, particularly for specified tasks. This collective arsenal empowers us to unearth and scrutinize forensic artifacts dispersed beyond the confines of the Windows Registry.



Parse the $MFT file placed in C:\users\THM-4n6\Desktop\triage\C\ and analyze it. 

What is the Size of the file located at .\Windows\Security\logs\SceSetupLog.etl

The Windows command to parse this file:

MFTECmd.exe -f "C:\users\THM-4n6\Desktop\triage\C\ $MFT" --csv "C:\Users\THM-4n6\Desktop"


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/0cc375a2-d381-40ad-8333-912a61da8a30)

Open file in Event Viewer: 

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/e5c55d11-a01d-4bda-b704-a72d6f288519)

The file size is  49152


What is the size of the cluster for the volume from which this triage was taken?

The command to parse the $Boot file:
MFTECmd.exe -f "C:\users\THM-4n6\Desktop\triage\C\$Boot" --csv "C:\Users\THM-4n6\Desktop"


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/f2776d9b-9053-41bd-98e8-32afaad18c93)

The cluster size is 4,096

Creating a disk image with Autopsy.


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/60bc0dab-cb4a-43a9-a7ca-c5534f4deeb1)


Create new case

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/fd424c7a-69b6-4fcd-8018-81617921a8c0)


Case information

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/ac21a4eb-4298-4e58-9b3f-3727ff859920)


System will generate a host name on database source

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/ad91020a-1aa0-48dd-98aa-31105ee65659)

Select Disk image or VM file

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/870fe077-58de-4602-829e-9919d8c50377)


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/0b7d1e19-ed57-4986-a51f-beb87c35ab4d)

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/b07bfbbc-3b4e-4b87-ab09-562ed2e8ee92)


Next screen deselect all then click next

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/66003932-f0b3-4056-8a0a-d6bba0d61c32)


Selecting the source shows us the file and the contents of  usb.001

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/672ad6b5-f446-4563-9720-a929c9678408)


There is another xlsx file that was deleted. What is the full name of that file?
The metadata file give us the full file name of the deleted xlsx file


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/027d40b3-b306-4898-9a6d-196b32c2b72c)

TryHackme.xlsx


What is the name of the TXT file that was deleted from the disk?

TryHackMe2.txt


Recover the TXT file from Question #2. What was written in this txt file?

To recover the deleted file we need to do an extraction


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/ea66f7ac-62dd-473a-aa01-48ba11284b5d)

Contents of the file
THM-4n6-2-4

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/fe12d501-2f09-4310-99d3-7cbc8be945d6)

Evidence of Execution


How many times was gkape.exe executed?

To parse the file :

The  command point to the gkape file that we need to parse and the output will got to a folder created earlier on the desktop C:\Users\THM-4n6\Desktop\THM06 in CSV.

PECmd.exe -f C:\Users\THM-4n6\Desktop\triage\C\Windows\prefetch\GKAPE.EXE-E935EF56.pf --csv C:\Users\THM-4n6\Desktop\THM06

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/55004b64-10aa-489e-b343-62aed6d41c13) 

The file went the desktop folder


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/e942ebf8-3673-4a0d-87c6-072f7207a1c7)


We can use the Ezviewer to see the parsed file. 
We can see Gkape was executed two times.

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/72296e31-01de-4b69-b305-926cecc3b6fd)


The answer is 2


What is the last execution time of gkape.exe
12/01/2021 13:04

When Notepad.exe was opened on 11/30/2021 at 10:56, how long did it remain in focus?

To parse the file, we use the following :

WxTCmd.exe -f C:\Users\THM-4n6\Desktop\triage\C\Users\THM-4n6\AppData\Local\ConnectedDevicesPlatform\L.THM-4n6\ActivitiesCache.db --csv C:\Users\THM-4n6\Desktop\THM089

The parsed file is stored in CSV format to an folder  on desktop and we can open it to find the answer


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/17596cc6-55fa-4bc4-a30f-ffa1f8ff6254)

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/11b97f21-b274-471d-8caa-2c2811140c95)

The answer is 00:00:41

What program was used to open C:\Users\THM-4n6\Desktop\KAPE\KAPE\ChangeLog.txt?
notepad.exe

When was the folder C:\Users\THM-4n6\Desktop\regripper last opened?

We are using autopsy to find C:\Users\THM-4n6\Desktop\regripper


![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/0d156b63-593d-41aa-85fe-329236853144)


We can then use the path from Autopsy to parse the file and save it to an output CSV file.

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/9e86f7ab-37e5-4c75-a2d3-c58655dfdd32)

EZviewer to see the CSV file

![image](https://github.com/Rory33160/Windows-Forensics-2/assets/47018034/8a830802-9df9-4ef1-9715-a85b34e8d535)


Answer:
12/1/2021 13:01



When was the above-mentioned folder first opened?

The same file from the previous question shows the creation date.
Answer:  12/1/2021 12:31






































































