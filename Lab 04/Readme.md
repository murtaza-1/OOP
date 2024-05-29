Q1
#include<iostream>

using namespace std;

class book{
	private:
	    string name;
	    string author;
	    int ISBN;
	    int totalpages;
	    int currentpagesread;
	    
	public:
		//default constructor function
		book() {
			name="";
			author="";
			ISBN=0;
			totalpages=0;
			currentpagesread=0;
		}
		
		//parameterized constructor function
		book(string aname, string aauthor, int aisbn, int total, int current) {
			name=aname;
			author=aauthor;
			ISBN=aisbn;
			totalpages=total;
			currentpagesread=current;
		}
		
		//function to update pages and to check if book is finished
		void read() {
			if(currentpagesread<totalpages) {
				currentpagesread++;
				cout<<"you have read the page "<< currentpagesread<<endl;
			} else {
				cout<<"book is finished"<<endl;
			}
		}
};

int main () {
	
	//initializing a object of the class
	book Book("harry potter","jk-rowling",234567,3,0);
	
	//attempted to read 4 pages
	Book.read();
	Book.read();
	Book.read();
	Book.read();
	
	
	
}
Q2
#include<iostream>

using namespace std;

class book{
	private:
	    string name;
	    string author;
	    string ISBN;
	    int totalpages;
	    int currentpagesread;
	    
	public:
		//default constructor function
		book() {
			name="";
			author="";
			ISBN="";
			totalpages=1000;
			currentpagesread=0;
		}
		
		void set_name(string aname){
			name=aname;
		}
		
		void set_author(string aauthor) {
			author=aauthor;
		}
		
		void set_isbn(string aISBN) {
			ISBN=aISBN;
		}
		
		
		//function to update pages and to check if book is finished
		void read() {
			if(currentpagesread<totalpages) {
				currentpagesread++;
				cout<<"you have read the page "<< currentpagesread<<endl;
			} else {
				cout<<"book is finished"<<endl;
			}
		}
		
		//function to display all info about books
		void showBookInfo() {
            cout<<"Name: "<<name<<endl;
            cout<<"Author: "<<author<<endl;
            cout<<"ISBN: "<<ISBN<<endl;
            cout<<"Total Pages: "<<totalpages<<endl;
            cout<<"Pages Read: "<<currentpagesread<<endl;
        }
};

int main () {
	
	//initializing a object of the class
	book Book;
	//using setter methods to give values to the leftover attributes
	Book.set_name("Harry-potter");
	Book.set_author("JK-rowling");
	Book.set_isbn("123456789");
	
	//attempted to read 4 pages
	Book.read();
	Book.read();
	Book.read();
	Book.read();
	//calling functon to show information about the book
	Book.showBookInfo();
	
	
	
}
Q3
#include <iostream>
#include <string>

using namespace std;

class weekDays {
private:
    string days[7] = {"Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"};
    int currentDay;

public:
    // Default constructor
    weekDays() {
        currentDay = 0; //starting current day is sunday
    }

    // Parameterized constructor
    weekDays(int acurrentday) {
        if (acurrentday > 6) {
            currentDay = acurrentday % 7;
        } else {
            currentDay = acurrentday;
        }
    }

    string getCurrentDay() {
        return days[currentDay];
    }

    string getNextDay() {
        return days[(currentDay + 1) % 7]; // Ensure index remains within bounds
    }

    string getPreviousDay() {
        return days[(currentDay + 6) % 7]; 
    }

    string getNthDayFromToday(int n) {
        return days[(currentDay + n) % 7];
    }
};

int main() {
    int n;
    weekDays week;

    cout << "Current Day: " << week.getCurrentDay() << endl;
    cout << "Next Day: " << week.getNextDay() << endl;
    cout << "Previous Day: " << week.getPreviousDay() << endl;
    cout << "Enter the value of n to find the Nth day from today: " << endl;
    cin >> n;
    cout << "Nth Day from Today: " << week.getNthDayFromToday(n) << endl;

    return 0;
}
Q4
#include<iostream>
#include<string>

using namespace std;

class office {
private:
    string location;
    int seatingCapacity;
    string furniture[3];

public:
    // Parameterized constructor with default values
    office(string loc = "", int capacity = 0, string furn1 = "", string furn2 = "", string furn3 = "") :
        location(loc), seatingCapacity(capacity), furniture{furn1, furn2, furn3} {}

    // Function to display office information
    void displayInfo() {
        cout<<"Location: "<<location<<endl;
        cout<<"Seating Capacity: "<<seatingCapacity<<endl;
        cout<<"Furniture: ";
        for(int i=0;i<3;i++) {
            cout<<furniture[i];
            if(i!=2)cout<<", ";
        }
        cout<<endl;
    }
};

int main() {
    office office1; // no arguments given
    office office2("Building A"); // One argument gave
    office office3("Building B", 50); // Two arguments passed
    office office4("Building C", 100, "table", "kursi", "pc"); // Three arguments pass

    // Displaying all the office information
    cout<<"Office 1 Info:"<<endl;
    office1.displayInfo();
    cout<<endl;

    cout<<"Office 2 Info:"<<endl;
    office2.displayInfo();
    cout<<endl;

    cout<<"Office 3 Info: "<<endl;
    office3.displayInfo();
    cout<<endl;

    cout<<"Office 4 Info:"<<endl;
    office4.displayInfo();
    cout << endl;

    return 0;
}
#include<iostream>
#include<string>

using namespace std;

class office {
private:
    string location;
    int seatingCapacity;
    //pointer to array furiture that wil store all the furniture in the office
    string* furniture;

public:
    // Parameterized constructor with default values and dynamic memory allocation for furniture array
    office(string loc = "", int capacity = 0, int furniturenum=3) :
        location(loc), seatingCapacity(capacity) {
        	furniture= new string[furniturenum]; 
		}
    
    //destructor to de-alocate memory for furniture array
    ~office() {
        delete[] furniture;
    }
    
    //function to set furniture in the array at the next available location
    void set_furniture(int index, const string& item/*address of an item of the array furniture is being given1*/) {
    	furniture[index]=item;
	}
    
    // Function to display office information
    void displayInfo() {
        cout<<"Location: "<<location<<endl;
        cout<<"Seating Capacity: "<<seatingCapacity<<endl;
        cout<<"Furniture: ";
        for(int i=0;i<3;i++) {
            cout<<furniture[i]<<", ";
            
        }
        cout<<endl;
    }
};

int main() {
	
	//initializing a pointer of type office to store the object of the class and giing it inital values of some data members
	office* Officeptr = new office ("clifton",100,3);
	
	//giving values to the 
	Officeptr->set_furniture(0,"table");
	Officeptr->set_furniture(1,"kursi");
	Officeptr->set_furniture(2,"PC"); 
	

    // Displaying the office information
    cout<<"Office Info:"<<endl;
    Officeptr->displayInfo();
    cout<<endl;
    
    //clearing the dynamically allocated memory
    delete Officeptr;

    
    return 0;
}
