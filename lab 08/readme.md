q1
#include <iostream>
#include <string>

using namespace std;

//base class 
class Book {
	protected:
    	string title;
    	string author;
    	string publisher;

	public:
    	//parameterized constructor with initializer list
    Book(string atitle, string aauthor, string apublisher)
        : title(atitle), author(aauthor), publisher(apublisher) {}

    //display function
    void display() const {
    	cout<<"information about the book"<<endl;
        cout<<"Title: "<<title<<endl;
        cout<<"Author: "<<author << endl;
        cout<<"Publisher: "<<publisher<<endl;
    }
};

//derived or subclass 
class FictionBook : public Book {
	private:
    	string genre;
    	string protagonist;

	public:
    	//parameterized constructor with initializer list for inheritance
    	FictionBook(string atitle, string aauthor, string apublisher, string agenre, string aprotagonist)
        : Book(atitle, aauthor, apublisher), genre(agenre), protagonist(aprotagonist) {}

    //second implemenyain of display function (function overriding)
    void display() const {
        //get existing implementation of the display
        Book::display();
        //define additional implementation
        cout<<"Genre: "<<genre<<endl;
        cout<<"Protagonist: "<<protagonist<<endl;
    }
};

int main() {
	cout<<"Murtaza jafri\n23k-0076"<<endl;
    //instance of the derived class
    FictionBook book("it ends with us", "Collen Hoover", "oxford", "Romantic-Fiction", "lily Bloom");
    book.display();

    return 0;
}
q2
#include <iostream>
#include <string>

using namespace std;

//Base class 
class Character {
	protected:
    	int health;
    	int damage;

	public:
    	// Constructor with intializer list
    	Character(int ahealth, int adamage) : health(ahealth), damage(adamage) {}

    //display function
    void display() const {
        cout<<"Health: "<<health<<endl;
        cout<<"Damage: "<<damage<<endl;
    }
};

//sub-class 1
class Enemy : public Character {
	public:
    	//constructor with initializer list
    	Enemy(int ahealth, int adamage) : Character(ahealth, adamage) {}

    //function overloading
    void display() const {
        //calling existing implementatiom
        Character::display();
        //adding extra implementation
        cout<<"Type: Enemy"<<endl;
    }
};

//sub-class 2
class Player : public Character {
	public:
    	//constructor with initializer list
    	Player(int ahealth, int adamage) : Character(ahealth, adamage) {}

    	//function overriding
    	void display() const {
        	Character::display();
        	//extra implementation
        	cout<<"Type: Player"<<endl;
    	}
};

//sub class of player
class Wizard : public Player {
	private:
    	int magicPower;
    	string spells;

	public:
    	//constructor with intializer list
    	Wizard(int ahealth, int adamage, int amagicPower, string aspells) : Player(ahealth, adamage), magicPower(amagicPower), spells(aspells) {}

    
    	void display() const {
        	Player::display();
        	cout<< "Magic Power: "<<magicPower<<endl;
        	cout<<"Spells: "<<spells<<endl;
    	}
};

int main() {
	cout<<"Murtaza\n23k-0076\n"<<endl;
    //instance of an object of Wizard class
    Wizard wizard(100, 20, 50, "lightning strike, healing spell;");

    //display details of the wizard
    cout<<"Wizard Details:"<<endl;
    wizard.display();

    return 0;
}
#include <iostream>

using namespace std;

//base-class 1
class Position {
	protected:
    	double x;
    	double y;
    	double z;

	public:
    	//constructor with initializer list
    	Position(double ax, double ay, double az) : x(ax), y(ay), z(az) {}

    	//function to display position
    	void displayPosition() const {
        	cout<<"Position: ("<<x<<", "<<y<<", "<<z<<")"<<endl;
    	}
};

//base-class 2
class Health {
	protected:
    	int health;

	public:
    	Health(int ahealth) : health(ahealth) {}

    //utility to display health
    void displayHealth() const {
        cout<<"Health: "<<health<< endl;
    }
};

//derived class with mulitple inheritance
class Character : public Position, public Health {
	private:
    	string name;
    	int level;

	public:
    //constructor with initializer list
    Character(double ax, double ay, double az, int ahealth,string aname, int alevel) : Position(ax, ay, az), Health(ahealth), name(aname), level(alevel) {}

    //utility to display character deets
    void displayCharacter() const {
        cout<<"Character Name: "<<name<<endl;
        cout<<"Character Level: "<<level<<endl;
        //display functions from both inherited classes
		displayPosition(); 
        displayHealth();   
    }
};

