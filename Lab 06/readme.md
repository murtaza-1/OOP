Q1
#include<iostream>
#include<cstring>

using namespace std;

class BankAccount {
    private:
        int accountId;
        double balance;
        int* transactionHistory;
        int numTransactions;

    public:
        //parameterized constructor
        BankAccount(int id, double bal, int* transhist, int transnum) {
            accountId=id;
            balance=bal;
            numTransactions=transnum;
            //DMA for the array to store the transacton history
            transactionHistory = new int[numTransactions];
            //copying memory for allocation
            memcpy(transactionHistory, transhist, numTransactions * sizeof(int));
        }

        //copy constructor with initializer list
        BankAccount(const BankAccount& other/*copying one bankaccount object to another*/) : accountId(other.accountId), balance(other.balance), numTransactions(other.numTransactions) {
            //allocate memory for transaction history and copy transactions
            transactionHistory = new int[numTransactions];
            memcpy(transactionHistory, other.transactionHistory, numTransactions * sizeof(int));
        }

        //destructor
        ~BankAccount() {
            delete[] transactionHistory;
        }
       
        //display function for information
        void display() {
            cout<<"Account ID: "<<accountId<<endl;
            cout << "Balance: " <<balance<<endl;
            cout << "Transaction History: ";
            for (int i = 0; i<numTransactions;i++){
                cout<<transactionHistory[i]<<" ";
            }
            cout<<endl;
        }
        
		//function to add trasaction data to the tansaction history array
        void updateTransactionHistory(int* transactions, int numTrans) {
            //deallocate existing transaction history
            delete[] transactionHistory;
       
           //allocate memory for new transaction history and copy transactions
           numTransactions = numTrans;
           transactionHistory = new int[numTransactions];
           memcpy(transactionHistory, transactions, numTransactions * sizeof(int));
        }
};

int main() {
    cout<<"Murtaza jafri\n23k-0076\n"<<endl;
	int transactions1[] = {600, -500, 700}; //sample transaction history
    //to find number of data elements in the array (size of whole array / size of one data item in the array)
	int numTrans1 = sizeof(transactions1) / sizeof(transactions1[0]);

    //sample bank account
    BankAccount account1(033222, 1000.0, transactions1, numTrans1);

    //creating a copy of the original account
    BankAccount account2 = account1;

    //displaying the account details of both the original and copied accounts
    cout<<"Original Account:"<<endl;
    account1.display();
    cout<<endl;

    cout<<"Copied Account:"<<endl;
    account2.display();
    cout<<endl;

    //chage the transaction history of the original account
    int newTrans[] = {-200, 300};
    //finding num of data items in the array
    int numNewTrans = sizeof(newTrans) / sizeof(newTrans[0]);
    account1.updateTransactionHistory(newTrans, numNewTrans);

    //showing the details of the original account after updating t#include <iostream>
    q2
    
#include <cstdlib> //library for rand function
#include <ctime> //library for time function from the system

using namespace std;

class image {
    private:
        int width;
        int height;
        int* image_data;

    public:
        //parameterized constructor
        image(int awidth, int aheight, const int* imgData) : width(awidth), height(aheight) {
            //DMA for a array to store pixel data 
			image_data = new int[width * height];
			//populating the array with pixel data
            for (int i = 0; i < width * height; i++) {
                image_data[i] = imgData[i];
            }
        }

        //copy constructor
        image(const image& other/*passing another object as argument*/) : width(other.width), height(other.height) {
            image_data = new int[width * height];
            for (int i = 0; i < width * height; i++) {
                image_data[i] = other.image_data[i];
            }
        }

        //destructor
        ~image() {
            delete[] image_data;
        }

        //display function
        void display() const {
            cout<<"image Data:\n";
            //diplaying image pixel data
		    for (int i=0;i<height;i++) {
                for (int j=0;j<width; j++) {
                    cout<<image_data[i * width + j] << " ";
                }
                cout<<endl;
            }
            cout<<endl;
        }

        //add pixel data in places where pixel value is less then or equal to zero with random values between 1 and 255
        void updateData() {
        	//this function will generate random numbers to populate the array with DIFFERENT numbers each time the program is run based on the time as the seed of the function
            srand(time(NULL));
            for (int i = 0; i < width * height;i++) {
                if (image_data[i] <= 0) {
                	//makes sure random value is between 1 and 255
                    image_data[i]=rand() % 255 + 1;
                }
            }
        }
};

int main() {
	cout<<"Murtaza jafri\n23k-0076\n\n"<<endl;
	
    //sample image data
    int imgdata[6] = {1, -2, 3, -4, 5, 6};

    //create original image
    image original(2, 3, imgdata);

    //create a copy of the original image
    image copy(original);

    //show the original and copied images
    cout<<"Original image:\n";
    original.display();

    cout<<"Copied image:\n";
    copy.display();

    //alter data and display again
    original.updateData();
    copy.updateData();

    cout << "after updating data:\n";
    cout << "Original Image:\n";
    original.display();

    cout << "copied Image:\n";
    copy.display();

    return 0;
}ransaction history
    cout<<"original Account after changing transaction history:"<<endl;
    account1.display();
    cout<<endl;

    return 0;
}
#include <iostream>

