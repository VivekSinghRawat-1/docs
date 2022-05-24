---
title: "General Purpose OCR"
category: "App Services"
tags: ["Document Service", "AI", "ML", "OCR", "Industrial", "Manufacturing"]
---

## 1 Introduction

The [General Purpose Optical Character Recognition](https://marketplace.mendix.com/link/component/118392) app service can help you extract text, tables, and barcodes from images or PDF documents and get output in XML formats in bulk.

### 1.1 Features

* Extract data(text,table and barcode) in XML format from images and pdf documents in bulk and map data to an entity.
* Support [Mendix SSO](/appstore/modules/mendix-sso/)

### 1.2 Limitation

* Currently only supports images(in JPG, JPEG, PNG, BMP, TIFF formats) and Pdf documents. 
* Total documents size cannot exceed 20 MB.
* ABBYY FineReader Engine will not open images larger than 32512*32512 pixels.

### 1.3 Prerequisites

* This app service works best with Studio Pro 8 versions starting with [8.18.15](/releasenotes/studio-pro/8.18/#81815) and 9 versions starting with [9.0](/releasenotes/studio-pro/9.0/).

## 2 Installation

### 2.1 Obtaining the Binding Keys {#obtain-keys}

The General Purpose OCR is a premium Mendix product subject to a purchase and subscription fee. To successfully use this app service in your app, first you need to start a subscription or a trial to get the binding keys.

#### 2.1.1 Starting a Trial

A trial gives everyone in your company one-month of access to the app service. To start a trial, perform the following steps:

1. Go to the [General Purpose OCR](need to edit: https://marketplace.mendix.com/link/component/118388) page in the Marketplace.
2. Click **Try for Free** to open the **Start Your Free Trial** page. Here you can see the **Trial Details** for the app service.
3. Select the check box to agree to the **Terms & Conditions**.
4. Click **Enable Trial**. A page opens and confirms that your request has been received.
5. Wait until your request is processed. It can take more than at least 15 minutes for the system to process your request. After your request is processed, you will receive an email that says the app service is ready to be used. 
6. Click the link in the email to go to the [My Subscriptions](/appstore/general/app-store-overview/#my-subscriptions) page and log in there. This page shows all the products that you have trials for.
7. Click **General Purpose OCR** to open the [service management dashboard](/appstore/general/app-store-overview/#service-management-dashboard).
8. Follow the instructions in the [Creating Binding Keys](/appstore/general/app-store-overview/#creating-binding-keys) section in the *Marketplace Overview* to create binding keys. Save the binding keys somewhere safe. Later you will need to [configure the binding keys](#configure-keys) in your app.

#### 2.1.2 Starting a Subscription

1. Go to the [General Purpose OCR](need to edit: https://marketplace.mendix.com/link/component/118388) page in the Marketplace.
2. Click **Subscribe** to start a subscription.
3. Select your subscription plan.
4. Fill in **Technical Owner** information (**First Name**, **Last Name**, **Email Address**), billing account information, payments and other required information and then place the order. A page opens and confirms that your request has been received.
5. Wait until your request is processed. It can take more than 15 minutes for the system to process your request. After your request is processed, the Technical Owner will receive an email that says the app service is ready to be used.
6. Click the link in the email to go to the [Company Subscriptions](/appstore/general/app-store-overview/#company-subscriptions) page and log in there. This page gives an overview of all the subscriptions of your organization.
7. Click **General Purpose OCR** to open the [service management dashboard](/appstore/general/app-store-overview/#service-management-dashboard).
8. Follow the instructions in the [Creating Binding Keys](/appstore/general/app-store-overview/#creating-binding-keys) section in the *Marketplace Overview* to create binding keys. Save the binding keys somewhere safe. Later you will need to [configure the binding keys](#configure-keys) in your app.

### 2.2 Installing the Component in Your App

To download and install the General Purpose OCR app service in your app, follow the instructions in the [Importing Content from the App Explorer](/appstore/general/app-store-content/#import) section in *Use Marketplace Content in Studio Pro*. After the app service is installed, you can see it in the **App Explorer** and also in the **Document Data Capture Service** category in the **Toolbox**.

## 3 Configuring the Binding Keys {#configure-keys}

Before you deploy an app, you should configure the binding keys in your app as follows:

1.  In the **App Explorer** or the **Project Explorer**, go to **GeneralPurposeOCR** > **Configurations**. **Access_Key** and **Secret_Key** are defined as constants.

    {{< figure src="/attachments/appstore/app-services/intelligent-document-service/configurations-keys.png" alt="Keys under Configurations in a tree view" >}}

2. Double-click the constant for each constant, enter the key you saved and click **OK** to save the changes.    

## 4 Usage

To use the General Purpose OCR, first create an [import mapping](#mapping-file) that defines how to map extracted data from documents to an entity, and then include the [General Purpose OCR activity](#extraction-activity) in a microflow. This microflow should be set up to accept your input documents, extract data from the documents in bulk and then map the data to an entity using the import mapping that you created.

### 4.1 Extracting the Data {#extraction-activity}

1.  In the **Toolbox**, drag **General Purpose OCR** activity from the **Document Data Capture Service** category into your microflow.

    {{< figure src="/attachments/appstore/app-services/intelligent-document-service/intelligent-document-microflow.png" alt="intelligent-document-microflow" >}}

2.  Create a list of documents that inherits from `System.FileDocument`. Documents from where data are extracted should be passed as a list, as shown in the microflow above.
3.  Double-click the **General Purpose OCR** activity to open the dialog box.

    {{< figure src="/attachments/appstore/app-services/intelligent-document-service/intelligent-document-service-dialog-box.png" alt="Intelligent Document Service dialog box" >}}

**Input Section:**

There are three Input Fields users must select, i.e., Document List, Behaviour, and Extraction_Result_Microflow.

4. For **Document List**, click **Edit** to select the **Document List** which inherits from `System.FileDocument`.
5. For **Behaviour**, we have two options sync & async in the same activity.  
Now, click **Edit** to select any one of the Behaviour out of **Blocking_Process** and **Non_Blocking_Process**. 
6. For **Extraction_Result_Microflow**, this field will only be edited/selected in the case of Non_Blocking_Process Behavior chosen by the user.
Now, click **Select** to select the **Microflow** created by the user.
 * Once we receive the data extraction result from the Backend, we will call the Microflow provided in the input **“Extraction_Result_Microflow”** and pass the extraction result in the input parameter of the Microflow. 

**Output Section:**

There are three Output Fields users will have, i.e., Return type, Use return value and Object name. 

7. The **Return type** field is already selected as **GPO.GPOExtractionResult**.
8. For **Use return value**, the user can select any one option from **Yes** and **No**.
9. For **Object name**, the user can type the response object name as **GPOExtractionResult**.


**The output of the activity:**

* Object of GPOExtractionResult entity :

The result of data extraction is returned in the following format for Sync Behaviour and Async Behaviour.

1). **Sync Behaviour (Blocking_Process) :**
     “Behaviour” → “Blocking_Process”
     “Accepted”  → true (If data extraction is successful )
     “ExtractionResponse_GPOExtractionResult” → This association will contain the result of data extraction. 
     
2). **Async Behaviour (Non_Blocking_Process) :**
     “Behaviour” → “Non_Blocking_Process”
     “Accepted”  → true (If data extraction is successful)
     
Above 2 properties will be returned immediately.

Once we receive the data extraction result from the Backend, we will call Microflow provided in the input “Extraction_Result_Microflow” and pass the extraction result in the input parameter of the Microflow.  

* In case of any Exceptions, the response of the activity will be as follows in case of both Sync and Async Behaviour:
 “Behaviour” → “Non_Blocking_Process” / “Blocking_Process”
 “Accepted”  → false
 “ExtractionResponse_GPOExtractionResult” → None/NULL


### 4.2 Checking Statistics on the Usage Dashboard

The **Usage** dashboard shows real-time statistics about the usage of an app service. Perform the following steps to check the real-time statistics:

1. Log into the Marketplace.
2. Go to **My Marketplace** and then do as follows:

    * If you have a trial, click [My Subscriptions](/appstore/general/app-store-overview/#my-subscriptions) on the left navigation menu. This page shows all the products that you have trials for.
    * If you have a subscription, click [Company Subscriptions](/appstore/general/app-store-overview/#company-subscriptions) on the left navigation menu. This page gives an overview of all the subscriptions of your organization.
3. Find **General Purpose OCR** in the list.
4. Click **Usage Dashboard** to show the usage details.


## 5 Technical Provider{#technical-provider}

The AI and OCR technologies used by General Purpose OCR are powered by [ABBYY&reg;](https://www.abbyy.com). The application includes ABBYY® FineReader Engine® 12 SDK © 2019 ABBYY Production LLC. Also, ABBYY and FINEREADER ENGINE are either registered trademarks or trademarks of ABBYY Software Ltd. and cannot be used without the prior written consent of ABBYY Software Ltd.

{{< figure src="/attachments/appstore/app-services/general-purpose-ocr/logo-powered-by-abbyy.png" alt="Technical Provider ABBYY" >}}
