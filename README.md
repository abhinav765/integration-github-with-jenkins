# integration-github-with-jenkins
# Integration-with-Github-apache-using-Jenkins
In this, I have Integrate Github with Jenkins and Hosted my webpage also I can do real-time changes</br>


## Diagram:- ![965cf1b3-34c9-4877-afb6-b14e8214f932](https://user-images.githubusercontent.com/89704283/156210500-3ff5af67-7564-4606-8acb-4af151f89eb0.jpg)



## set-up step :- 
- Go to AWS account create 2 instance with name <b>Jenkins and Webserver</b>
- Now set all as default only change Configure Security Group <b>(All traffic) for Jenkins and change there from Anywhere</b> and </br> 
  <b>For webserver select HTTP and in custom change Anywhere</b>
- Now Open puttygen load pem file and genrate ppk key and save it 
- Open putty and paste ip of jenkins machine</br>
    <b>Jenkins Machine</b>:- </br>
    * Login with <b> ec2-user
    * `sudo su`</br>
    * `sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo ` 
    * `sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key`
    * `sudo yum upgrade`
    * `sudo yum install java-11-openjdk-devel`
    * `sudo yum install --nobest jenkins`
    * `sudo yum install git -y`
    * `sudo systemctl start jenkins`
    * `sudo systemctl status jenkins`
    * `sudo systemctl enable jenkins`</b>
   
 - Copy the Ip adress of Jenkins machine <b>(IP address:8080)</b>
 - Now Open putty and paste ip of webserver machine</br>
   * Login with <b> ec2-user
   * `sudo su`
   * `yum install httpd -y`
   * `yum install java-11-openjdk-devel`
   * `yum install git -y`
   * `systemctl start httpd`
   * `systemctl status httpd`
   * `systemctl enable httpd`</b>
   
 - Now go to jenkins and go to manage Node 
 - create Node `slave1 perment agent` 
 - Name :- `slave1`
 - Remote root dir :- `home/ec2-user`
 - Label :- `slave1`
 - usage :-`use this node as much as possible`
 - lounch method :- `lounch agents via SSH`
 - Host:- `IP address of Webserver`
 - Creditial:- 
    * add 
    * kind:- `SSH` VN and PK`
    * Discription:- `Slave1_key`
    * Username:-`ec2-user`
    * Enter :- `enter Your pem file key open pem file you have downloaded copy and paste the key`
    * Host key Verify:- `non verifying verification Strategy`
 - All the Configuration has been done. Now your jenkins is connected to Webserver 
 - Go to jenkins create Job name test1 and select free style project 
 - in restrict where this project can be run under that option select label experession</br>
   write slave1
 - Go to build execute shell write `sudo mkdir /root/test1` 
 - now go to job and build now run the job you will see that you have successfully deployed your job  
 
 
 ## Step to connect Github with Jenkins:- 
 - Go to github Create repository with any name then select public and a readmefile 
 - Go to local system open gitbash go to working directory 
 - `git clone https://github.com/rushabhmahale/xyzfilename`
 - `cd workspace`
 - `git remote -v`
 - `nano index.html` <b>(write your content in this file)</b>
 - `git add .`
 - `git commit -m "commit from my local system"` 
 - `git log --oneline`
 - `git status`
 - `git push`
 - now go to your github repository and go to settings there is the option <b>Webhooks</b> add <b>webhook</b>
 - payload url :- </b>copy jenkins url eg:- http://65.2.29.57:8080//github-webhook/ (in last write /github-webhook/)
 - select send everything 
 - add webhook go to webhook redilievery you are successfully connected to jenkins 
 - Now go to jenkins Create job with any name 
 - Select freestyle project 
 - go to scm copy git repo url paste here 
 - Restrict where this project can be run under that label expression Type <b>slave1</b>
 - Build execute `sudo cp -f * /var/www/html` all the github content will be added in your webserver instance in the folder /var/www/html using jenkins 
 - Build triggers select option  github hook trigger at git scm polling 
 - and save now  
 - Build now 

 *Now you will see real time change in your webpage if not refesh browser*
 ![g1](https://user-images.githubusercontent.com/89704283/156204894-df0bd4fe-037e-436a-94dc-0ed8b037e2eb.png)
 
![g2](https://user-images.githubusercontent.com/89704283/156205158-df7e7327-58f0-48aa-b332-0cfcc00f925b.png)

![g3](https://user-images.githubusercontent.com/89704283/156205320-6ff93111-063f-424f-8386-7c6fb302935b.png)

![g4](https://user-images.githubusercontent.com/89704283/156205384-3846a673-423f-404a-a9ae-583d321c61e3.png)
![g5](https://user-images.githubusercontent.com/89704283/156205533-58afd2ac-b6f2-4da8-8149-2ee130f98e7a.png)
![git push](https://user-images.githubusercontent.com/89704283/156205582-1e759e9d-e320-4266-a89c-d67e94cf13f9.png)
![from local to github](https://user-images.githubusercontent.com/89704283/156206062-5c30e813-d148-400a-a307-b81d6513721a.png)
![webserver machine](https://user-images.githubusercontent.com/89704283/156207155-eb280a19-a3a1-43b9-8611-edcfebf7a989.png)
![installinghttpd](https://user-images.githubusercontent.com/89704283/156208861-625aca2e-ffe3-441d-a6b6-bd303fe314c3.png)
![test page apache](https://user-images.githubusercontent.com/89704283/156208957-abd4ac5c-019f-419f-9fd9-856ac5001597.png)
![docker image](https://user-images.githubusercontent.com/89704283/156209908-f569c28d-ad41-47ee-b475-f4e07ef28fc2.png)
![launching container](https://user-images.githubusercontent.com/89704283/156209957-08b00d13-0926-4301-b127-3e7688d7725a.png)

![webhook config](https://user-images.githubusercontent.com/89704283/156210819-015fb544-8bc6-4ce6-9e0d-792401ac2fe0.png)
![awsnode](https://user-images.githubusercontent.com/89704283/156210844-beaf2ae2-849e-4c11-9426-aaaa636691c7.png)
![jenkinsjob](https://user-images.githubusercontent.com/89704283/156210874-8910b2d2-68aa-46f8-9569-ecfad36b51c8.png)
![jenkinsjob2](https://user-images.githubusercontent.com/89704283/156210888-5948f067-98e7-43d4-8db0-a116d426cd7f.png)
![jenkinsjob3](https://user-images.githubusercontent.com/89704283/156210906-64e3743b-c7e3-402f-bd0c-56bfbc6b8f2e.png)
![changeinput](https://user-images.githubusercontent.com/89704283/156211204-e148755c-dc97-4ef7-98b8-a3735a92d03e.png)
![changeoutput](https://user-images.githubusercontent.com/89704283/156211224-9abe7ebe-5785-40b4-ad61-04688d1a47a0.png)
