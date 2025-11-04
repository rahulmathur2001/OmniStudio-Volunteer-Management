# OmniStudio-Volunteer-Management
An end-to-end OmniStudio solution using FlexCards, OmniScripts, and DataRaptors to manage volunteer shift registration, including dynamic eligibility checks

🚀 Project Overview

This project demonstrates how to leverage OmniStudio tools — including FlexCards, OmniScripts, Integration Procedures, and DataRaptors — to design an interactive volunteer management application directly within Salesforce.

Volunteers can:
*View available shifts with live data.
*Check their eligibility based on training completion.
*Join a specific shift using an intuitive guided form.
*Automatically update Volunteer and Shift records in Salesforce.

🧩 OmniStudio Components Used
1. FlexCard – AvailableShiftsCard
*Displays all upcoming volunteer shifts.
*Shows Shift Name, Date, and Slots Available.
*Includes a “Join Shift” button that launches the OmniScript with the selected shift ID.

2. OmniScript – **JoinShift**
*Guided form for volunteers to register for a shift.
*Includes steps for:
  -Entering volunteer information.
  -Checking training status and eligibility.
  -Confirmation before submission.
*Integrates with DataRaptors and Integration Procedures to fetch and post data.

3. Integration Procedure – **VolunteerShiftHandler**

Handles backend orchestration:
   -Extracts Volunteer and Shift data.
   -Sets eligibility automatically (via Set Values).
   -Updates the Volunteer record using DataMapperPost.


4. Data Mapper
Name	                   Type	          Purpose
GetAvailableShift	       Extract	      Retrieves all available shifts from Salesforce
GetVolunteerDetails	     Extract	      Fetches volunteer details (age, training status, etc.)
PostVolunteerDetails	   Post	Updates   Volunteer record with eligibility and selected shift
UpdateShiftSlots	Post	 Decrements     available slot count after volunteer joins


⚙️ Data Model
Objects Used:-
1.)Volunteer__c 
   Name
   Age__c
   Training_Status__c
   Eligibility_Status__c
   Joined_Shift__c (Lookup to Shift)
2.)Shift__c
   Name
   Date__c
   Slots_Available__c

🔁 Flow Summary
graph TD
A[FlexCard: Available Shifts] -->|Select Shift| B[OmniScript: JoinShift]
B --> C[Integration Procedure: VolunteerShiftHandler]
C --> D[DataMapper Extract: GetVolunteerDetails]
C --> E[Set Values: Determine Eligibility]
C --> F[DataMapper Post: PostVolunteerDetails]
C --> G[DataMapper Post: UpdateShiftSlots]

🧠 Key Logic
Eligibility Logic (Set Values)
{{#eq(DataMapperExtract[0].TrainingStatus,"Yes")}}Eligible{{/eq(DataMapperExtract[0].TrainingStatus,"Yes")}}
{{#eq(DataMapperExtract[0].TrainingStatus,"No")}}Not Eligible{{/eq(DataMapperExtract[0].TrainingStatus,"No")}}

FlexCard → OmniScript Input Mapping
Key	        Value
ShiftId	    {{ID}}

🧰 Tools & Technologies
Category	Tool
Platform	Salesforce OmniStudio
UI Components	FlexCards, OmniScripts
Data Integration	DataRaptors, Integration Procedures
Logic	Set Values, Conditional Display
Deployment	Lightning App Builder

🧪 Deployment & Testing Steps
1.) Deploy Components
   Import FlexCard JSON.
   Import OmniScript JSON.
   Import Integration Procedure and DataRaptors.
2.)Add FlexCard to Lightning Page
   Go to App Builder → Add FlexCard Component → select AvailableShiftsCard.
3.)Test in Runtime
   View available shifts.
   Click “Join Shift”.
   Fill volunteer form → Submit.
   Confirm record updates in Volunteer__c and Shift__c.

📸 Screenshots
FlexCard View	OmniScript Form
<img width="1430" height="267" alt="Screenshot 2025-11-04 at 6 56 53 PM" src="https://github.com/user-attachments/assets/c2898a55-0a5a-499e-b094-4231d2ba8ebe" />
<img width="1005" height="481" alt="Screenshot 2025-11-04 at 6 58 49 PM" src="https://github.com/user-attachments/assets/82f277b0-e98c-446c-a24d-46b25bed32fc" />



👨‍💻 Author
Rahul Mathur
Salesforce Developer | OmniStudio Specialist
🔗 LinkedIn
 • 💻 GitHub
 • ✉️ rahulmathurjuly@gmail.com

🏁 Future Enhancements
Add approval step for volunteer eligibility.
Integrate email notifications using Messaging Templates.
Create Shift Summary Dashboard using OmniAnalytics or Tableau CRM.
