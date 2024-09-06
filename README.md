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



- **BlazeMeter:** <br
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
- Number of Threads (users): 1 to 9
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
   - Continue open "mt_thread_01.jmx" to "mt_thread_09.jmx"
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

| Concurrent Request  | Loop Count | Avg TPS for Total Samples  | Error Rate | Total Concurrent API request |
|               :---: |      :---: |                      :---: |                        :---: |      :---: |
| 1  | 1  | 3.350  | 0%      | 212   |
| 2  | 1  |  7     | 0%      | 424   |
| 3  | 1  |  11    | 0.47%   | 636   |
| 4  | 1  |  14.1  | 0.59%   | 848   |
| 5  | 1  |  17.6  | 0.94%   | 1060  |
| 6  | 1  |  20    | 1.18%   | 1272  |

### Summary
- While executing 3 concurrent requests, found  636 request got connection timeout and error rate is 0.47%.
- Server can handle almost concurrent 424 API calls with almost zero (0) error rate.

 
# HTML Report

**Number of Threads 1 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![1](https://user-images.githubusercontent.com/92669932/189543492-df0751ca-3642-4e3f-a050-0454e38117ef.jpg)  |  ![2](https://user-images.githubusercontent.com/92669932/189543499-17c168a2-5b32-4710-9bc0-df7a2b3656c7.jpg)

**Number of Threads 2 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![3](https://user-images.githubusercontent.com/92669932/189543781-8e545531-a134-4dfd-b6bc-36b6539668b5.jpg) |  ![4](https://user-images.githubusercontent.com/92669932/189543783-37624029-b0ea-4671-b5e7-e158453b6d7c.jpg)


**Number of Threads 3 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![5](https://user-images.githubusercontent.com/92669932/189543851-f5ee4f83-275f-4c9d-b716-748380ab337e.jpg)  |  ![6](https://user-images.githubusercontent.com/92669932/189543857-e2042257-9410-4a04-a301-e89631204291.jpg)


**Number of Threads 4 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![7](https://user-images.githubusercontent.com/92669932/189543865-5acac49a-e858-4ce0-95ce-92500d1a1cf0.jpg)  |  ![8](https://user-images.githubusercontent.com/92669932/189543871-749aaf77-1639-4de4-9f59-5476c63ced98.jpg)


**Number of Threads 5 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
![9](https://user-images.githubusercontent.com/92669932/189543881-995a888b-c63b-4f38-8b42-d21140704dfc.jpg)  |  ![10](https://user-images.githubusercontent.com/92669932/189543883-8229a05a-6a96-41da-85c8-d8ae587ebcae.jpg)


**Number of Threads 6 ; Ramp-Up Period 10s**
   
Requests Summary             |  Errors
:-------------------------:|:-------------------------:
 ![11](https://user-images.githubusercontent.com/92669932/189543896-bba2da13-370e-438c-84e9-88439c8e307e.jpg) |  ![12](https://user-images.githubusercontent.com/92669932/189543902-851bd50a-95a7-435e-8df2-a6c615786109.jpg)   



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



