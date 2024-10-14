1. The first step is to get Kali Linux using VMWare or VirtualBox
2. Create an Elastic account on https://cloud.elastic.co
3. Select "Create Deployment" and give it a name
   ![FirstDeployment](deployment.png)

Now we will add the agent on the Kali VM to push audit logs to the SIEM
1. Click hamburger menu
2. Add Integrations
   ![hamburger!] (hamburger menu.png)
3. Elastic Defend
4. Add Elastic Defend
5.  Configure Integration (then give it a name)
6.  I was asked it I wanted to Install Elastic defend Agent and I clicked yes and copied and pasted the Linux tar command in my terminal and let it run 
   ![InstallAgent] (install agent.png)
7.  When it is done you will show "1 agent has been enrolled"
8.  Click "Add the integration" and then "confirm incoming data"
    ![addIntegration](add the integration.png)
9.  Click "Add elastic defend"
    ![addelasticdefend](add agent to your host.png)
   
10. Under Integration settings, give it a name and save
11. Click "add elastic agent to your host"
   ![addagent] (add agent to your host.png)

Next we'll generate commands
1.  Open terminal and find your host's ip address by typing ifconfig. Look for inet ip
2.  type nmap <inet_ip>
3.  type other commands such as
4.  nmap -sS <inet_ip>
5.  nmap -sU <inet_ip>
   ![namp] (nmap.png)

6.  Go to the hamburger menu, observability, logs
   ![logs] (logs.png)
7.  type "process.args: nmap" in search bar
   ![customQueryNmap] (custom query -nmap.png)
8.  click on one of the results to expand it and click on table and scroll and click through it to see date, time, user, ip and the command that was ran
9. ![SearchArgs] (search args.png)
   ![NmapProof] (nmap proof.png)


The Next step will be creating a dashboard
1.  Go to the hamburger menu, analytics, dashboards
2.  Click "create dashboard"
3.  Click "create visualization"
4.  Select "Vertical bar"
5.  Select "@timestamp in horizontal field"
6.  Select "count" in vertical field
7.  Click "Save and return"
8.  Click Save and name the dashboard
    ![dashboard](bar dashboard.png)
    
Let's Create an alert
1.   Go to hamberger menu, security and alerts
2.   Select manage rules, create new rules
3.   Select "Custom query"
4.   Beside custom query, type "event.action; nmap_scan"
5. ![CustomQuery] (custom query.png)
6.   Click "continue"
7.   In "about rule", give it a name and a description of the alert and click continue until you get to "Rule Actions"
8.   I selected "Email"
   ![email] (email action.png)
9.   Under "if alert match a query", type "process.args: nmap"
10.  Add your email in the "To" section. Add Subject
11.  Click "Save and enable rule"
12.  Run some more nmap scans and see if the alerts will appear in your email.
    
That's it!
    