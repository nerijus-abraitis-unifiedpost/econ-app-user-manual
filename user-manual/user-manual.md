# Euroconnector client-app user manual

## Technical requirements
The minimum requirements for running the software required to operate the Euroconnector client-app are listed below:
- Microsoft Windows 10 or later
- Internet Connectivity


## Getting started 
The Euroconnector client-app is the application used to send and receive invoices via Peppol network. Application is able to handle invoices using [Euroconnector OpenAPI standard definition](https://app.swaggerhub.com/apis-docs/euroconnector/econ-def). The invoices should follow the [Peppol BIS Billing 3.0 standard](https://docs.peppol.eu/poacc/billing/3.0/).


### Installing instructions
The application has fully prepared and ready to use version for Microsoft Windows 10 (or later) platform.

In order to start using it you need to:
- download the latest release of the application from [Releases page](https://github.com/UnifiedPost/econ-client-app/releases);
- extract the downloaded package `euroconnector-clientapp-*-win10-x64.zip` into a local folder, for instance `C:\APPS\euroconnector-clientapp`;
- then click on the executable file `EuroConnector.ClientApp.exe` and now you are ready to run your application for the first time.

### Navigating the application
After you start the `EuroConnector.ClientApp.exe` the following application view should be loaded:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ-first-run-setup.PNG" width=60%>

The next sections explains the functions which are available in the application.

#### Menu item | Setup
In the first run you will be asked to enter the connection credential for the Euroconnector OpenAPI. The API is handled by the Access point provider. The connection credentials are created by the ERP/EDI provider or the Access point provider. If you don't have the credentials, please contact the provider(s).

Once you have the credentials, please enter them into the application **Setup** fields:
 - User name
 - Secret key
 - API URL

and click **[SAVE]** button.

The connection should be established and you will be moved to the [**Home**](#menu-item--home) screen of the application.

Also you will be asked to enter the settings for Inbox and Outbox. Please enter them and click **[SAVE]** button.


#### Menu item | Home
The view presents the dashboard of the application. It contains several parts:
- current date and time;
- the version and some additional information from the Access point API. Information is presented if the connection to the API was established successfully;
- the version of the current application.

![Euroconnector Home](https://einvoice.epay.lt/documentation/.econ-images/econ-home.PNG)

#### Menu item | Inbox
The view like below is displayed when you select the Inbox item:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ-inbox1.PNG" width=75%>

There are few operations available here:
 - View Document Data - retrieves more metadata about newly received document. It depends on Access point provider's implementation how many data is displayed.
 - Download Document - downloads the document content from the API and saves it to the local Inbox folder as BIS3 UBL file. Open that folder in order to read those files.

If you want to download all received documents at once, please click the button **[DOWNLOAD&nbsp;ALL&nbsp;DOCUMENTS]**.

The documents table is not displayed if there is no new documents in the Inbox.

#### Menu item | Outbox
Select the Outbox menu item in order to handle your outgoing documents:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ-outbox2.PNG" width=75%>

The view contains 3 sections:
 - **Outbox Spool** - where to place BIS3 UBL files (documents) in order to get them send out. The sending engine works automatically, every X minutes, which are set in the argument "Minutes between sending documents".
 - **Sent** - where the sent documents will be moved after they are successfully sent out;
 - **Failed** - where the documents are placed if they have been failed during the sending process. The error description could be found next to the original file with the `*.json` extention.


#### Menu item | Logs
Use the Logs view for troubleshooting the events:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ-logs.PNG" width=75%>

You can filter logs by date and log level, do some extra filtering by adding search keywords.