int main() {
	cout<<"Murtazas\n23k-0076\n"<<endl;
	
    //instace of a Character object
    Character player(9.9, 10.7, 4.5, 100, "Player1", 1);
    player.displayCharacter();

    return 0;
}
q4
#include <iostream>
#include <string>

using namespace std;

//base class
class Person {
	protected:
    	string name;
    	int age;

	public:
    	//constructor with initializer list
    	Person(string aname, int aage) : name(aname), age(aage) {}

    	void display() const {
        	cout<<"Name: "<<name<<endl;
			cout<<"Age: "<<age<<endl;;
    	}
};

//derived class 1
class Student : public Person {
	protected:
    	string studentID;
    	int gradeLevel;

	public:
    	//constructor with intializer list
    	Student(string& aname, int aage, string astudentID, int agradeLevel) : Person(aname, aage), studentID(astudentID), gradeLevel(agradeLevel) {}


    	void display() const {
    		//existing implementation called
        	Person::display(); 
        	//extra implementation
        	cout <<"Student ID: "<<studentID<<endl;
			cout<<"Grade Level: "<<gradeLevel<<endl;
    	}
};

//derived class 2
class Teacher : public Person {
	protected:
    	string subject;
    	int roomNumber;

	public:
    	Teacher(string aname, int aage, string asubject, int aroomNumber) : Person(aname, aage), subject(asubject), roomNumber(aroomNumber) {}

    	//function to display 
    	void display() const {
        	Person::display(); // Call base class display function
        	cout<<"Subject: "<<subject<<endl;
			cout<<"Room Number: "<<roomNumber<<endl;
        }
};

//derived class with multiple inheritance
class GraduateStudent : public Student, public Teacher {
	public:
		//constructor with initializer list
    	GraduateStudent( string aname, int aage, string astudentID, int agradeLevel, string asubject, int aroomNumber)
        : Student(aname, aage, astudentID, agradeLevel), Teacher(aname, aage, asubject, aroomNumber) {}

    
    	void display() const {
        	Student::display(); // Call display function of Student class
        	cout<<"Teaching Subject: "<<subject<<endl;
			cout<<"Teaching Room Number: "<<roomNumber<<endl;
        }
};

int main() {
    //instance an object 
    GraduateStudent gradStudent("Murtaza", 20, "12345", 12, "Computer Science", 101);

    // Display details of the graduate student
    cout << "Details of Graduate Student:" <<endl;
    gradStudent.display();

    return 0;
}
#include <iostream>
#include <string>

using namespace std;

//base class 
class Vehicle {
	protected:
    	string make;
    	string model;
    	int year;

	public:
    	//constructor to initialize member variables
    	Vehicle( string amake, string amodel, int ayear) : make(amake), model(amodel), year(ayear) {}

    	//function to display 
    	void display() const {
        	cout<<"Make: "<<make<<endl;
			cout<<"Model: "<<model<<endl;
			cout<<"Year: "<<year<<endl;
    	}
};

// Derived class 1
class Car : public Vehicle {
	protected:
    	int numDoors;
    	double fuelEfficiency;

	public:
    	//xonstructor to initialize base class and derived class member variables
    	Car(string amake, string amodel, int ayear, int anumDoors, double afuelEfficiency) 
		: Vehicle(amake, amodel, ayear), numDoors(anumDoors), fuelEfficiency(afuelEfficiency) {}

    	//function to display
    	void display() const {
        	Vehicle::display(); //initial function implementation called
        	cout<<"Number of Doors: "<<numDoors<<endl;
			cout<<"Fuel Efficiency: "<<fuelEfficiency<<"mpg"<<endl;
    }
};

// Derived class 2
class ElectricCar : public Car {
	protected:
    	double batteryLife;

	public:
    	
    	ElectricCar(string amake, string amodel, int ayear, int anumDoors, double afuelEfficiency, double abatteryLife)
        : Car(amake, amodel, ayear, anumDoors, afuelEfficiency), batteryLife(abatteryLife) {}

    	void display() const {
        	Car::display(); 
        	cout << ", Battery Life: "<<batteryLife<<" kWh"<<endl;
    }
};

int main() {
		cout<<"Murtaza\n23k-0076\n"<<endl;
    ElectricCar electricCar("TESLA", "Model-Y", 2020, 4, 95.5, 100);

    //display details of the electric car
    cout << "Details of Electric Car:" <<endl;
    electricCar.display();

    return 0;
}