using namespace std;

class appointment {
    private:
        string Name;
        double cost;
        static int totalAppointments;
        static double totalEarnings;

    public:
    	//parameterized constructor
        appointment(const string& name, double acost) : Name(name), cost(acost) {
            totalAppointments++;
            totalEarnings += cost;
        }
        
        //static function to calculate average cost of each appointment
        static double averageCost() {
            //returns 0 if no appointments have been made to avoid division by zero error
			if (totalAppointments == 0) {
                return 0; 
            }
            //calculating average
            return totalEarnings/totalAppointments;
        }
        
        //getter functions
        string getName() const {
            return Name;
        }

        double getCost() const {
            return cost;
        }
        
        void displayAppointment() const {
            cout<<"Customer Name: "<<Name<<"\nAppointment Cost: $" <<cost<<endl;
            cout<<endl;
        }
};

//Initializing static data members
int appointment::totalAppointments = 0;
double appointment::totalEarnings = 0;

int main() {
	cout<<"murtaza jafri\n23k-0076\n\n"<<endl;
	
    //creating appointments with different details
    appointment appointment1("murtaza", 89.0);
    appointment appointment2("zia", 46.0);
    appointment appointment3("Akil", 64.0);
    appointment appointment4("hamza", 36.0);
    
    //displaying all the customer data
    appointment1.displayAppointment();
    appointment2.displayAppointment();
    appointment3.displayAppointment();
    appointment4.displayAppointment();

    //Calculate and display average cost per appointment
    cout<<"average cost per appointment: $" <<appointment::averageCost()<<endl;

    return 0;
}
q4
#include <iostream>

using namespace std;

//inline function to calculate batting average
inline double calcBattingAvg(int runs, int dismissals) {
    if (dismissals == 0) {
    	//to remove division by zero error
        return 0; 
    }
    //typecasts integer values to double for finding the answer in double
    return static_cast<double>(runs) / dismissals;
}

//inline function to calculate strike rate
inline double calcStrikeRate(int runs, int balls) {
    if (balls == 0) {
    	//removing division by zero error
        return 0; 
    }
    return static_cast<double>(runs) / balls * 100;
}

int main() {
	cout<<"Murtaza jafri\n23k-0076\n\n"<<endl;
	
    int Runs, Dismissals, Balls;

    cout<<"Enter total runs scored: ";
    cin>>Runs;
    cout<<"Enter total payer dismissals ";
    cin>> Dismissals;
    cout<<"Enter num of balls faced: ";
    cin>>Balls;

    double battingAverage = calcBattingAvg(Runs, Dismissals);
    cout<<"Batting Average: "<<battingAverage<<endl;


    double strikeRate = calcStrikeRate(Runs, Dismissals);
    cout<<"Strike Rate: "<<strikeRate<<endl;

    return 0;
}
q5
#include <iostream>
#include <string>

using namespace std;

class Course {
    private:
        string courseCode;
        string courseName;
        int creditHours;

