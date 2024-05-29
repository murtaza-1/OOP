lab 02 Q1

#include<iostream>

//using the standard namespace
using namespace std;

//defining the recursive function
void recursiveSwap(int& x, int& y/*pointers passed as arguments so any alteration to the variables is done directly*/) {
	//if values are same so no swap required
	if(x==y) {
		cout<<"no swap required"<<endl;
	} else {
		int temp = x;
        x = y;
        y = temp;
//        recursiveSwap(x, y);
	}
}

int main() {
	int a,b;
	cout<<"enter the value of the first variable: "<<endl;
	cin>>a;
	cout<<"enter the value of the second variable"<<endl;
    cin>>b;
    cout<<"the values before the swap are a="<<a<<" and b="<<b<<endl;
    recursiveSwap(a,b);
    cout<<"the values after the swap are a="<<a<<" and b="<<b<<endl;
    return 0;
}

Q2
#include <iostream>
#include <string> //header file for string
#include <unistd.h> // header file for sleep function used in the code to pause the program
#include <cstdlib>  // header file for the system() function that we will use to clear the command console

using namespace std;

//a strucutre that defines a book data type
struct book {
    string title;
    string author;
    int publicationyr;
    string genre;
};


int main() {
    int choice, numBooks = 0/*variable that will hold the number of books present in the database*/;

    cout << "\n\n\n\n\t\t\t\t      welcome to the book management system" << endl;
    book books[100];//array of the structure books to hold all the data

    while (true) {
    	//custom menu to show the user all the options and functionalities of the prgram
        cout << "\n\n\t\t\t\t********choose from the following options:*******\n\n" << endl;
        cout << "\t\t\t\t|-----------------------------------------------|" << endl;
        cout << "\t\t\t\t|-----------------------------------------------|" << endl;
        cout << "\t\t\t\t|    1)find a book from the database            |" << endl;
        cout << "\t\t\t\t|    2)add a book to the database               |" << endl;
        cout << "\t\t\t\t|    3)update data of a existing book record    |" << endl;
        cout << "\t\t\t\t|    4)exit                                     |" << endl;
        cout << "\t\t\t\t|-----------------------------------------------|" << endl;
        cout << "\t\t\t\t|-----------------------------------------------|" << endl;
        cout << "enter your choice:" << endl;
        cin >> choice;
        
        //main switch statement that will execute program based on user choice
        switch (choice) {
            //code for updating a already present book record
			case 3: {
                string search2;
                cout << "enter the title of the book that you want to update" << endl;
                cin.ignore();//clearing the input buffer
                getline(cin, search2); //getline() used for string inpt
                  
                for (int i = 0; i < numBooks; i++) {
                    if (books[i].title == search2) {
                        cout << "book found enter new data" << endl;
                        cout << "add new author" << endl;
                        getline(cin, books[i].author);
                        cout << "add new year of publication" << endl;
                        cin >> books[i].publicationyr;
                        cout << "add new genre" << endl;
                        cin.ignore();//clearing the buffer
                        getline(cin, books[i].genre);
                        break;
                    }
                }
                break;
            }
            
            //code for entering new book data in the array
            case 2: {
                cout << "enter data for book " << endl;
                cout << "enter the title:" << endl;
                cin.ignore();//clearing buffer
                getline(cin, books[numBooks].title);
                cout << "enter the author name:" << endl;
                getline(cin, books[numBooks].author);
                cout << "enter the year of publication:" << endl;
                cin >> books[numBooks].publicationyr;
                cout << "enter the genre:" << endl;
                cin.ignore();
                getline(cin, books[numBooks].genre);
                numBooks++; // Increment the number of books after adding a new book
                cout << "Book added successfully!" << endl;
                break;
            }
            
            //code for searching for a book based on title or author
            case 1: {
                int choice2;
                string search;
                while (true) {
                    cout << "will you be searching with the title or author choose from below:" << endl;
                    cout << "1)search by title" << endl;
                    cout << "2)search by author" << endl;
                    cout << "enter your choice:" << endl;
                    cin >> choice2;

                    cout << "enter search value" << endl;
                    cin.ignore(); //cearing the input buffer
                    getline(cin, search);
                    
                    //switch statement that will search based on title or author whatever the user wants
                    switch (choice2) {
                        case 1:
                            for (int i = 0; i < numBooks; i++) {
                                if (books[i].title == search) {
                                    cout << "book found" << endl;
                                    cout << "the title of the book is:" << endl;
                                    cout << books[i].title << endl;
                                    cout << "the author of the book is:" << endl;
                                    cout << books[i].author << endl;
                                    cout << "the year of publication is:" << endl;
                                    cout << books[i].publicationyr << endl;
                                    cout << "the genre of the book is:" << endl;
                                    cout << books[i].genre << endl;
                                    break;
                                }
                            }
                            cout << "no relevant book record found" << endl;
                            break;

                        case 2:
                            for (int i = 0; i < numBooks; i++) {
                                if (books[i].author == search) {
                                    cout << "book found" << endl;
                                    cout << "the title of the book is:" << endl;
                                    cout << books[i].title << endl;
                                    cout << "the author of the book is:" << endl;
                                    cout << books[i].author << endl;
                                    cout << "the year of publication is:" << endl;
                                    cout << books[i].publicationyr << endl;
                                    cout << "the genre of the book is:" << endl;
                                    cout << books[i].genre << endl;
                                    break;
                                }
                            }
                            break;

                        default:
                            cout << "wrong choice enter again" << endl;
                            continue;
                    }
                    break;
                }
                break;
            }
            
            //code to exit the program when the user wants
            case 4:
                cout << "thank you use us again soon:)" << endl;
                exit(0); //exit function

            default:
                cout << "wrong choice, the program will pause for a few seconds then try again" << endl;
                sleep(3); //function to pause the program for 3 secods
                system("cls");//function to clear the command console
                continue; //keyword to continue to next iteration of the loop
        }
    }

    return 0;
}
Q3
#include<iostream>

