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

# Step 5: Pulled Files Using CyberChef

After copying hex data from the relevant TCP streams, I dropped it into CyberChef. That helped me reconstruct two ZIP files that had been transferred through the network.

# Step 6: One ZIP File Was Locked

One of the extracted ZIPs was password-protected. I had the MD5 hash from earlier, so I searched for it using an online MD5 lookup.

# Step 7: Cracked the Password

The hash matched the password: avengers. I used that to unlock the archive.

# Step 8: Found a QR Code Inside

Inside the unlocked ZIP was a file called secrets.txt with a QR code. I scanned it using an online QR code reader.

# Step 9: Got the Flag

The QR code gave me the final flag for the challenge.


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
