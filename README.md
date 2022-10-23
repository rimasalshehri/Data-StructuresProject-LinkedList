# Data-StructuresProject-LinkedList
You are assigned as the head manager of a medical facility. You must design and implement the Facility’s working system using linked list,,  
Task: Design and implement Management system for that facility using linked list. Your system must target the patients.  
Operations: the system must include the following operations:
 • Insert patient’s record 
• Delete patient’s record 
• Update patient’s record 
• Show patient’s record 
• Search data in patient’s invoice
• Invoice  
Key Data: The patient record should contain the following items 
• Name of patient 
 • ID of patient
• Phone number of the patient 
• Address of the patient 
• Invoice   
Approach: With the basic knowledge of operations on Linked Lists like insertion, deletion of elements in the Linked list, the patient record management system can be created. Below are the functionalities explained that are to be implemented: 
Check Record: It is a utility function of creating a record it checks before insertion that the Record Already Exist or not. It uses the concept of checking for a Node with given Data in a linked list. 
Create Record: It is as simple as creating a new node in the Empty Linked list or inserting a new node in a non-Empty linked list. 
Smart Search Record: Search a Record is similar to searching for a key in the linked list. Here in the patient record key is the ID number as a unique for every patient. 
Delete Record: Delete Record is similar to deleting a key from a linked list. 
Show Record: It shows the record is similar to printing all the elements of the Linked list. 
Update Invoice : It add 15% of the invoice total only for invoices more than 100 SR. 


Regulations:
1.	ID must be used as a key to distinguish between two different records so while inserting record check whether this record already exists in our database or not if it already exists then immediately report to the user that record already exists and insert that record in the database.
2.	Every new patient’s record should be added in the end of the list
3.	The clerk (user) should get prompted by messages such as “please enter total invoice”.
4.	All the data must be inserted from the clerk (user). 
5.	Delete the Invoices that are less than SR 10. 
6.	Add the VAT (15%) only on invoices more than 100 SR. 


