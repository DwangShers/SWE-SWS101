Submitted by:

Student Name: Dechen Wangdra Sherpa

Enrollment No.: 02230281

Programme: BESWE

Date: 5/5/2024

---

### Executive Summary 

The Network Penetration Testing aimed to assess the security of a new server deployed by lecturers within the GCBS college network before its release to the internet. As a Senior Penetration Tester at the Royal University of Bhutan(RUB), I identified multiple vulnerabilities, including entry points and privilege escalation paths. Detailed findings are documented in the report, and the evidence is stored in the Github repository.

1. #### Github Repo Link for evidences

https://github.com/DwangShers/SWE-SWS101/tree/main/caps/cap1

2. #### Approach

I performed penetration testing under the server “10.3.21.140”  approach April 15, 2024, to May 5, 2024 without credentials in an internally facing environment with the goal of identifying vulnerabilities and exploits. However, the process presented challenges, as I had to stay up late night utilizing the college’s WIFI to conduct the penetration testing on the server. I used youtube to research the pen testing methods on the ports and it was time consuming as some worked and some did not. 

3. #### Scope

I am tasked with assessing the security of the new server deployed by a lecturer, which will be released after my successful testing. It involves conducting tests to identify vulnerabilities and potential entry points into the server, examining all ports and see which ones are vulnerable. 

4. #### Assessment Overview and Recommendations

During the internal penetration test against the server, I identified five (5) vulnerabilities which are not secure and safe for the server to be deployed to the internet. The vulnerabilities are threats to confidentiality, and integrity of the system. Hackers would easily get root access by brute forcing the passwords and usernames. 

Another issue was a weak configuration involving service accounts that allows any unauthenticated users to steal documentations and could even make changes to the service accounts.

Finally, I also found a web server that uses weak and easily guessable credentials to access the server to gain unauthorized access. 

### Network Penetration Test Assessment Summary

I began all the testing activities from the perspective of an unauthenticated user on the internal network. 

#### Summary of the Findings.

During the pen testing, I uncovered a total of five (5) ways to gain root access which were found to be easily accessible.

![alt text](<Images/Pasted image.png>)

### Network Compromise Walkthrough

During the testing I was able to gain root access in different ways leading to full control over the server. The steps below demonstrate the steps that I followed during penetration testing. 

First step is to check whether the machine or the host is up or not. We can do this by browsing the Ip-address in the network server. 

![alt text](../notes/Images/website.png)

Since, the server was up. 

Then I did nmap scan for all the ports 

![alt text](../evidences/scans/service-enumeration/nmap-all-port-scan.png)

I found that there are 23 open ports. 
Then, I did a particular scan for port 22, which served ssh. 

![alt text](../evidences/scans/service-enumeration/nmap-port-22.png)

#### (way1) auxiliary/scanner/ssh/ssh_login

To identify vulnerability for port number 22, I used metasploit. 

Step 1: start the console to use the tool.

![alt text](../evidences/exploitation/metasploitable_ssh-port22/1.open_metaspoitable_console.png)

Step 2: Use the ‘search’ function to quickly locate specific modules.

![alt text](../evidences/exploitation/metasploitable_ssh-port22/2.search_name.png)

Step  3: Use the ‘use’ function to select a specific module and the ‘show options’ command to display the configuration parameters and options associated with the selected module. 

![alt text](../evidences/exploitation/metasploitable_ssh-port22/3.use_and_show_options.png)

Step 4: From the options in the ‘current settings’ option, set the ‘rhosts’ to <target-ip>  ‘user_file’ to <Users.txt> and ‘pass_file’ to <Passwords.txt>.

![alt text](../evidences/exploitation/metasploitable_ssh-port22/4.set_current_setting.png)

Step 5: Check ‘Options’ to confirm that everything is set. 

![alt text](../evidences/exploitation/metasploitable_ssh-port22/5.confirm_setting_is_set.png)

It’s a good practice to check options again. As I found that I forgot to set ‘stop_on_success’ to <true>

![alt text](../evidences/exploitation/metasploitable_ssh-port22/6.set_required_setting.png)

Step 6: Start exploiting.

![alt text](../evidences/exploitation/metasploitable_ssh-port22/7.start_exploit.png)

I found one user with the password after bruteforce and session 1 had opened. 

Step 7: Start interacting with the specified session that has been established with a compromised target system. Here’s what  it does;

![alt text](../evidences/exploitation/metasploitable_ssh-port22/8.start_interation.png)

After I gained access, I made changes in the server. Like; I created a folder and a file. 

![alt text](../evidences/exploitation/metasploitable_ssh-port22/9.making_changes_in_server.png)

