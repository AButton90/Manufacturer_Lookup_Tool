# Manufacturer Lookup Tool
A desktop application that scrapes product information from a manufacturer site and compares it to the data on the CRM system.

## Application Context
[TecEx](https://tecex.com/) is a company that provides customs compliance solutions through turnkey Import or Export Representation (IOR) services, serving as an Exporter of Record (EOR) and offering full door-to-door (DDP) solutions across various sectors. They use [Salesforce](https://www.salesforce.com/eu/?ir=1) as their Customer Relationship Management (CRM) tool.

TecEx is committed to delivering exceptional client service and have a strong focus on scalability of their technology. To achieve this, the company's Cloud team, creates innovative applications that automates processes, streamlines workflows, and eliminates manual errors. The aim is to ensure that the company can efficiently handle increasing demands from clients while maintaining a high level of service quality.

Accurate classification of goods is essential for ensuring compliance with customs regulations. Incorrectly classifying goods can result in fines, delays, and other penalties. By researching and accurately determining export data for each item they are handling, TecEx can ensure that their clients are in compliance with customs regulations and avoid any potential problems at the border. Additionally, accurate product classification is also important for ensuring that clients are paying the correct tariffs and taxes. 

Various manufactureres provide public resources online where product export data can be found.  

As part of my role in TecEx's Cloud team, I developed this Manufacturer Lookup Tool.

## Application Overview

The Manufacturer Lookup Tool was created to automate the process of gathering product export data from various manufacturers, such as Cisco Systems. TecEx retains information on all Cisco products shipped in Salesforce, and consults the Cisco site for export data such as HS Code, ECCN Number, and Encryption when shipping new products. It is also important to keep the data on the CRM system up-to-date in case of any changes to the Cisco database.

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_Process.png">
</p>

### Process
Upon start, the following screen appears:

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_Start.png">
</p>

The tool has two options for retrieving product codes:
  1. **Local File** - used for new products with no data in the CRM system, the product codes are provided in an Excel file.
  2. **Salesforce** - the tool pulls data directly from Salesforce, with the option to filter the data.

Once the user submits the product codes, the tool navigates to the Cisco site and searches for the product information using the Selenium Python library. The search results are scraped and provided to the user in an Excel file.

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_CS_Search.png">
</p>

The search results are provided in a table as shown below, using XPaths, the tool will scrape all the product export data. If multiple result pages exist, the tool will navigate to each page and continue scraping.

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_CS_Results.png">
</p>

### Results

The scraped results are provided to the user in an Excel file, the results look different based on the process chosen.

#### Local File

The local file results provide the scraped data for each product code. If no information is found for a product code, the row is highlighted in yellow. If multiple results exist for a product code, the column's value is a comma-separated string of the results, highlighted in red.

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_LF_Result.png">
</p>

#### Salesforce
When using the tool to scrape data from Salesforce, the tool performs an analysis between the data on the Cisco site and the data in Salesforce. 

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_SF_Result.png">
</p>

If there are differences between the two systems, they are highlighted: 

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_SF_Color.png">
</p>

  1. **Red** – Multiple results for the field were found on the Cisco site.
  2. **Orange** – There are differences between the Salesforce and Cisco data.
  3. **Green** – The Salesforce and Cisco export data are the same.
  4. **Yellow** – The product was not found on the Cisco site.

Once the user has reviewed the differences between what is on the CRM system and what is provided on the Cisco site, they have the option to update the CRM system with the Cisco data.

<p align="center">
  <img width="739" height="354" src="https://github.com/AButton90/Manufacturer_Lookup_Tool/blob/main/images/Lookup_Tool_SF_Update.png">
</p>

In conclusion, the Manufacturer Lookup Tool streamlines the process of gathering and comparing product export data, reducing manual errors, and increasing efficiency. By using this tool, TecEx can ensure that their clients are in compliance with customs regulations and avoid potential penalties, fines, and delays.

## Python Libraries

The follwing Python libraries were used in the Attachment Tool desktop app:

- PySimpleGUI
- simple_salesforce
- selenium
- openpyxl
- pandas, numpy, math
- collections
