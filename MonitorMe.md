## MonitorMe
by <img src="resources/images/velocity.png" width="90" height="30">

### Table of Contents

- Overview
- Mission
- User Journey
- Requirements
- Design Constraints

## Overview
  **MonitorMe** is a new patient monitoring product from Stayhealthy Inc. This document describes high-level architecture of MonitorMe’s local-standalone IT infrastructure in hospitals. It documents key requirements and features extracted from clients requirements and research on similar products on market. A software and hardware architecture that satisfies these requirements is presented in this document.

## Mission
  Stay Health Inc. is on a long journey to provide End to End support for hospitals. The company already has a two popular SaaS application **MonitorThem** and **MyMedicalData** in the market. **MonitorMe** aims to close the gap between Cloud based Saas applications to inhouse patient monitoring requirements. 

## User Journey
  **MonitorMe** has two unique user groups/Actors.
  1. Nurse Station Users / **Kiosk User**
       This user monitors patients on a monitoring screen set up at each nurses station.
     
     ![Kiosk User!](/resources/images/KioskUserStory.png "Kiosk User")
       ### Nurse Station Users journey
         * User logs in to Kiosk
         * User observes the patient's vitals which rotate every every 5 seconds
         * User can review history and filter patient vitals through filters
         * User can generate holistic snapshot for a patient and upload it to 'MyMedicalData'
      
  3. On the go Users / **Mobile Users**
       This user monitors patients patients through a Push notification on a mobile app.

     ![Mobile User!](/resources/images/MobileUserStory.png "Mobile User")
       ### Mobile Users Journey
         * User downloads and registers through mobile app
         * User receives alerts through push notification

## Requirements
  The architecture for **MonitorMe** must support the below requirements

  ### 1. Availability
   This is a critical system requirement as the patients needs to be monitored constantly. The system must be available throughtout the day. Redundancy must be built in for patching and maintenance activity. All the data from patient vitals must be read through a persistent queue with alteast 2 consumers for each vitals to provide redundancy.
  ### 2. Flexibility
   The design must be able to accommodate new monitoring vectors as the system grows. It is expected that newer patient monitoring technology might emerge and this must be part of the sofware design for monitoring. New monitoring metrics must be as simple a plug-n-play with minimum effort to code.
  ### 3. Security
   This is of the highest concern and a critical requirement. The patient vitals are highly confidential. The data must only be accessible to authorized user and behind a credential MFA gateway. Also the data needs to be encrypted both at transmit and rest.
  ### 4. Scalability
   This is not of much concern as we know what is the maximum number of patients to be monitored by one **MonitorMe** instance. A fixed hardware requirement is enough to meet the requirement.
  ### 5. Performance
    This is of the highest concern and a critical requirement. The system must be capable of processing, storing, analyzing and displaying huge amount of data accurately to the Medical professional. The application must be responsive enough to alert users in case of any deviation
  ### 6. Fault Tolerance
   This is of the highest concern and a critical requirement. The system must function even incase of any disruption for patient vital feeds or sofware/network/hardware glitches. Multiple redundance needs to be in place as well as code to be written such that data received, whatever the quality may be needs to be stored with metadata capturing the fault/missing data
  ### 7. Configurability
   This is one of the key features expected. The system must be highly configurable in terms of setting alerts for each patient. The alerts for vitals deviation might vary drastically based on patients age, medical history, current ailments and so on. All the parameters to monitor must be configurable.

## Design Constraints
  **MonitorMe** is an on-prem solution. All the system requirements must be met will limited hardware as there will be space/power/budget constraint. Also the hardware and software need to be maintained and updated on-site. Secure Network needs to be opened to send data to **MyMedicalData** Saas application and to push notification servers.
## High-Level Architecture
  
  ![High-Level Architecture!](/resources/images/High-Level-Architecture.png "High-Level Architecture")

  This is a user-centric architecture, user interface must be well designed with touch screens in mind for ease of use. Since the system also needs to support mobile push notification, crossplatform framework may be used to achieve the same.
  This Architecture uses a combination of Traditional/Monolithic framework for storing and displaying data, Event-based architecture for ingesting data and push notification, and Micro-services architecture for analyzing patient data.
  The different framework was decided based upon the application requirements to be hosted on Hospital site. A polyglot architecture fits the bill perfectly as we optimizing hardware based on software/system requirements.
## Component-Level Architecture

