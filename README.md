### Disclaimer:
This comparison and reason behind choosing chef over ansible is not passed by any reliable resources. It is purely based on my knowledge of Chef and Ansible. If you find any mistakes or misleading information, please revert back to me on "manish.devops@gmail.com"

## Chef Vs Ansible

### Limited OS Support vs Large OS Support: 

**Ansible:** Either Ansible launched their product in a hurry or they were quite satisfied to have a product which supports only Linux. Ansible 1.x has a very limited support for Windows, Mac and many other operating systems. They recently released Ansible 2.0 (12 Jan 2016) which claims to have "Expanded support for managing Microsoft Windows environments". But it's success story is not yet written. 

**Chef:** On contrary, Chef claims to have a large Operating System support including Linux, Windows, iOS etc. 

### Terrible GUI vs Neat GUI: 

**Ansible:** There are cases in which you will find totally different result in GUI and CLI for same queries.  The features are limited and GUI is not properly synced with CLI.

**Chef:** Even in Chef, you can't manage your entire infrastructure using only GUI. There are certain limitations but it still has a lot of features which makes Chef administration easier. It is neat and well synced with CLI.

### Less Documentation vs Better Documentation:

**Ansible:** Ansible has provided very limited documentation. There are multiple improvement possibilities in it. On their defense, Ansible Community says that you don't really need much documentation to work with ansible (Considering the ease of use). 

**Chef:** Chef itself has provided ample documentation. Since is it pretty old and widely used, you can find a lot of study material and live use cases in different communities.
 
### Architectural Differences: 
This is the biggest and decision making difference between these two tools. Before jumping into any conclusion, we need to understand how Ansible and Chef typically work.

**Ansible:** We install ansible server on machine "ABC", this will contain a text file named "inventory.ini". This inventory.ini file will be having list of all the agent machines. You can create groups of Agents in this file and push playbooks into one or more groups in one go. Authentication is done by either passing username and password or by SSH Key Authentication. Look at it this way now: If there are 1000 servers, they all need to be listed in inventory.ini file. There will be just one machine from where you can execute playbooks and that machine already has ssh authentication keys for all the agent machines. For this system to work, eventually you will have to give access to project teams. Since there is just one Ansible server for multiple project teams  and all the project teams has access to that one server, the probability of huge blunders becomes more. Team "A" might change "inventory.ini" file and it may affect team "B". Team "A" might end up doing configuration changes in Ansible Server (Since they have server access) and it will impact all other teams as well. If you want to use one Ansible for each project team then you will be managing hundreds of Ansible. In either way, Ansible is not a suitable tool for our infrastructure. 

**Chef:** Can we resolve above mentioned problems using Chef? The answer is Yes. How? Precisely chef is a combination of three separate entities. Chef Server, Chef Nodes and Chef Workstation. User need not have access to Chef Server, he can do all possible Chef operations by just accessing Chef-Workstation and one Chef server can have any number of Workstations. Well, this solves the problem of accessing server directly but how will you distinguish between projects? If workstation can do everything then it may make changes in other teams project as well. Right? No, Chef has a concept called Organization. Every organization is an independent entity and does not share any data with other organization. Meaning we can map our Project Teams to Organizations and now every project team is an isolated entity. Chef-Workstation of organization "A" cannot execute recipes in the nodes of organization "B". Problem Solved :). Now we can have one centralized Chef server (Just like Central Jenkins Server) and teams will be given the access to the workstations of their organizations. 
 
### Agent vs Agentless: 

Being agentless definitely eases the work and reduces the load in nodes. Ansible is agentless and it uses SSH for communication. Great. But... there are certain limitations of SSH communication and when you have a root access agent running on node (In case of Chef), all these limitations vanish.

### Ruby vs YAML:

Chef uses Ruby for cooking Recipes and Ansible uses YAML to write playbooks. Ruby is an Object oriented Programming language. This gives us liberty to create complicated logics. YAML sticks with a very strict format. You don't really write program in it, you just pass values. Exposing only YAML to users will not be enough in custom use cases.

### Reliability vs Un-Tested-ness:

Chef is used, tested and certified by big Giants like Facebook, Amazon etc. There is huge support available for it. Chef community aka Chef Supermarket will get you a lot of Chef contributors. Most of the devops tools are featuring integration with Chef, Which puts Chef in the category of reliable tools. On the other hand, Ansible is new and not tested in huge scale. No doubt it works faster than Chef in small environments but we as large organization will be dealing with huge environments. Hence Chef is reliable and a better choice.  


Considering all these points we can say that if we want to use configuration management tool for a small environment, we should use Ansible (It is faster and easier) but since we are dealing with multi-tiered complex architectures with a lot of servers, we should use Chef. 
