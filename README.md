\# 🚀 Jenkins Master-Agent Setup (AWS)



\## 📌 Project Overview



This project demonstrates how to set up a \*\*Jenkins distributed architecture\*\* using a Controller (Master) and Agent (Slave) on AWS EC2 instances.



\---



\## 🧠 Architecture



Controller (Jenkins Server)

↓ (SSH)

Agent (Build Executor)



\---



\## ⚙️ Technologies Used



\* Jenkins

\* AWS EC2

\* Ubuntu Linux

\* SSH

\* Git



\---



\## 🔥 Step-by-Step Setup



\### 1️⃣ Launch EC2 Instances



\* Instance Type: t3.large

\* OS: Ubuntu

\* Security Group:



&#x20; \* Port 22 (SSH)

&#x20; \* Port 8080 (Jenkins UI)



\---



\### 2️⃣ Install Java (Both Machines)



```bash

sudo apt update

sudo apt install openjdk-21-jdk -y

```



\---



\### 3️⃣ Setup Jenkins (Controller)



```bash

wget https://get.jenkins.io/war-stable/latest/jenkins.war

java -jar jenkins.war --httpPort=8080

```



Access Jenkins:



```

http://<controller-ip>:8080

```



\---



\### 4️⃣ Configure SSH (Controller → Agent)



Generate SSH key on Controller:



```bash

ssh-keygen

```



Copy public key:



```bash

cat \~/.ssh/id\_ed25519.pub

```



Add key to Agent:



```bash

nano \~/.ssh/authorized\_keys

```



Fix permissions:



```bash

chmod 700 \~/.ssh

chmod 600 \~/.ssh/authorized\_keys

```



Test connection:



```bash

ssh ubuntu@<agent-ip>

```



\---



\### 5️⃣ Add Agent in Jenkins



\* Go to: Manage Jenkins → Nodes → New Node

\* Name: agent-1

\* Type: Permanent Agent



Configuration:



\* Remote root directory: `/home/ubuntu`

\* Labels: `linux`

\* Launch method: Launch via SSH

\* Credentials: SSH private key

\* Host verification: Non-verifying



\---



\### 6️⃣ Test Job Execution



Create a Freestyle Job:



Build Step:



```bash

echo "Running on agent"

hostname

```



Restrict job to:



```

linux

```



\---



\## ✅ Output



The job executes on the agent machine:



```

Running on agent

ip-172-31-xxx-xxx

```



\---



\## 🎯 Key Learnings



\* Jenkins distributed architecture

\* Controller vs Agent concept

\* SSH-based authentication

\* Remote job execution

\* AWS EC2 setup



\---



\## 🚀 Outcome



Successfully implemented a \*\*Jenkins Master-Agent setup\*\* where:



\* Controller schedules jobs

\* Agent executes jobs

\* Communication is done via SSH



\---



\## 📸 Future Improvements



\* Add screenshots of setup

\* Convert to Jenkins Pipeline

\* Integrate with GitHub (auto trigger)

\* Add multiple agents



\---



\## 👨‍💻 Author



Mohit Verma



