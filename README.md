# Content

- [Introduction](#introduction)
- [Install](#install)      
- [Prerequisites](#prerequisites)   
- [Elements of a Minimal Test Plan](#prerequisites)
- [Test Plan](#test-plan)    
- [Collection of API](#collection-of-api)   
    - [List of API](#list-of-api) 
    - [Load the JMeter Script](#load-the-jmeter-script)      
- [Test execution (from the Terminal)](#Test-execution-from-the-Terminal)  
- [Creating JTL and HTML file](#Creating-JTL-and-HTML-file)  
- [Load testing Report](#load-testing-report)  
- [Summary](#summary)  
- [HTML Report](#html-report)
- [Stress Testing](#stress-testing)    
- [Spike Testing](#spike-testing)      
- [Endurance Testing](#endurance-testing)
- [Read Test Data from CSV file in Jmeter](#read-test-data-from-csv-file-in-jmeter)



# Introduction

This document explains how to run a performance test with JMeter against -**Mercury Tours** a travel website where users can book flights, hotels, car rentals, etc.


# Install

- **Java**  
URL: https://www.oracle.com/java/technologies/downloads/

- **JMeter**  
URL: https://jmeter.apache.org/download_jmeter.cgi  
<p align="center">
  <img src="https://github.com/user-attachments/assets/76a1e6ec-a779-4cc0-8665-2fb4b28c0ae7" alt="Image description" />
</p>



- **BlazeMeter:** <br>
For this project, BlazeMeter has been used for the JMX file. <br>
URL: https://chrome.google.com/webstore/detail/blazemeter-the-continuous/mbopgmdnpcbohhpnfglgohlbhfongabi?hl=en
<p align="center">
  <img src="https://github.com/user-attachments/assets/b182d91d-9824-4c48-890d-2e497acc1857" alt="Image description" />
</p>


# Prerequisites
- As of JMeter 4.0, Java 8 and above are supported.
- we suggest  multicore CPUs with 4 or more cores.
- Memory 16GB RAM is a good value.

# Elements of a minimal test plan
- Thread Group

    The root element of every test plan. Simulates the (concurrent) users and runs all requests. Each thread simulates a single user.

- HTTP Request Default (Configuration Element)

- HTTP Request (Sampler)

- Summary Report (Listener, Assertions)

# Test Plan

Right-click on Testplan > Add > Threads (Users) > Thread Group (this might vary depending on the JMeter version you are using)
<p align ="center">
    <img src="https://github.com/user-attachments/assets/fa5ee4a5-e327-42f6-a6e9-ee9679051340" />
</p>

- Name: **Test Plan Name**
- Number of Threads (users): 1 to 10
- Ramp-Up Period (in seconds): 10
- Loop Count: 1  

  1) The general setting for the test execution, such as whether Thread Groups will run simultaneously or sequentially, is specified in the item called Test Plan.

  2) All HTTP Requests will use some default settings from the HTTP Request, such as the Server IP, Port Number, and Content-Encoding.

  3) Each Thread Group specifies how the HTTP Requests should be carried out. To determine how many concurrent "users" will be simulated, one must first know the number of threads. The number of actions each "user" will perform is determined by the loop count.

  4) The HTTP Header Manager, which allows you to provide the Request Headers that will be utilized by the upcoming HTTP Requests, is the first item in Thread Groups.

# Collection of API

- Run BlazeMeter  
- Collect Frequently used API  (for this project, **Login with valid info > Click on flights > fill flight details and preferences > continue > Back to home**)
- Save the JMX file
- Now place the JMX file inside > **apache-jmeter-5.6.3\bin**

    ### List of API 

    - [https://demo.guru99.com/test/newtours/index.php](https://demo.guru99.com/test/newtours/index.php)
    - [https://demo.guru99.com/test/newtours/login_sucess.php](https://demo.guru99.com/test/newtours/login_sucess.php)
    - [https://demo.guru99.com/test/newtours/reservation.php](https://demo.guru99.com/test/newtours/reservation.php)
    - [https://demo.guru99.com/test/newtours/reservation2.php](https://demo.guru99.com/test/newtours/reservation2.php)
    - [https://demo.guru99.com/test/newtours/index.php](https://demo.guru99.com/test/newtours/index.php)


   **OR**
    
  ### Load the JMX file in JMeter  
   - File > Open (CTRL + O)
   - Locate the "mt_thread_01.jmx" file contained on this repo
   - Continue open "mt_thread_01.jmx" to "mt_thread_10.jmx"
   - Open those file
   - The Test Plan will be loaded  

  <p align ="center">
    <img src="https://github.com/user-attachments/assets/1ee8ac5c-72b6-41d2-a406-b605543fbf6f" />
</p>

                                   
# Test execution (from the Terminal)
 
- JMeter should be initialized in non-GUI mode.
- Make sure all assertions and listeners should be disabled before testing in non-GUI mode
- Create a report folder inside the **bin** folder.  
- Run the Command line in the bin folder.

 # Creating JTL and HTML  file
 - jtl file create

```bash
  jmeter -n -t  mt_thread_01.jmx -l mt_thread_01.jtl
```
   
 - HTML file create
  
```bash
  jmeter -g report\mt_thread_01.jtl -o mt_thread_01.html
```

 
Here, 
   	- **n** = non - GUI mode
	- **t** = Load the test plan located
	- **l** = Save the test result's location 
	- **g** = Generate
	- **o** = Output
 
Now open the report folder you will see - a jtl file and an HTML folder there. 
<p align ="center">
    <img src="https://github.com/user-attachments/assets/455647b9-a9c2-420c-9750-ecf38dea3404" />
</p>

Once you click on index.html from the HTML folder you will see the results on any of your default browsers. 
<p align ="center">
    <img src="https://github.com/user-attachments/assets/c9da552f-c7c1-4a28-9b71-4db3c5219265" />
</p>

Now continue the same process for threads(1 to 9) by keeping the Ramp-up period and loop count without any change. 

# Load testing Report

| Concurrent Request  | Loop Count | Ramp-up Period  | Avg TPS for Total Samples  | Error Rate | Total Concurrent API request |
|               :---: |      :---: |      :---: |                      :---: |                        :---: |      :---: |
| 1  | 1  | 10  |0.08  | 0%      | 5   |
| 2  | 1  | 10  |  0.167     | 0%      | 10   |
| 3  | 1  | 10  |  0.20    | 0%   | 15   |
| 5 | 1  | 10  |  0.30  | 0%   | 25   |
| 9  | 1  | 10  |  0.72    | 0%   | 45  |
| 10  | 1  | 10  |  0.8    | 2%   | 50  |

### Summary
- While executing no 5th concurrent requests, we found  1 request got a response code error and the error rate is 2%.
- Server can handle almost concurrent in between 45 to 47 API calls with almost zero (0) error rate.

 
# HTML Report

**Number of Threads 1 ; Ramp-Up Period 10s**
   
Requests Summary             |  Statistics
:-------------------------:|:-------------------------:
![1](https://github.com/user-attachments/assets/9b362090-b029-4c71-b75c-db0cfa7839bc)  |  ![2](https://github.com/user-attachments/assets/9df76f71-f709-49ee-a846-029e0dffd2a0)


Total Transaction  Per Second |
:-------------------------:
![3](https://github.com/user-attachments/assets/ed4268b8-616a-4b1d-be0f-c06d427a8fae)
 

**Number of Threads 2 ; Ramp-Up Period 10s**
   
Requests Summary             |  Statistics
:-------------------------:|:-------------------------:
![4](https://github.com/user-attachments/assets/d0c92f4c-db1e-4132-8faa-3f4781ec2486)  |  ![5](https://github.com/user-attachments/assets/314d3df0-742c-4119-9f9f-047d5a384c8e)


Total Transaction  Per Second |
:-------------------------:
![6](https://github.com/user-attachments/assets/a5e2b569-cbd0-4e87-a30c-45657c57d6d3)


**Number of Threads 3 ; Ramp-Up Period 10s**
   
Requests Summary             |  Statistics
:-------------------------:|:-------------------------:
![7](https://github.com/user-attachments/assets/27ff75d5-beec-41f1-8854-ab05bc8d4dec)  |  ![8](https://github.com/user-attachments/assets/c74dde22-0d63-4985-ba87-39d3259857b0)


Total Transaction  Per Second |
:-------------------------:
![9](https://github.com/user-attachments/assets/96b0a638-b309-44d4-9a82-15332d11cafa)


**Number of Threads 5 ; Ramp-Up Period 10s**
   
Requests Summary             |  Statistics
:-------------------------:|:-------------------------:
![10](https://github.com/user-attachments/assets/3c0938ef-50a9-42c7-8cf5-f8d8cb2b5ce9)  |  ![11](https://github.com/user-attachments/assets/061d94de-e2b6-4000-8dcb-99a0b9f8e743)



Total Transaction  Per Second |
:-------------------------:
![12](https://github.com/user-attachments/assets/cada3d63-aa1a-459a-8870-2c0a8b6cc696)



**Number of Threads 9 ; Ramp-Up Period 10s**
   
Requests Summary             |  Statistics
:-------------------------:|:-------------------------:
![13](https://github.com/user-attachments/assets/073db2e3-25ca-48d5-a05f-4d524ac12827)  |  ![14](https://github.com/user-attachments/assets/a74ea987-5e97-4d00-9069-688b6f9be1ff)



Total Transaction  Per Second |
:-------------------------:
![15](https://github.com/user-attachments/assets/e9e5baeb-e0df-4b92-8c3a-acedbe02ea55)


**Number of Threads 10 ; Ramp-Up Period 10s**
   
Requests Summary             |  Statistics
:-------------------------:|:-------------------------:
![16](https://github.com/user-attachments/assets/91cc74ca-dec5-4a86-860d-39bb170f9c36)  |  ![17](https://github.com/user-attachments/assets/a3a73b4c-6e82-4062-bc85-c3c06162690d)


Total Transaction  Per Second | Errors
:-------------------------:|:-------------------------:
![18](https://github.com/user-attachments/assets/3314e883-6f30-4d93-be78-e08df2f46e74) |  ![19](https://github.com/user-attachments/assets/66cb0e35-7103-4e84-ae9c-e3685423b8cb)






# Stress Testing

Stress Testing is a type of software testing that evaluates how the software responds under extreme conditions. It verifies how robust a system will be, and its response capabilities and error handling when it is subjected to conditions where its normal functioning can be compromised.

**Number of Threads 7 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![a](https://user-images.githubusercontent.com/92669932/189820373-01f812aa-acaa-47fc-a7f2-91e813e23a4a.jpg) |  ![b](https://user-images.githubusercontent.com/92669932/189820402-fcef18b3-cd47-4b60-8ee1-87e1a7e59a01.jpg)

  


**Number of Threads 8 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![c](https://user-images.githubusercontent.com/92669932/189820654-d0f9744c-d05e-462f-88f7-ba8f91125f29.jpg) | ![d](https://user-images.githubusercontent.com/92669932/189820670-b90a99e7-d44a-47f5-8d66-806e571c1fb4.jpg)    



**Number of Threads 9 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![e](https://user-images.githubusercontent.com/92669932/189820708-da2be22b-1718-4f9a-a89a-e5235d6d1e82.jpg)  |   ![f](https://user-images.githubusercontent.com/92669932/189820724-4217425e-491d-4177-918b-347e89281b6b.jpg)

# Spike Testing

Spike testing is a type of performance testing where the demand for an application is suddenly and drastically increased or decreased. Spike testing's objective is to ascertain how a software program will behave under highly variable traffic conditions.

**Number of Threads 15 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![s](https://user-images.githubusercontent.com/92669932/189822076-38361a8b-db25-4e43-98f4-2a582d0244fa.jpg) | ![p](https://user-images.githubusercontent.com/92669932/189822103-fdcd8c85-6d17-4135-af20-a700b5bb05d7.jpg)

# Endurance Testing
An application may be put through endurance testing to see if it can handle the processing load that will be placed on it over an extended period of time. Memory usage is tracked throughout endurance tests to identify potential issues.   

**Start Threads count 6s ; Initial Delay 0s ; Start up Time 10s ; Hold load for 600s ; Shutdown Time 0s**     

Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![e](https://user-images.githubusercontent.com/92669932/189861431-3843b069-8a12-4e38-b527-2a28700f7bf9.jpg) | ![f](https://user-images.githubusercontent.com/92669932/189861468-84b0bd3c-1531-4a30-a7b2-9d9f59964823.jpg)

![t](https://user-images.githubusercontent.com/92669932/189866938-ce1e11e2-9720-4c4f-91a6-6c79e450632b.jpg)

# Read Test Data from CSV file in Jmeter    

- Create a CSV file in the test suite folder and add test data to it.  <br/>

![csv](https://user-images.githubusercontent.com/92669932/189913089-8bab3573-ad13-4d80-b9da-ff8168b953fe.jpg)

- Add a Config Element CSV Data Set Config in Jmeter.   <br/>

![2](https://user-images.githubusercontent.com/92669932/189913286-0ef1bf60-234f-4275-8def-47d815221dab.jpg)   

- Configure ' CSV Data Set Config ' based on the need such as providing path of CSV file and variable names and other configs.   <br/>

![1](https://user-images.githubusercontent.com/92669932/189913690-80380eda-a4df-4e92-901b-5f1424dadcc2.jpg)  

- Run the test to see if data from the CSV file is read and populated in the results.  <br/>

- Run the test to see if data from CSV file is read and populated in the results.    <br/>  


**Number of Threads 13 ; Ramp-Up Period 5s**

<p float="left">
  <img src="https://user-images.githubusercontent.com/92669932/189938100-48702b1a-99a6-4de4-af25-66f069b78e1c.jpg" width="49%" />   
  <img src="https://user-images.githubusercontent.com/92669932/189938110-331e82ad-1e51-465a-a2e8-aec250760351.jpg" width="49%" />   
  <img src="https://user-images.githubusercontent.com/92669932/189938113-dee95de0-4302-41ed-9924-5ddac5836cfe.jpg" width="49%" />    
  <img src="https://user-images.githubusercontent.com/92669932/189938115-2de6ea5e-d90c-4fd1-bcc9-7e3997c52693.jpg" width="49%" />     
</p>



