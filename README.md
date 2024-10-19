# Day-26-Investigating-SSH-Brute-Force-Alerts

In today’s interconnected digital landscape, security threats are ever-present, and one of the most common attacks that organizations face is the SSH Brute Force attack. Attackers try thousands of login attempts, hoping to crack credentials and gain unauthorized access. If you’re responsible for securing your systems, investigating and responding to these alerts is crucial.

But where do you start, and what should you look for? In this blog, we’ll break down the key steps to investigate an SSH Brute Force alert effectively. By the end, you’ll know exactly how to determine whether an attack was successful, the signs to watch out for, and how to automate your response for seamless alert management.

Let’s dive in and uncover the steps to securing your systems against brute force threats!

## Getting Started

First, let’s navigate to our security dashboard. Click on the hamburger icon, scroll down, and select Alerts under the Security tab. You should now see the alert screen, which may show a large number of alerts — mine displays over 2,000! Depending on your situation, you might have more or fewer alerts to review.

## Key Areas to Investigate

When investigating an SSH Brute Force alert, there are several crucial aspects to consider:

- **IP Address**: Is this IP known for brute force activity?
- **Affected Users**: Are there any other users affected by this IP?
- **Successful Logins**: Were any of these login attempts successful?
- **Post-Login Activity**: If successful, what activities occurred after the login?

Now, let’s dive into our alert and investigate the log using these criteria.

### Step 1: Investigate the IP Address

For our investigation, we’ll use the IP address `83.222.191.62`.

1. **Check the IP on Abuse IPDB**:
   - Copy the IP address and paste it into Abuse IPDB. This tool will help us determine if the IP is associated with malicious activity.
   - The result indicates that this IP is indeed known for performing brute force attacks.

2. **Check the IP on GreyNoise**:
   - Next, open GreyNoise and click on Get Started for Free.
   - Enter the same IP address in the search bar. The result again confirms that this IP is malicious.

**Conclusion**: The answer to our first question — Is this IP known for brute force activity? — is **YES**.

### Step 2: Identify Affected Users

Next, we need to determine which users are affected by this IP.

1. Go to Elastic and select Discover.
2. Paste the copied IP in the search bar.
3. Check the `user.name` field (located on the left-hand side under field names).

From our search, we find that the affected user is **1** and the user is **root**.

### Step 3: Check for Successful Logins

Now, let’s investigate whether any of the login attempts were successful.

1. Remain on the same page as the previous step and modify your search query to include both the IP address and “Accepted”.
2. In my case, there were no successful logs, leading us to conclude that the answer to our question — Were any of these logins successful? — is **NO**.

### Step 4: Investigate Post-Login Activity

This question is crucial: If there had been a successful login, what activities occurred afterward? Possible actions could include:

- Downloading malicious scripts
- Executing discovery commands
- Establishing persistence
- Running privilege escalation tools like LinPEAS

Since we found no successful logins, we will simply state **NO** for our fourth question.

## Conclusion of the Investigation

Given that there were no successful logins, we can confidently close this particular alert.

## Automating Alerts to Your Ticketing System

Next, let’s modify our rules to send alerts to our ticketing system. Here’s how:

1. Click on Rules on the left sidebar and select Detection Rules.
2. Locate SSH Brute Force Attempt and click on it.
3. Inside, select Edit Rule Settings, then navigate to the Action tab at the top and select Webhook.
4. You should see your OS Ticket connector available. For Action Frequency, choose **for each alert**. In the Body, use the same OS Ticket GitHub test body and edit it as needed for your context.
5. Once you’ve made your changes, click **Save Changes**. It may take some time to receive an alert ticket, so let’s be patient.

### Step 5: Managing Your Tickets in OS Ticket

Now, let’s head over to OS Ticket to manage our newly created alert ticket:

1. Navigate to the Admin Panel in OS Ticket.
2. Once you are inside, you should see the ticket for your alert.
3. Click on the ticket to open it. From here, you can assign the ticket to a specific user, or you can assign it to yourself.

## Conclusion

Congratulations! You’ve now successfully navigated the entire process of investigating an SSH Brute Force alert — from identifying malicious IPs to managing your alerts in a ticketing system. By following this structured approach, you’re not only safeguarding your systems but also streamlining your incident response workflow.

Remember, every alert is a potential threat, and by mastering these investigative steps, you’re staying one step ahead of attackers. You’ve also taken the extra step of integrating your alerts with OS Ticket, ensuring that no critical notification slips through the cracks.

In the fast-paced world of cybersecurity, there’s always something new to learn and refine. In my next blog, we’ll turn our focus to RDP Brute Force activity, diving into how to detect and mitigate these attacks just as efficiently.

Stay sharp and stay secure — until next time!