    public:
    	//default constructor
    	Course() {
    		courseCode="";
    		courseName="";
    		creditHours=0;
		}
		
    	//parameterized constructor with initializer list
        Course(string acode, string aname, int hours) : courseCode(acode), courseName(aname), creditHours(hours) {}

        //getter methods
        string getCourseCode() const {
            return courseCode;
        }

        string getCourseName() const {
            return courseName;
        }

        int getCreditHours() const {
            return creditHours;
        }
};

class Student {
    private:
        string studentID;
        string studentName;
        //array of data type courses to store all courses the student is enrolled in
        Course* enrolledCourses;
        int numCourses;

    public:
        //parameterized constructor
        Student(string id, string name, Course* courses, int count) : studentID(id), studentName(name), enrolledCourses(courses), numCourses(count) {}

       void enroll(const Course& course) {
    // Allocate memory for the new array
    Course* temp = new Course[numCourses + 1];
    // Copy existing courses to the new array
    for (int i = 0; i < numCourses; i++) {
        temp[i] = enrolledCourses[i];
    }
    // Add the new course
    temp[numCourses] = course;
    // Delete the old array and save the new array
    delete[] enrolledCourses;
    enrolledCourses = temp;
    // Increment the course count
    numCourses++;
}

void drop(const Course& course) {
    // Search for the course in the array
    int index = -1;
    for (int i = 0; i < numCourses; i++) {
        // Finding index of desired course based on course code
        if (enrolledCourses[i].getCourseCode() == course.getCourseCode()) {
            index = i;
            break;
        }
    }
    
    // If required course code is found
    if (index != -1) {
        // Create a new array with one less element
        Course* temp = new Course[numCourses - 1];
        // Copy elements before the dropped course
        for (int i = 0; i < index; i++) {
            temp[i] = enrolledCourses[i];
        }
        // Copy elements after the dropped course
        for (int i = index + 1; i < numCourses; ++i) {
            temp[i - 1] = enrolledCourses[i];
        }
        // Remove the old array and assign the new array
        delete[] enrolledCourses;
        enrolledCourses = temp;
        // Reduce the course count by 1
        numCourses--;
    }
}


    //getter method to get total credit hours
    int getTotalCreditHours() const {
        int totalCreditHours = 0;
        for (int i = 0; i < numCourses;i++) {
            totalCreditHours += enrolledCourses[i].getCreditHours();
        }
        return totalCreditHours;
    }

    //display function to print enrolled courses
    void displayEnrolledCourses() const {
        cout<<"Enrolled Courses for Student "<<studentID<<" - "<<studentName<<":\n";
        for (int i = 0; i < numCourses; i++) {
            cout<<"Course Code: "<<enrolledCourses[i].getCourseCode()<<endl;
			cout<<"Course Name: "<<enrolledCourses[i].getCourseName()<<endl;
            cout<<"Credit Hours: "<< enrolledCourses[i].getCreditHours()<<endl;
        }
    }

    // Destructor to deallocate memory
    ~Student() {
        delete[] enrolledCourses;
    }
};

int main() {
	cout<<"Murtaza\n23k-0076\n\n"<<endl;
	
    Course course1("OOP101", "Object-oriented-programming", 3);
    Course course2("MATH345", "Multivariable Calculus", 4);
    Course course3("PHY851", "applied physics", 3);
    Course course4("ENG101", "English Composition", 3);
    Course course5("BIO201", "Biology", 4);

    //array of all the courses 
    Course courses[] = {course1, course2, course3};

    //Create a student and enroll in courses
    Student student("23k-001", "Ahmed", courses, 3);

    // Print enrolled courses
    student.displayEnrolledCourses();
    
    //enrolling in a course
    student.enroll(course5);
    //dropping a course
    student.drop(course4);

    //Print enrolled courses after dropping a course and enrolling in a course
    cout << "\nAfter changing courses:\n";
    student.displayEnrolledCourses();

    //find total credit hours
    cout<<"\nTotal Credit Hours: "<<student.getTotalCreditHours()<<endl;

    return 0;
}
