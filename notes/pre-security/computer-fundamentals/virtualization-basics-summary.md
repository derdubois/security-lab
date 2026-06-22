After learning about virtualization, you were hired to be responsible for the virtual environment for AutoGalo, a company that has recently started using lab machines.
In this company, they use an application called Virtualization Manager. This application provides a clear view of the overall status of an entire virtualization environment, providing details of each virtualized instance and the physical hosts. It also enables you to run actions and manage the VMs you create.

Your manager has asked you to investigate an issue with the email service. Essentially, everyone in the company stopped receiving emails today, and no one knows what happened.

Open the Virtualization Manager site by clicking the View Site button below, and let's investigate!


View Site
Analyzing Lab Machine States
In the home screen, you should see three main sections:

Summary: Provides a generic view of the state of the environment.
Lab Machines: Provides details of each VM and enables you to run actions on them.
Hosts: Displays usage and performance details for each physical server.
Go to the Lab Machines section and look for the VM with the name Mail-SERVER:

Lab Machine section screenshot highlighting the Mal-SERVER machine.

Looks like this lab machine has entered an Error state. Let's try rerunning this VM using the Blue Square Button to restart it.

Lab Machines section screenshot highlighting the restart button.

After running again, it appears to be working correctly, with no errors!

Creating a Lab Machine
As part of your routine, you create lab machines for other teams. After resolving the email server issue, you received a task to create a VM to support the marketing team's website.

Now, let's create a VM to host their marketing website. In the Lab Machines section, locate the + Create VM button on the top right side of the Lab Machines section and click on it.

Lab Machines section screenshot highlighting the "+ Create VM" button.You should fill out the form with how much hardware your lab machine will be using:

Name: Marketing-VM
CPU Cores: 4
Memory (GB): 8
Disk Size (GB): 100
Then click on Create VM

Screenshot of the form to create a VM.
Now, at the top of the list of Lab Machines, you should see your created VM:

Lab Machines section screenshot highlighting the new Marketing-VM created.

Analyzing Hardware Usage
Another routine task you have is to manage the health of the physical servers and report status to your manager. Go to the Hosts section at the bottom of the page:

Screenshot of Hosts section.
By analyzing it, we can identify:

HV-PROD-01 has the capacity to host more VMs.
HV-PROD-02 is almost operating at 100% of its capacity, and we might need to report this!
HV-BACKUP-01 is disconnected and does not host any VMs.
Hosts section screenshot highlighting the insights mentioned above.

Now, answer the following task questions to conclude your shift as the responsible for virtualization in AutoGalo!