using namespace std;

bool hasSubsetSum(int arr[], int size, int targetSum) {
	
	if (targetSum == 0) {
        return true;  // Subset with sum 0 always exists (empty subset)
    }
    
    if (size == 0) {
        return false;  // No numbers left to check
    }

    // If the last element is greater than the target sum, it wont be included in the subset as 2 numbers are needed
    if (arr[size - 1] /*last element index*/> targetSum) {
        //recursive case
		return hasSubsetSum(arr, size - 1, targetSum);
    }

    // if neither of the above conditions are true then the recursive condition checks if either including the last element or excluding it gives the target sum
    return hasSubsetSum(arr, size - 1, targetSum) || hasSubsetSum(arr, size - 1, targetSum - arr[size - 1]);
}



int main() {
	int n,target,i;
	cout<<"enter the size of the integer array"<<endl;
	cin>>n;
	int numeric[n];
	
	cout<<"enter the target sum"<<endl;
	cin>>target;
	
	for(i=0;i<n;i++) {
		cout<<"enter value "<<i+1<<endl;
		cin>>numeric[i];
	}
	
	if (hasSubsetSum(numeric, n, target) ) {
        cout << "Subset with sum " << target << " exists." << endl;
    } else {
        cout << "subset with sum " << target << " does NOT exists." << endl;
    }
	
	return 0;
}
Q4
#include <iostream>
#include <string>//getline fuction wont have to be used for string input by using this header file
using namespace std;

// Define structure for Register
struct Register {
    int courseId;
    string courseName;
};

// Define structure for Student, which will inherit the properties of Register
struct Student : public Register {
    int studentId;
    string firstName;
    string lastName;
    string cellNo;
    string email;
};

int main() {
    // Create an array of structures to store data for 5 students
    Student students[5];

    // Taking data for each student
    for (int i = 0; i < 5; i++) {
        cout<<"Enter details for student "<<i + 1<<":"<< endl;
        cout<<"Course ID: ";
        cin>>students[i].courseId;
        cout<< "Course Name: ";
        cin.ignore(); //clearing input buffer
        getline(cin, students[i].courseName);
        cout<< "Student ID: ";
        cin>> students[i].studentId;
        cout<< "First Name: ";
        cin>> students[i].firstName;
        cout<< "Last Name: ";
        cin>> students[i].lastName;
        cout<< "Cell No: ";
        cin>> students[i].cellNo;
        cout<< "Email: ";
        cin>> students[i].email;
    }

    // Display the info for all 5 students
    cout << "\nStudent Information:" << endl;
    for (int i = 0; i < 5; ++i) {
        cout << "Student " << i + 1 << ":\n";
        cout << "Course ID: " << students[i].courseId << endl;
        cout << "Course Name: " << students[i].courseName << endl;
        cout << "Student ID: " << students[i].studentId << endl;
        cout << "First Name: " << students[i].firstName << endl;
        cout << "Last Name: " << students[i].lastName << endl;
        cout << "Cell No: " << students[i].cellNo << endl;
        cout << "Email: " << students[i].email << endl;
        cout << endl;
    }

    return 0;
}
Q5
#include<iostream>
#include<unistd.h>//header added for sleep() function to pause program

using namespace std;

//global variable to hold the number of items in the main database array
int position=0;

