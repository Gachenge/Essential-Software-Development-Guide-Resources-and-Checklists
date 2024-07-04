# Essential-Software-Development-Guide-Resources-and-Checklists.
A Comprehensive Dictionary of all the essential guides, resources and tools in every aspect of software development.
A COMPREHENSIVE SOFTWARE DEVELOPMENT GUIDE, CHECKLIST AND RESOURCES.

Self-Hosting Guide, Devops & DevSec Ops and A guide to Security in development.

I. Self-Hosting Guide.
Tools to use:  i. Coolify – Open Source alternative to Heroku, Netlify, Render and Vercel that make deployment easy and simple. [ https://github.com/coollabsio/coolify ]
		ii. Dokploy – Another Open Source alternative to Heroku, Netlify, Render and Vercel that make deployment easy and simple.[ https://github.com/Dokploy/dokploy  ]
		iii. Hetzner for VPS/ KVM VPS – As of 4th July 2024 Hetzner is the best source for quality VPS because of its good mix of affordability and value meaning it has many server options and you can get what you need for a relatively good price.
Depending on the use case, for production grade deployments (non CPU and Traffic/bandwidth heavy applications) buy the 40-50 dollar VDS in which you can host 2-3 applications like this. For other CPU, Traffic/Bandwidth heavy applications buy the 100-500 dollar VDS. Changes can be made when you reach a point where you both need the capacity and you have the resources for it in which you can just pay for really expensive 500-1000 dollar VDS and consolidate all your applications to just that one VDS.
For personal/hobby use the 5-10 dollar VPS are good.
		iv. Various Linux distros and open source cloud systems like Casa OS can be installed.









II. Devops Guide.
Refer to the following Github Repository`s:
	1. Devops guide - https://github.com/antonputra/tutorials [devops tutorials]
   -https://github.com/milanm/DevOps-Roadmap [Roadmap]
	2. Ansible - https://github.com/geerlingguy/ansible-for-devops [Ansible for devops examples]
	3. Terraform- https://github.com/shuaibiyy/awesome-tf [Hashicorp Terraform Resources]
		- https://github.com/Devgurusio/terraform-aws-eks-ecommerce [AWS elastic kurbenetes starter kit]
	4. Kubesphere - https://github.com/kubesphere/kubesphere [Platform tailored for kurbenetes multi-cloud, data center and edge management.]

III. DevSecOPs
Refer to this Guide: https://github.com/sottlmarek/DevSecOps



B2B & B2C Software Design.
I. AB Testing.


II. API Keys.


III. Authentication.
Alternatives: Open Source Versions.



IV. CI/CD.
Alternatives: CI/CD tools provided by Cloud Providers e.g. AWS & Azure devops or you can build your own if it’s necessary and you have the manpower, time and money for it.


V. Communication
Alternatives: Self hosted Open Source Communication.e.g. Mattermost

I. Search.
Addition: Medusa search


II. Database

III. Documentation.
Alternatives: Open Source Self Hostable Versions

IV. Email.

V. Events.

VI. Feedback.

VII. Design.

VIII. File Storage.






IX. Hosting.
Alternatives: For cloud use AWS free tier or serverless option [set budget alerts and automated kill switches for over budgets] while for VPS and KVM VPS use Hetzner [Buy from Auctions for production grade releases & 5-10 dollar VPS for personal use] or Hostinger $60-dollar plan. 

X. Issue Tracking.

XI. Version Control
Addition: Mercurial Version control

XII. SMS
Addition: Local Providers

XIII. Logging.
Addition: Loki for logs aggregation and Promtail for log fetching and labelling and other quality open source versions.


XIV. Marketing.
Addition: SMS & WhatsApp Marketing.

XV. Payment Processing.
Other Options maybe be added depending on use case.e.g. cashapp/venmo/wise/western union/MoneyGram.


XVI. Monitoring
Monitoring Tools Include Prometheus, Netdata for server monitoring.
XVII. Dashboards
Tools: Grafana, tremor and Netdata plus other quality open source versions.
XVIII. AI and Machine Learning
Hugging Face - https://github.com/huggingface 
Awesome Machine Learning - https://github.com/josephmisiti/awesome-machine-learning 
XIX. Frontend Resources
Frontend Checks - https://github.com/kriasoft/aspnet-starter-kit 
XX. Templates and Boilerplates
.NET - https://github.com/kriasoft/aspnet-starter-kit 
React - https://github.com/mcnamee/react-native-starter-kit 
Nextjs - https://github.com/boxyhq/saas-starter-kit
Vue & .NET - https://github.com/alirizaadiyahsi/Nucleus 
SaaS - https://github.com/boxyhq/saas-starter-kit 





















An Example of Methods of Cost Analysis for an application. [ For use during System Design and Application Deployment.]
What is a rough estimate of the cost of a server space/hosting for a Tinder-style app with 200k users?
That’s impossible to say. Because you can have 200k users sitting in a $5 VPS doing nothing, and you can have 200k users hammering a cluster of servers continuously.
What you need to do is estimate how many requests your application/users will generate. If we estimate that no more than 20% of registered users are active at any one time, we have 40,000 users active at any one time.
40,000 users might generate 50 requests per minute (fast swiping ya’ know) is 2 million requests a minute. Then we take 2 million requests and divide it out in seconds, meaning 33,333 requests per second.
All those requests have various implications. Each request hits a load balancer, an application server and finally a database of sorts.
Now we have some rough numbers, now for the hard part. How many servers do we need for ~30k/s? Again some guesswork, because it depends on your application. If we estimate that an application server can handle 500 requests a second, we’ll need around 66 application servers. For the database we have a challenge. Because a “tinder style” app is quite write heavy.
For every swipe you generate data. I’m basing numbers on one request per swipe, however it would make sense to batch them up and for instance send collected data once a minute from the app. That would greatly decrease the number of requests and the number of servers.
Receiving requests isn’t enough. We’d need to persist all the requests too. I’d probably use a queue, as it’s not essential that data is written in real-time. Using a queue as a buffer, can keep the price of the database layer down greatly. So a swipe request hits an application server which might add it to a queue. Then some workers will chew through the queue in batches and add it to the database.
Let’s imagine we start with a cluster of 3 servers for the database and a single larger one for the queue.
For storage of images I’d suggest an object store. For general resources a CDN. each user stores maybe 5 pictures of 50kb each, meaning 250kb * 200,000 users = roughly 500GB of data.
Time for counting the money. I’ll base prices off Digital Ocean - Cloud Computing, Simplicity at Scale which i know. At the time of writing, the link gives a credit for $100 to try them out for performance, although it wouldn’t get you very far in this case.
Here goes:
* Load balancer (managed) for application servers: $10/month (cheapest part of the project)
* 66 application servers (8 vCPU, 32GB RAM) at $160 each: $10,560/month
* 3 database servers (12 vCPU, 48GB RAM) at $240 each: $720/month
* 1 queue server (8 vCPU, 32GB RAM): $160/month
* 3 workers (8 vCPU, 32GB RAM) to process data from queue into database at $160 each: $480/month
* Storage for 500GB: $10 (yes really)
Adding it all up, you’ll have a monthly bill of $11,490.
$11,490?!??! Yes, now don’t worry. It doesn’t even include traffic. However, the proper way to look at it is not total price, but price per user. If you have 200,000 users, the price per user is just under $0.06. So for you to be profitable, your average income per user just need to exceed $0.06 per month.
As for traffic, you have 514TB monthly traffic included with the price above. That’s roughly 208MB a second, if evenly distributed. So you’ll pay for some extra traffic, but not enough to skew the calculation that much. Also I’d probably add some servers for static content and a large server for caching database results, for frequent queries, if the database doesn’t provide a RAM based cache.
These prices do not include development or testing servers or geographic redundancy, but I hope it gave you a rough idea on what it would cost.

       Programming Standards and Error/Bug Prevention Techniques. [ Use Linters, Automated Tests to enforce them.]
Best practices that developers adhere to when writing code to ensure consistency, readability, and maintainability.
        ?? Indentation and Formatting: ? Use consistent indentation and formatting.
        ?? Comments: ? Include clear and concise comments. 
       ?? Naming Conventions: ? Use descriptive and consistent names. 
       ?? Function Length: ? Keep functions short and focused. 
       ?? Error Handling: ? Implement proper error handling with meaningful messages. 
       ?? Code Duplication: ? Minimize code duplication; refactor when necessary. 
       ?? Testing: ? Write and maintain unit tests. 
       ?? Performance: ? Optimize code for performance when needed.
Refer to this GitHub repo for better explanation https://github.com/Kristories/awesome-guidelines , JavaScript guidelines https://github.com/airbnb/javascript 
Links to tools used to enforce this:
