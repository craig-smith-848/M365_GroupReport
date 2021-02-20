## Microsoft 365 Group Report PowerShell Script – Execution Steps

Step 1: Download the script.  

Step 2: Start Windows PowerShell as Administrator.   

Step 3: To view all the groups and their members’ info, run the script as follows: 

```powershell
./M365GroupReports.ps1
```
After the script execution, both output files will be available in the execution directory. 

**_Note:_** You can use the above syntax to execute the script with both MFA and non-MFA account. 

### Microsoft 365 Group Report 

The Microsoft 365 Group report has the following columns: Group Name, Email Address, Group Type, Group Members Count, and Members Count by Type. 

### Microsoft 365 Group Membership Report

The Microsoft 365 group membership report has the following columns: Group Name, Group Email Address, Member Name, Member Email, and Member Type. Group member type is helpful in identifying type of a member such as user, group, and contact. 

### More Use-cases of Microsoft 365 Group Report Script 

As earlier said, the script supports advanced filtering params to get the report as per your requirement. 

Export all Microsoft 365 Groups and Membership to CSV

To export all the Microsoft 365 groups, execute the script as follows:

```powershell
./M365GroupReports.ps1
```

The exported report contains all the group types such as Distribution List, Security Groups, Mail-enabled Security group and Unified groups. 

By referring to this report, admin can add or remove user from the group. 

### Get Members for a Single/List of Groups

You can use –GroupIDsFile param to get the report for specific group(s) from the input list called “GroupId.txt” and exports all membership into CSV. 

To get group report and membership report for specific groups, pass an input file with a GUID of groups. 

```powershell
./M365GroupReports.ps1 -GroupIDsFile C:/GroupId.txt
```

The GroupIDsFile must follow the format below:  Group identity separated by new line without a header. 

## Office 365 group report

### Group Size Report 

The report helps you to get the groups that have more than an ‘N’ number of members. To get this report, you can execute the script with ```–MinGroupMembersCount``` param. 

```powershell
./M365GroupReports.ps1 -MinGroupMembersCount 50
```

The above script exports all groups that have more than 50 members. 

**_Note:_** If you want to determine group membership (I.e., members count) based on certain conditions, you can use Dynamic Group membership report. 

### Microsoft 365 Security Group Report 

Security groups are used for granting access to Microsoft 365 resources. To export security group report, you can run the script with ```–Security``` param.  

```powershell
./M365GroupReports.ps1 -Security
```

By referring group membership report, you can view the users who has rights and access to SharePoint sites and CRM Online.  

### Distribution List Report

Distribution lists are used for sending notifications to a group of people. To export distribution group and their membership, you can use ```–DistributionList``` param while executing the script. 

```powershell
./M365GroupReports.ps1 -DistributionList
```

The above script lists all the distribution groups and their members’ info.  

**_Note:_** The report lists Microsoft 365 groups (group mailboxes) as a Distribution List. 

You can also check our dedicated script on the Distribution Group membership report for a more detailed report. 

Mail-enabled Security Groups Report

This type of group works as regular security along with the ability to send mail to its members. To get a list of all the mail-enabled security groups, execute the script with –MailEnabledSecurity param. 

```powershell
./M365GroupReports.ps1 -MailEnabledSecurity
```

The script exports mail-enabled security groups info and membership to the CSV file. 

### Get Empty Groups Report 

To get an empty group report (i.e., groups without members), execute the script with ```–IsEmpty``` param. 

```powershell
./M365GroupReport.ps1 -IsEmpty
```

By referring to this report, you can delete unused/inactive groups in your tenant. 

### Schedule Group Report to run Periodically

As said earlier, this script is scheduler friendly. You can pass the credential as a parameter. So, it will not prompt for username and password during execution. 

./M365GroupReport.ps1 -UserName admin@contoso.com -Password XXX

You can use Windows Task Scheduler for PowerShell scheduled task. 

### Get more Granular Group Report

To export a more granular group report, you can use multiple filters (i.e., params and switches). I have given few examples below. 

To get empty distribution groups:

```powershell
./M365GroupReport.ps1 -IsEmpty -DistributionList
```

To view empty security groups:

```powershell
./M365GroupReport.ps1 -IsEmpty -Security
```

To list empty mail-enabled security groups:

```powershell
./M365GroupReport.ps1 -IsEmpty -MailenabledSecurity
```

To get large distribution groups:

```powershell
./M365GroupReports.ps1 -DistributionList -MinGroupMembersCount 500
```

To get security groups based on the members count:

```powershell
./M365GroupReports.ps1 -Security -MinGroupMembersCount 50
```