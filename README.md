# Attacker-Reconnaissance-Lab-
My goal with this lab is just to get more comfortable with reading security logs with my SOC setup through Elastic. Today I just worked on the scanning of a network as if I already breached an environment through various tools I'm using and learning for the first time.

The first one I used was as a recon tool was NMAP. NMAP is a tool that allows you to run and check to see what ports are open, services being used and what OS the system is running.

I ran NMAP from the Kali machine

<img width="891" height="642" alt="image" src="https://github.com/user-attachments/assets/a7fb326e-3662-4da6-b588-44e261e7d9cd" />

The only issue is that the NMAP scan wouldnt clearly show in the Elastic logs. Which is something I didnt know. Something so COOL I learned is that the reason NMAP wont show in a scan is the "-sS" in n"map -sS -A 192.168.1.101." The sS stands for stealth scan, meaning when nmap is reaching it never fully completes the 3 step TCP Handshake. Since the connection never fully established, the OS has nothing meaningful to log in auth logs. It's why it's called a "stealth scan" — it intentionally avoids triggering standard logging. 


NMAP goes like this 

1.Nmap sends SYN

2.Server responds SYN-ACK

3.Nmap sends RST (reset) and drops it  never completes



So for that reason I installed Suricata. Suricata is a network packet anazlyer that would see every SYN,ACK, and open half communications. 

<img width="938" height="162" alt="image" src="https://github.com/user-attachments/assets/8cd3fc37-680e-422e-8f34-4e98e6ffe9a8" />


After installing Suricata I ran the NMAP's again and it didn't get the logs added to Elastic so I needed to add the agent to Kibana then the logs would show.

<img width="864" height="697" alt="image" src="https://github.com/user-attachments/assets/3f60d000-8e9b-4c57-91af-3ff03eb957eb" />




<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fa276d16-996c-4804-8c94-82b99487dbcb" />

Then after this I ran NMAP again and viewed the logs and changed the query to change for the IP to be filtered.


<img width="636" height="49" alt="image" src="https://github.com/user-attachments/assets/4f6c77fa-76cd-47e5-a775-f3fed915155c" />




<img width="642" height="518" alt="image" src="https://github.com/user-attachments/assets/402ced21-d196-49a9-a0b6-a6db5f208c1b" />





