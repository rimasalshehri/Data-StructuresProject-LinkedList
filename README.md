# Data-StructuresProject-LinkedList using c++
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

//////////////////////////////////////////////////////////////////////////////////////////////////
#include<iostream>
using namespace std;

struct Patient
{
    string name;
    int ID;
    string phone;
    float invoice;
    Patient(string n,int i,string p,float inv):name(n),ID(i),phone(p),invoice(inv)
    {

    }
    Patient()
    {

    }
    bool operator==(const int& key)
    {
        return ID==key;
    }
    bool operator==(const Patient& p)
    {
        return name==p.name  && phone==p.phone && invoice == p.invoice;
    }
    void updateInvoice()
    {
        if(invoice>100)
        {
            invoice=invoice*1.15;
        }
    }
    bool operator<=(const int& inv)
    {
        return invoice<=inv;
    }
    void show()
    {
        cout << ID << "\t:\t" << name << "\t:\t" << phone << "\t:\t" << invoice << endl;
    }
};

struct node
{
    Patient val;
    node* next;
};

class linkedList
{
    node* head;
public:
    linkedList();
    ~linkedList();
    void addAtFront(Patient val);
    void addAtback(Patient val);
    void addAtIndex(Patient val, int ind);
    void deleteAtFront();
    void deleteATBack();
    void deleteAtIndex(int ind);
    void deleteLessthan(int value)
    {
        node *ptr=new node;
        node *dummy=ptr;
        ptr->next=head;
        while(ptr->next!=nullptr)
        {
            if(ptr->next->val<=value)
            {
                node* to_delete=ptr->next;
                ptr->next=ptr->next->next;
                delete to_delete;
            }else
                ptr=ptr->next;
        }
        delete dummy;
    }
    Patient find(int key)
    {
        node* ptr = head;
        while (ptr != nullptr)
        {
            if( ptr->val == key)
            {
                return ptr->val;
            }
            ptr = ptr->next;
        }
        return Patient("",0,"",0);
    }
    int index(int key)
    {
        node* ptr = head;
        int i=0;
        while (ptr != nullptr)
        {
            if( ptr->val == key)
            {
                return i;
            }
            i++;
            ptr = ptr->next;
        }
        return -1;
    }
    bool check(Patient key)
    {
        node* ptr = head;
        while (ptr != nullptr)
        {
            if( ptr->val == key)
            {
                return true;
            }
            ptr = ptr->next;
        }
        return false;
    }
    void update()
    {
        node* ptr = head;
        while (ptr != nullptr)
        {
            ptr->val.updateInvoice();
            ptr = ptr->next;
        }
    }
    void print()
    {
        node* ptr = head;
        while (ptr != nullptr)
        {
            ptr->val.show();
            ptr = ptr->next;
        }
    }
};
linkedList::linkedList()
{
    head = nullptr;
}
linkedList::~linkedList()
{
    while (head != nullptr)
    {
        node* ptr = head;
        head = ptr->next;
        delete ptr;
    }
}
void linkedList::addAtFront(Patient v)
{
    node* ptr = new node();
    ptr->next = head;
    head = ptr;
    ptr->val = v;
}
void linkedList::addAtback(Patient v)
{
    if(head==nullptr)
    {
        addAtFront(v);
        return;
    }
    node* ptr = head;
    while (ptr->next != nullptr)
    {
        ptr = ptr->next;
    }
    ptr->next = new node();
    ptr->next->next = nullptr;
    ptr->next->val = v;
}

void linkedList::addAtIndex(Patient v, int ind)
{
    node* ptr = head;
    for (int i = 0; i < ind-1; i++)
    {
        ptr = ptr->next;
    }
    node* temp = new node;
    temp->val = v;
    temp->next = ptr->next;
    ptr->next = temp;
}
void linkedList::deleteAtFront()
{
    node* ptr = head;
    head = ptr->next;
    delete ptr;
}
void linkedList::deleteATBack()
{
    node* ptr = head;
    while (ptr->next->next != nullptr)
    {
        ptr = ptr->next;
    }
    node* temp = ptr->next;
    ptr->next = nullptr;
    delete temp;

}
void linkedList::deleteAtIndex(int ind)
{
    if(ind==0)
    {
        deleteAtFront();
        return;
    }
    node* ptr = head;
    for (int i = 0; i < ind-1; i++)
    {
        ptr = ptr->next;
    }
    node* temp = ptr->next;
    ptr->next = temp->next;
    delete temp;
}
class PatientList
{
    linkedList patients;
public:
    static int ID;
    bool addPatient(string name,string phone,float invoice)
    {
        Patient p(name,ID++,phone,invoice);
        if(!patients.check(p))
        {
            patients.addAtback(p);
            return true;
        }
        return false;
    }
    Patient search(int Id)
    {
        return patients.find(Id);
    }
    bool delete_Patient(int Id)
    {
        int ind=patients.index(Id);
        if(ind==-1)
        {
            return false;
        }
        patients.deleteAtIndex(ind);
        return true;
    }
    void ShowRecords()
    {
        cout<<"ID\t:\tName\t:\tPhone\t:\tInVoice\n";
        patients.print();
        cout<<"\n\n";
    }
    void UpdateInvoices()
    {
        patients.update();
    }
    void deleteAllInvoicesLessThan10()
    {
        patients.deleteLessthan(10);
    }
};
int PatientList::ID=1;

int main()
{
    
    int choice;
    PatientList pl;
    Patient p;
    string name;
    string phone;
    float invoice;
    int id;
    do
    {
        cout<<"1. Add Record\n";
        cout<<"2. Delete Record\n";
        cout<<"3. Search Record\n";
        cout<<"4. Show Record\n";
        cout<<"5. Update Record\n";
        cout<<"6. Delete Records Having Invoice less than 10\n";
        cout<<"\n0. Exit\n";
        cout<<"\n\n\nEnter 0-6:\t\t";
        cin>>choice;
        switch (choice)
        {
        case 1:
            cout<<"Enter Name of Patient: ";
            cin>>name;
            cout<<"Enter phone of Patient: ";
            cin>>phone;
            cout<<"Enter invoice of Patient: ";
            cin>>invoice;
            if(pl.addPatient(name,phone,invoice))
            {
                cout<<"---------Your Record Has been Added---------\n";
            }
            else 
            {
                cout<<"---------Record Already Exists---------\n";
            }
            break;
        case 2:
            cout<<"Enter ID of Patient: ";
            cin>>id;
            if(pl.delete_Patient(id))
            {
                cout<<"---------Your Record Has been deleted---------\n";
            }
            else
            {
                cout<<"---------Record Already Does not Exists---------\n";
            }
            break;
        case 3:
            cout<<"Enter ID of Patient: ";
            cin>>id;
            p=pl.search(id);
            if(p.name!="")
            {
                p.show();
            }
            break;
        case 4:
            pl.ShowRecords();
            break;
        case 5:
            pl.UpdateInvoices();
            cout<<"---------Invoice Updated---------\n";
            break;
        case 6:
            pl.deleteAllInvoicesLessThan10();
            cout<<"---------Invoices less than 10 Deleted---------\n";
            break;
        }
    } while (choice!=0);
    return 0;
}


