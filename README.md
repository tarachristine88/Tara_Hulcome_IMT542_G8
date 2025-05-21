# **G8: Improve access methodology of existing information: 'The Diary Project' API**

## **1. About**

As part of ‘The Diary Project’, my information structure will host a structured dataset of personal (dummy) diary entries and make it accessible via a simple web-based API. 

### **1.1. Use** 

Users will be able to filter the diary entries (initially by country - but future uses will extend to themes, years and a variety of other filters), enabling them to analyze over 22 years of data in new and interesting ways.

### **1.2. Audience**

In the pilot phase, the audience will be strictly limited to the diary’s owner and project developer (i.e., myself). Future iterations of ‘The Diary Project’ may see the audience expand to include other authorized users, such as family members.
 
### **1.3. Access**

The diary data will be accessible to the user on their personal device via a public web link and will be read-only, served over HTTPS using Flask and nGrok.

## **2. Methodology**

-	I created 300 dummy diary entries using a large language model (ChatGPT). I decided not to use my authentic personal diary entries to maintain information security and data privacy while testing the API development process.

-	These dummy diary entries were structured into JSON format (see example in Section 5) and saved as ‘tara_diary_examples.json’.

-	I prompted the large language model (ChatGPT) to tag each entry with relevant metadata such as date, year, country, topics, people mentioned, and sensitivity level. I also included an entry_text field containing placeholder text. 

-	A Flask web server was written to load and serve the structured file through a RESTful endpoint.

-	nGrok was used to expose the local server to the web for easy public access.

-	In the initial pilot phase, the JSON file structure will be updated manually as new entries are created or tagged.

## **3. Access**


### **Step 1: Retrieve public API URL**

-	Once Flask is running and the local server is exposed using nGrok, copy the public HTTPS link shown in the terminal: https:// ee80-193-37-33-62.ngrok-free.app

### **Step 2: Navigate to endpoint**

-	Append */diary* to the end of the URL, and follow this link in your browser: https:// ee80-193-37-33-62.ngrok-free.app/diary

### **Step 3: View in browser and send the request**

-	After opening this link in your browser, the server will respond with all diary entries in a JSON array. Select ‘Pretty print’ for a more readable format (optional).

### **Step 4: Experiment with the data**

-	In the URL, replace */diary* with */entries?country=Australia*. Now, you can experiment with identifying the diary entries written in different countries. The server will return blocks of structured data containing ‘country’, ‘entry_text’ and ‘place’ fields.
-	Future versions of this API will enable you to filter by other interesting variables, such as year and theme.

### **Step 5: Refresh the data for updates**

-	If the JSON file on the server is updated, reload the browser to get the latest version.

### **Step 6: Retrieve information**

-	The API only supports GET requests. This means you can retrieve and save the JSON data for your own use, but you cannot modify it.

## **4. Structure**

Each dummy diary entry is a structured JSON object with the following fields:

| **Field** | **Type** | **Description** |
| :----------- | :----------: | :---------------------: |
| "entry_id" | String | A unique identifier assigned to each diary entry in ‘YYYY-MM-DD-###’ format |
| "date"      | String | Date of the entry in ‘YYYY-MM-DD’ format |
| "year"      | Number | Year of the entry in ‘YYYY’ format |
| "country" | String | Name of country in which the entry was written (i.e., Australia, Fiji, Indonesia) |
| “place” |  String | Type of place referred to in the entry (i.e., work, university, home) |
| “entry_text”|  String | Qualitative diary entry text |
| “topics” |  String, Array | Broad topics referred to in the diary entry text (i.e., travel, relationships, weather) |
| “people_mentioned” | String, Array | Names of people referred to in the diary entry text (i.e., Phil, Jess, Dad) |
| “tags” | String, Array | Specific keywords referred to in the diary entry text (i.e., challenge, stress, discovery) |
| “ocr_confidence” | Number | A number representing the level of certainty in the accuracy of the diary entry (i.e., 0.94 = 94% certainty) |
| “sensitivity” | String | An information security feature that classifies sensitivity levels, making it easier to apply appropriate security controls to higher-risk content (i.e., "confidential_personal") |
| “audit_log” | String | An information security feature that maintains an audit trail, logging attempts by unauthorized users to gain access. |


## **5. Examples**

### **5.1. Example JSON entry** 

![image](https://github.com/user-attachments/assets/e01fb91b-f591-428d-ab5a-6eeb13b95b09)

### **5.2. Example request and response** 

-	This example shows a request for all (dummy) diary entries that were written in the USA.
-	To access, the user appended the URL as follows: https:// ee80-193-37-33-62.ngrok-free.app/entries?country=USA
-	The response is structured as a block of JSON data containing ‘country’, ‘entry_text’ and ‘place’ fields (where "country": "USA").

![image](https://github.com/user-attachments/assets/6066fbfb-5935-49cd-adc2-da2412b564bd)

