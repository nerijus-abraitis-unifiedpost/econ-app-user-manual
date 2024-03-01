# Euroconnector client-app user manual

## Technical requirements
The minimum requirements for running the software required to operate the Euroconnector client-app are listed below:
- Microsoft Windows 10 or later
- Internet Connectivity


## Getting started 
The Euroconnector client-app is the application used to send and receive invoices via Peppol network. Application is able to handle invoices using [Euroconnector OpenAPI standard definition](https://app.swaggerhub.com/apis-docs/euroconnector/econ-def). The invoices should follow the [Peppol BIS Billing 3.0 standard](https://docs.peppol.eu/poacc/billing/3.0/).


## Installing instructions
The application has fully prepared and ready to use version for Microsoft Windows 10 (or later) platform.

In order to start using it you need to:
- download the latest release of the application from [Releases page](https://github.com/UnifiedPost/econ-client-app/releases);
- extract the downloaded package `euroconnector-clientapp-*-win10-x64.zip` into a local folder, for instance `C:\APPS\euroconnector-clientapp`;
- then click on the executable file `EuroConnector.ClientApp.exe` and now you are ready to run your application for the first time.

## Navigating the application
After you start the `EuroConnector.ClientApp.exe` the following application view should be loaded:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-setup.png" width=75%>

The next sections explains the functions which are available in the application.

### Menu item | Setup
In the first run you will be asked to enter the connection credential for the Euroconnector OpenAPI. The API is handled by the Access point provider. The connection credentials are created by the ERP/EDI provider or the Access point provider. If you don't have the credentials, please contact the provider(s).

Once you have the credentials, please enter them into the application **Setup** fields:
 - User name
 - Secret key
 - API URL

and click **[SAVE]** button.

The connection should be established and you will be moved to the [**Home**](#menu-item--home) screen of the application.

Also it is important to setup the working data locations for the application:
| Setting name           | Description |
|------------------------|-------------|
| Outbox spool directory | where the outgoing UBL files should be dropped |
| Outbox directory       | where the sent files will be saved | 
| Inbox directory        | where the received files will be saved | 
| Failed directory       | where the files will be moved in case of an error | 

Don't forget to press the **[SAVE]** button after you set those arguments.


### Menu item | Home
The view presents the dashboard of the application. It contains several parts:
- current date and time;
- the version of the application;
- the version and some additional information from the Access point API. Information is presented if the connection to the API was established successfully.

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-home1.png" width=80%>

### Menu item | Inbox
The view as presented below is displayed when you select the Inbox item:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-inbox-notes.PNG" width=100%>

Inbox view contains a table with the received documents which could be as follows:
 - Invoice
 - CreditNote
 - MessageLevelResponse
 - InvoiceResponse

There are a few actions available in the table:
| Action             | Description |
|--------------------|-------------|
| View document data | retrieves more metadata about the document. It depends on Access point provider's implementation how many data is displayed. |
| Download document  | downloads the document content from the API and saves it to the local Inbox folder as a file in a original document's format. Open that folder in order to read those files  | 
| Invoice response   | allows Customers to respond to the received invoice and let the Suppliers know whether they accepting it or not. Click [here](#triggering-invoice-response) to find out more  | 
| Response status   | redirects to the related documents (invoice or response message)  | 


The data in the table depends on the selected filtering conditions which could be set in the filter dialog box by clicking the button **[FILTER]**:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-inbox-filter.png" width=50%>

The documents table is not displayed if there is no documents in the Inbox according the selected filter. By start using the application the default filter is set which retrieves documents created in the last 10 days. 

### Triggering Invoice response

The [Peppol Invoice response message](https://docs.peppol.eu/poacc/upgrade-3/2023-Q4/profiles/63-invoiceresponse/) is a standardized electronic document exchanged between business partners through the Peppol network. This message serves as a confirmation or response to a previously sent Peppol Invoice. It typically includes information about the status of the invoice, such as acceptance, rejection, or other relevant updates.
 
 The example below presents how to send the response to an invoice:
 
<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-imr.png" width=50%>

 - Choose the response code from the drop-down box
 - Add some description
 - Send the response by clicking button **[SEND]**
 - Check the response status by clicking on an icon "Response status" which changes the view to Outbox with the reference to the received invoice
 
 > The invoice response is generated according the [Peppol Invoice response message](https://docs.peppol.eu/poacc/upgrade-3/2023-Q4/profiles/63-invoiceresponse/) standard
 
### Menu item | Outbox
The Outbox view works in the same way as an Inbox, the only difference is that it presents the sent documents and it has separate filtering conditions.

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-outbox.PNG" width=100%>

The document types are available:
 - Invoice
 - CreditNote
 - InvoiceResponse

> There is no possibility to send MessageLevelResponse as it is sent by Access point server.

### Menu item | Send Documents

Use this section in order to handle your outgoing documents:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-send-documents.PNG" width=85%>

The view contains 3 sections:
 - **Outbox Spool** - where to place BIS3 UBL files (documents) in order to get them send out. The sending engine works automatically, every X minutes, which are set in the argument "Minutes between sending documents". Also it is possible to put and send files manually  by clicking **[ADD DOCUMENTS]** and then **[SEND DOCUMENTS]**
 - **Outbox** - where the sent documents will be moved after they have been sent. The status of the sent document can be verified in a  [**Outbox**](#menu-item--outbox) view.
 - **Failed** - where the documents are placed if they have been failed during the sending process. The error description could be found next to the original file with the `*.json` extention.

### Menu item | Transformations

There is an extra feature in the application for converting a few most popular Lithuanian e-invoice formats to the BIS3 standard UBL. This option lets you to
Use this section in order to handle your outgoing documents:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-tr.PNG" width=90%>

Transformations engine is based on a XSLT v2.0 programming language which is mostly used for transforming XML documents into different structures or formats. It provides a powerful and expressive framework for transforming XML documents, and it is widely used in various applications, including data integration, document generation, and web development.

This option lets you to customize the existing transformations and also to add your own as well. All the transformation source files (*.xsl) are stored in a sub-folder "Transformations" which is located in the application's working directory, like in a sample below:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-tr-folder.PNG" width=50%>

All those transformations can be enabled from the application by clicking **[CREATE]** and then creating a transformation setup item:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-tr-create.PNG" width=50%>

- Select the XSLT name from the drop-down box
- Set the source directory for the input files to be transformed
- Set the destination directory for the output files which will be created after the transformation. It is useful to note that destination could be set the same folder as the "Outbox spool directory" in order to send the converted file automatically.

#### Create and send simple invoice (CSV transformation)
There is a potential risk that a small suppliers can face with a situation when they need to create a BIS3 standard invoice which is not an easy task. For that reason a separate CSV invoice format is prepared. The invoice data are handled by Excel application via particular *template** (Excel sheet) and then data are exported as (saved as) a CSV file. The given CSV file should be moved to the "Source directory" of the "CSV-to-BIS3" transformation and the result in BIS3 format is generated in the "Destination directory". Then the BIS3 xml file could be sent via the same application using  [**Send Documents**](#menu-item--send-documents) menu item.

> *The invoice template for CSV can be found in the sub-folder "Templates" which is located in the application's working directory.

Example of CSV template and exported data:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-csv-template1.png" width=100%>

- Multiple lines where each line refers to a line item of the invoice (yellow mark in the sample);    
- CSV file contains only one invoice;
- CSV field separator is a semicolon symbol “;”
- First line always contains a header with field names. Every field has its dedicated position in the file (according the excel layout the positions are the columns A, B, C …);
- All lines belonging to one invoice have a value in a specific column in common (e.g. InvoiceNo, IssueDate, Sender…, Receiver …). This is called the “grouping key” or “grouping field”.

#### Notes for Rivile transformation 
The original Rivile data file misses the required information for BIS3. For that reason the transformation file must be updated before the first use:
 - Open the file "Rivile-to-BIS3.xsl" with a Notepad 
 - Enter the Supplier's data (name, reg.number, VAT number & etc.) by changing the variables which name starts with `Sender*`
 - Save the file and close it. You're ready to use the transformation.

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-tr-rivile.png" width=80%>


### Menu item | Logs
Use the Logs view for troubleshooting the events:

<img src="https://einvoice.epay.lt/documentation/.econ-images/econ2-logs.PNG" width=80%>

You can filter logs by date and log level, do some extra filtering by adding search keywords.
