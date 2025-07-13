# stolen_mount
TryHackMe - Stolen Mount Lab Writeup

# What This Challenge Was About

This TryHackMe room focused on analyzing a packet capture (PCAP) file to figure out what an attacker accessed and stole from an NFS server. The task was to investigate the network traffic, extract any transferred files, and uncover the hidden flag.


How I Solved It

# Step 1: Opened the PCAP

I started by opening the provided challenges.pcapng file in Wireshark to get an overview of the traffic and look for anything interesting.

Step 2: Spotted NFS Operations

# While browsing through the packets, I noticed NFS operations like:
	•	LOOKUP – used to find files
	•	GETATTR – checking file attributes
	•	READ – actually reading the contents of the files (this is where the theft happened)

# Step 3: Followed TCP Streams

I followed TCP streams to trace how the files were being accessed and pulled from the server.

# Step 4: Used the strings Command

To make things easier, I ran strings on the PCAP file to extract readable text. This helped surface key info, including an MD5 hash that would be useful later.

<img width="848" height="263" alt="image" src="https://github.com/user-attachments/assets/cd60aa63-4931-4feb-9410-8f04fbcb8887" />

# Step 5: Pulled Files Using CyberChef

After copying hex data from the relevant TCP streams, I dropped it into CyberChef. That helped me reconstruct two ZIP files that had been transferred through the network.
<img width="1097" height="530" alt="image" src="https://github.com/user-attachments/assets/b9f0d411-4239-4f6f-a475-34b8257105e3" />


# Step 6: One ZIP File Was Locked

One of the extracted ZIPs was password-protected. I had the MD5 hash from earlier, so I searched for it using an online MD5 lookup.

<img width="472" height="329" alt="image" src="https://github.com/user-attachments/assets/7e11e50e-0d32-4366-a564-296747be1fe2" />


# Step 7: Cracked the Password

The hash matched the password: avengers. I used that to unlock the archive.

<img width="1127" height="257" alt="image" src="https://github.com/user-attachments/assets/2607d3a1-95a5-47d1-aad2-0112123674c6" />

# Step 8: Found a QR Code Inside

Inside the unlocked ZIP was a file called secrets.txt with a QR code. I scanned it using an online QR code reader.

# Step 9: Got the Flag

The QR code gave me the final flag for the challenge.
<img width="653" height="479" alt="image" src="https://github.com/user-attachments/assets/e5c7f612-5a2d-4e48-be9c-795fa44d462a" />



# Key Things I Learned
	•	How to identify and understand NFS traffic in a PCAP
	•	How to follow TCP streams to trace file access
	•	How to extract file data from network traffic using CyberChef
	•	How to handle password-protected archives and use hashes for cracking
	•	How multiple steps like ZIP extraction and QR decoding can be chained in forensic investigations


# Tools I Used
	•	Wireshark
	•	CyberChef
	•	strings (Linux CLI)
	•	MD5 hash lookup site
	•	QR code scanner



# Final Thoughts

This challenge was a great deep dive into network forensics. It combined protocol analysis, file extraction, and even a bit of password cracking. The multi-step process really reflected how complex and layered real-world investigations can get.