//structure template for each product
struct product{
	int productid;
	string name;
	float price;
	int quantity;
};

//global array of structures as it has to be used outside the main function
product products[100];

//function to add new product records to the array
void addProduct(product products[],int &position) {
	cout<<"add the details of the product you want to add to the database"<<endl;
	cout<<"enter the product ID:"<<endl;
	cin>>products[position].productid;
	cout<<"enter the product name"<<endl;
	cin.ignore();//clearing the input bffer
	getline(cin,products[position].name);
	cout<<"enter the product price"<<endl;
	cin>>products[position].price;
	cout<<"enter the product quantity"<<endl;
	cin>>products[position].quantity;
	cout<<"\nproduct added successfully!"<<endl;
	position++;//incrementing the global variable telling the number of items in the array so next time the next location in the array is used to store the next data
}

//function to find a product from the array
void findProduct(product products[],int productid) {
	for(int i=0;i<position;i++) {
		if(products[i].productid==productid) {
			cout<<"product found"<<endl;
			cout<<"product id is:"<<endl;
			cout<<products[i].productid<<endl;
			cout<<"product name is:"<<endl;
			cout<<products[i].name<<endl;
			cout<<"product price is:"<<endl;
			cout<<products[i].price<<endl;
			cout<<"product quantity is:"<<endl;
			cout<<products[i].quantity<<endl;
		}
	}
	cout<<"no such product found"<<endl;
}

//function to update existing record
void updaterecord(product products[],int productid) {
	for(int i=0;i<position;i++) {
		if(products[i].productid==productid) {
			cout<<"add new product name:"<<endl;
			cin.ignore();//clearing buffer
			getline(cin,products[i].name);
			cout<<"add new product price:"<<endl;
			cin>>products[i].price;
			cout<<"add new product quantity:"<<endl;
			cin>>products[i].quantity;
			cout<<"record updated successfully!"<<endl;
		}
	}
}


int main() {
	int choice;
	//label used to bring back program execution here when required
	again:
	cout<<"\t\t\t\t   welcome to the product management system";
	cout << "\n\n\t\t\t\t********choose from the following options:*******\n\n" << endl;
    cout << "\t\t\t\t|-----------------------------------------------|" << endl;
    cout << "\t\t\t\t|-----------------------------------------------|" << endl;
    cout << "\t\t\t\t|    1)add a product to the database            |" << endl;
    cout << "\t\t\t\t|    2)find a product from the database         |" << endl;
    cout << "\t\t\t\t|    3)update a existing record                 |" << endl;
    cout << "\t\t\t\t|    4)exit                                     |" << endl;
    cout << "\t\t\t\t|-----------------------------------------------|" << endl;
    cout << "\t\t\t\t|-----------------------------------------------|" << endl;
    cout << "enter your choice:" << endl;
    cin >> choice;
    
    //calling the respective functions based on user choice
    switch (choice) {
    	case 1:
    		addProduct(products,position);
    		break;
    		
    	case 2:
    		int productid;
    		cout<<"enter the id of the product you want to find"<<endl;
    		cin>>productid;
    		findProduct(products,productid);
    		break;
    		
    	case 3:
    		int productid2;
    		cout<<"enter the id of the product you want to find"<<endl;
    		cin>>productid2;
    		updaterecord(products,productid2);
    		break;
    		
    	case 4:
    		cout<<"thank you for coming use us again:)"<<endl;
    		exit(0);//function to exit the program
    		break;
    		
        default:
        	cout<<"wrong input program loading again choose again"<<endl;
        	sleep(2);//function to pause the program for required seconds
        	break;
	}
	//goto statement will take program execution to where the mentioned label is
	goto again;
	
}
Q6
#include <iostream>

using namespace std;

//Euclidean algorithm used to find GCD or HCF
int calculateGCD(int a, int b) {
    if (b == 0) {
        return a;//basecase
    } else {
    	//according to the algorithm each consecutive calls will see the value of a being replaced by b and b getting the remainder of a/b
        return calculateGCD(b, a % b);//recursive case
    }
}

// LCM calculation using a simple formula which includes the gcd euclidean algorthm as well. so basecase of the above function will be the basecase of this function as well
int calculateLCM(int a, int b) {
    return (a * b) / calculateGCD(a, b);
}

int main() {
    int num1, num2;

    cout<<"Enter the first number: ";
    cin>>num1;
    cout<<"Enter the second number: ";
    cin>>num2;

    cout<<"GCD of "<<num1<<" and "<<num2<<" is: "<<calculateGCD(num1, num2)<<endl;

    cout<<"LCM of "<<num1<<" and "<<num2<<" is: "<<calculateLCM(num1, num2)<<endl;

    return 0;
}