### (way2) auxiliary/scanner/ssh/ssh_login

I found another way to gain access in port 22 ssh, the methods are the same, just the difference is setting the ‘current setting’. Here, Instead of ‘stop_on_success’  the ‘verbose’ is set to <true>.

![alt text](../evidences/exploitation/second-way-metasploitable_ssh-port22/4.set_current_setting.png)

This method is much better than the first one, as it bruteforce every username and passwords. In the first method I only found one user, but in this method, I found two users. 

![alt text](../evidences/exploitation/second-way-metasploitable_ssh-port22/7.1.success_i_found.png)

![alt text](../evidences/exploitation/second-way-metasploitable_ssh-port22/7.2.success_ii_found.png)

Two sessions are open and I can use either of it to gain access. 

![alt text](../evidences/exploitation/second-way-metasploitable_ssh-port22/8.session_interaction_and_make_changes.png)

### exploit/multi/http/php_cgi_arg_injection

Next, to identify vulnerability on port 80 which is http port. I used metasploit. 

Step 1: Start console.

![alt text](../evidences/exploitation/metasploitable_http-port80/1.start_console.png)

Step 2: Search for a specific name.

![alt text](../evidences/exploitation/metasploitable_http-port80/2.search_name.png)

Step 3: Use the module and show options.

![alt text](../evidences/exploitation/metasploitable_http-port80/3.use_and_show_options.png)

Step 4: Set the required settings. 

![alt text](../evidences/exploitation/metasploitable_http-port80/4.set_current_setting.png)

Step 5: Run to start exploitation. Then upgrade (-u) a regular Meterpreter session to a more fully featured Meterpreter session. 

![alt text](../evidences/exploitation/metasploitable_http-port80/5.run_session_interaction.png)

Step 6: ‘Shell’ command to spawn an interactive shell session.  

![alt text](../evidences/exploitation/metasploitable_http-port80/6.create_shell_make_changes.png)

After I gained the access, I made some changes inside the server.

### auxiliary/scanner/telnet/telnet_login

Also for exploiting telnet, I used metasploit.

Step 1: Start the console. 

![alt text](../evidences/exploitation/metasploitable_telnet-port23/1.starting_console.png)

Step 2: Search for a specific name.

![alt text](../evidences/exploitation/metasploitable_telnet-port23/2.search_name.png)

Step 3: Use the module and show options.

![alt text](../evidences/exploitation/metasploitable_telnet-port23/3.use_and_show_options.png)

Step 4: Set the required settings. 

![alt text](../evidences/exploitation/metasploitable_telnet-port23/4.set_current_setting.png)

Step 5: Show options to confirm the changes. 

![alt text](../evidences/exploitation/metasploitable_telnet-port23/5.confirm_setting_options.png)

Step 6: Start exploiting.

![alt text](../evidences/exploitation/metasploitable_telnet-port23/6.start_exploit.png)

![alt text](../evidences/exploitation/metasploitable_telnet-port23/7.login_success_shown.png)

Login successful for ‘service’ user and session 1 has opened. 

Step 7: Start session interaction.

![alt text](../evidences/exploitation/metasploitable_telnet-port23/8.session_interation_make_changes.png)

I’ve made some changes in the server after gaining access.

### Ftp

I used hydra to exploit ftp which has the port number 21. Hydra is a tool used for performing brute-force attacks against various types of online services and protocols. It is designed to automate the process of guessing login credentials by systematically trying different combinations of usernames and passwords until the correct combination is found.

Step 1: Use ‘Users.txt’ file and ‘Passwords.txt’ file and brute-force the Username and Passwords.  

![alt text](../evidences/exploitation/hydra_ftp-port21/1.exploiting_using_hydra.png)

Here;

* -L : Flag specifies the path to a file containing a list of usernames.
* -P : Flag specifies the path to a file containing a list of passwords.
* ftp : This indicates the protocol to be used for the  brute-force attack.

After brute-force I could find two Usernames service and postgres.

Step 2: Initiate an FTP connection to the server.

![alt text](../evidences/exploitation/hydra_ftp-port21/2.expoiting.png)

After I login as a service user, I retrieve a file from the FTP server and download it to the local system.

![alt text](../evidences/exploitation/hydra_ftp-port21/download_proof.png)

### Remediation Summary

From this assessment, I would like to inform the lecturer and the head ICT officer of RUB that the server is not ready to be deployed into the internet, there are many ports that are not secure and I recommend all remediation steps and mitigating controls are carefully planned and tested to prevent any unauthenticated access or loss of data.
