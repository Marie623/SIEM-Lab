
1. The first step is to get Kali Linux using VirtualBox. You can find instructions here https://youtu.be/M0mBpTPE78k?si=k4FH0nbh_dzfTLJz

2. Create an Elastic account on https://cloud.elastic.co
3. Select "Create Deployment" and give it a name
![deployment](https://github.com/user-attachments/assets/0e362b17-c054-49c8-b4bf-2b93f4410e81)

Now we will add the agent on the Kali VM to push audit logs to the SIEM
1. Click hamburger menu
2. Add Integrations
  ![hamburger menu](https://github.com/user-attachments/assets/a0a566e3-babd-48a0-b360-901a7945e90e)
3. Elastic Defend
4. Add Elastic Defend
   ![add elastic defend](https://github.com/user-attachments/assets/fdc4a6f7-0b1e-4b30-91f7-74e5d9860de4)
5.  Configure Integration (then give it a name)
6.  I was asked it I wanted to Install Elastic defend Agent and I clicked yes and copied and pasted the Linux tar command in my terminal and let it run 
  ![install agent](https://github.com/user-attachments/assets/7466d127-fd36-4110-8345-37bb76e0b5b8)

7.  When it is done you will show "1 agent has been enrolled"
8.  Click "Add the integration" and then "confirm incoming data"
   ![add the integration](https://github.com/user-attachments/assets/9b416b64-858a-451d-8639-d6d73af290da)
  
   
9.  Under Integration settings, give it a name and save
10. Click "add elastic agent to your host"
  ![add agent to your host](https://github.com/user-attachments/assets/d3fed2e3-0d2f-4799-a28b-98c92e21d68f)

Next we'll generate commands
1.  Open terminal and find your host's ip address by typing ifconfig. Look for inet ip
2.  type nmap <inet_ip>
3.  type other commands such as
4.  nmap -sS <inet_ip>
5.  nmap -sU <inet_ip>
  ![nmap](https://github.com/user-attachments/assets/e5e0f7b6-2b1e-4ea8-af52-9cdd8ac0e38b)

6.  Go to the hamburger menu, observability, logs
   ![logs](https://github.com/user-attachments/assets/02f3029d-8030-4abd-be2b-56956f921963)

7.  type "process.args: nmap" in search bar
   ![custom query -nmap](https://github.com/user-attachments/assets/9c306bb5-d9a4-4109-a4b7-6f3d3ae5a062)
8.  click on one of the results to expand it and click on table and scroll and click through it to see date, time, user, ip and the command that was ran
  ![search args](https://github.com/user-attachments/assets/f46edbb4-2cff-4daa-aecc-847ca8d4db14)
  ![nmap proof](https://github.com/user-attachments/assets/0b01205c-f9ca-43e9-92f1-5c3f421926b3)


The Next step will be creating a dashboard
1.  Go to the hamburger menu, analytics, dashboards
2.  Click "create dashboard"
3.  Click "create visualization"
4.  Select "Vertical bar"
5.  Select "@timestamp in horizontal field"
6.  Select "count" in vertical field
7.  Click "Save and return"
8.  Click Save and name the dashboard
   ![bar dashboard](https://github.com/user-attachments/assets/1dbaabe2-b7a6-4dfe-99a0-174b66e3116f)
    
Let's Create an alert
1.   Go to hamburger menu, security and alerts
2.   Select manage rules, create new rules
3.   Select "Custom query"
4.   Beside custom query, type "event.action; nmap_scan"
   ![custom query](https://github.com/user-attachments/assets/6f74db4e-a992-4ab3-88cf-da6bfc45eaef)
5. 
6.   Click "continue"
7.   In "about rule", give it a name and a description of the alert and click continue until you get to "Rule Actions"
8.   I selected "Email"
  ![email action](https://github.com/user-attachments/assets/57b2cc57-2eeb-429b-bab6-320131cc4330)

1.   Under "if alert match a query", type "process.args: nmap"
2.   Add your email in the "To" section. Add Subject
3.   Click "Save and enable rule"
4.   Run some more nmap scans and see if the alerts will appear in your email.
    
That's it!
    