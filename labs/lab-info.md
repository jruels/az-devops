# Access Window VMs
To access the Windows VMs, please go to [Inspired Portal](https://html.inspiredvlabs.com/) and log in with the following: 


| First Name        | Last Name  | Username   | Password    |
| ----------------- | ---------- | ---------- | ----------- |
| David             | Henrique   | WNS2022-85 | TeKwns2022! |
| Henrique          | Weh        | WNS2022-86 |             |
| Khuddus           | Mohammed   | WNS2022-87 |             |
| Chander           | Anand      | WNS2022-88 |             |
| Rexford           | Machu      | WNS2022-89 |             |
| Sarnam            | Patel      | WNS2022-90 |             |
| Madhukar          | Kalla      | WNS2022-94 |             |
| Srividhya Kalyana | Ramamurthy | WNS2022-91 |             |
| Harpreet S        | Lotay      | WNS2022-92 |             |
| Vanaja            | Pilaka     | WNS2022-93 |             |



# Access the Linux lab VMs

| First Name        | Last Name  | VM             |
| ----------------- | ---------- | -------------- |
| David             | Henrique   | 54.241.229.2   |
| Henrique          | Weh        | 3.101.65.131   |
| Khuddus           | Mohammed   | 18.144.47.130  |
| Chander           | Anand      | 52.53.182.42   |
| Rexford           | Machu      | 54.151.121.25  |
| Sarnam            | Patel      | 54.177.46.3    |
| Madhukar          | Kalla      | 13.56.197.212  |
| Srividhya Kalyana | Ramamurthy | 54.153.90.26   |
| Harpreet S        | Lotay      | 54.193.247.138 |
| Vanaja            | Pilaka     | 54.183.152.62  |

# Azure credentials
Please log into the [Azure Portal](http://portal.azure.com) using the credentials below. 

Username: `<student#>@jasoninnovationinsoftware.onmicrosoft.com`

Instructor will provide the password 

| First Name        | Last Name  | student number |
| ----------------- | ---------- | -------------- |
| David             | Henrique   | student3       |
| Henrique          | Weh        | student4       |
| Khuddus           | Mohammed   | student5       |
| Chander           | Anand      | student6       |
| Rexford           | Machu      | student7       |
| Sarnam            | Patel      | student8       |
| Madukar           | Kalla      | student9       |
| Srividhya Kalyana | Ramamurthy | student10      |
| Harpreet S        | Lotay      | student11      |
| Vanaja            | Pilaka     | student12      |



# Lab Setup

To connect to the lab VMs, you must authenticate using an SSH key. Download the keys from [here](https://github.com/innovationinsoftware/microservices-practical/raw/refs/heads/main/keys.zip). Once the download is complete, extract the zip file where it is easily accessible.

### Mac/Linux

The username for SSH is
`ubuntu`

Open a terminal and `cd` to the extracted lab directory that contains the SSH keys. Inside the directory, run the following command.

### Set permission on SSH keys

```
chmod 600 lab.pem
```



### SSH to lab servers

```
ssh -i lab.pem ubuntu@<MANAGED NODE IP FROM SPREADSHEET>
```

### Set up Putty

If you don’t already have it, download Putty from [here](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe) and save it to your desktop.

Open Putty and configure a new session for the lab VM.

![img](https://jruels.github.io/openshift-admin/labs/openshift-deploy/images/putty-session.png)

Expand Connection -> SSH -> Auth -> Credentials, click “Browse”, and then in the extracted `keys` directory, choose `lab.ppk`

![image-20230918185300995](https://jruels.github.io/openshift-admin/labs/openshift-deploy/images/putty-auth.png)

**Remember to save your sessions**.
