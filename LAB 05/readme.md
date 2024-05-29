Q1
#include<iostream>

using namespace std;

class square {
	private:
		float sidelength;
		float area;
		//static variable to store sum of all areas of all squares
		static float allareas;
		
	public:
		square() {
			sidelength=0;
			area=0;
		}
		
		square(float sidelength) {
			this->sidelength=sidelength;
			area=0;
		}
		
		void calcarea() {
			area= sidelength * sidelength;
			allareas = allareas + area;
		}
		
		void setlength(int sidelength) {
			this->sidelength;
		}
		
		float getsidelength()const {
			return sidelength;
		} 
		
		float getarea()const {
			return area;
		}
		
		static float getallareas() {
			return allareas;
		}
		
};

float square::allareas=0;

int main() {
	square Square1(2.9); //create Square with side length 2.9
    Square1.calcarea();
    cout<<"area of square1: " <<Square1.getarea()<<endl;
    cout<<"All areas: " << square::getallareas() <<endl;

    square Square2(3.6); //create Square with side length 3.6
    Square2.calcarea();
    cout<<"\narea of square2: "<<Square2.getarea()<<endl;
    cout<<"All areas: "<<square::getallareas() <<endl;

    square Square3(4.4); //create Square with side length 4.4
    Square3.calcarea();
    cout<< "\narea of square3: " << Square3.getarea() <<endl;
    cout<< "all areas: " << square::getallareas() <<endl;

}
q2
#include<iostream>

using namespace std;

class Loanhelper{
	private:
	    const float rate;
	    float amount;
	    int timeMonths;
	
	public:
		//parameterized constructor with initializer list
		Loanhelper(float arate, float aamount, int atimeMonths) : rate(arate), amount(aamount), timeMonths(atimeMonths) {}
		
		void calculateMonthlyPayment() {
        //calculate monthly payment
        float monthlyPayment = amount / timeMonths;
        float monthlyInterest = monthlyPayment * rate;

        //adding interest to payments
        monthlyPayment = monthlyPayment+monthlyInterest;

        cout << "You have to pay " << monthlyPayment << " every month for " << timeMonths << " months to repay your loan" << endl;
        }
};

int main() {
	Loanhelper loan(0.07, 10000.0, 8);

    // Calculate and display monthly payment
    loan.calculateMonthlyPayment();
    return 0;
}
q4
#include <iostream>
#include <string>

class ValidateString {
    private:
        string str;

    public:
    	//parametrized constuctor with initializer list
        ValidateString(const string &s) : str(s) {}

       //a constant function to check the string.the function is made constant so that the value it gives doesnt change
        bool isValid() const {
            for(char c : str) {
            	//using ASCII values to check of entered data is alphabet or not
                if (!(c >= 'A' && c <= 'Z') && !(c >= 'a' && c <= 'z')) {
                    return false;
                }
            }
            return true;
        }
};

int main() {
    
	ValidateString str1("helloeveryone");
    ValidateString str2("9876");
    ValidateString str3("blahblah123");

    //checking if the strings are valid using ternary operators
    cout<<"String 1 is "<< (str1.isValid() ? "valid" : "invalid")<<endl;
    cout<<"String 2 is "<< (str2.isValid() ? "valid" : "invalid")<<endl;
    cout<<"String 3 is "<< (str3.isValid() ? "valid" : "invalid")<<endl;

    return 0;
}
#include<iostream>

using namespace std;

class BankAccount{
    public:
        int accountNumber;
        string accountHolderName;
        double balance;
   
    public:
        BankAccount(int accnum, string accname, int abalance) {
            accountNumber=accnum;
            accountHolderName=accname;
            balance=abalance;
        }

        void deposit(double amount) {
            balance=balance+amount;
        }

        int withdraw(double amount) {
            if(amount>balance){
                cout<<"insufficent amount"<<endl;
            } else {
                balance=balance-amount;
            }
        }

        void display() {
            cout<<"following are the account details"<<endl;
            cout<<"the account number is: "<<accountNumber<<endl;
            cout<<"the name of the account holder is: "<<accountHolderName<<endl;
            cout<<"the balance currently in the account is: "<<balance<<endl;
        }
};

int main() {
    //array of banckaccount objects
	BankAccount accounts[3]={
    BankAccount(1010, "asif ali Zardari", 0),
    BankAccount(1011, "Nawaz shareef", 2000), 
    BankAccount(1111, "imran khan", 3000)
    };

    cout<<"welcome to bank account management system"<<endl;

    for(int i = 0; i<3; i++) {
        accounts[i].display();
        cout<<"\n";
    }

    accounts[0].deposit(0);
    accounts[0].withdraw(200);

    cout<<"new account details are: "<<endl;
    accounts[0].display();

}
q3
#include <iostream>
#include <string>

class ValidateString {
    private:
        string str;

    public:
    	//parametrized constuctor with initializer list
        ValidateString(const string &s) : str(s) {}

       //a constant function to check the string.the function is made constant so that the value it gives doesnt change
        bool isValid() const {
            for(char c : str) {
            	//using ASCII values to check of entered data is alphabet or not
                if (!(c >= 'A' && c <= 'Z') && !(c >= 'a' && c <= 'z')) {
                    return false;
                }
            }
            return true;
        }
};

int main() {
    
	ValidateString str1("helloeveryone");
    ValidateString str2("9876");
    ValidateString str3("blahblah123");

    //checking if the strings are valid using ternary operators
    cout<<"String 1 is "<< (str1.isValid() ? "valid" : "invalid")<<endl;
    cout<<"String 2 is "<< (str2.isValid() ? "valid" : "invalid")<<endl;
    cout<<"String 3 is "<< (str3.isValid() ? "valid" : "invalid")<<endl;

    return 0;
}
q5
#include <iostream>
#include <string>

using namespace std;

class Engine {
private:
    string type;

public:
    Engine(const string& aType) : type(aType) {}

    void start() {
        cout<<"Engine of type " <<type<<" has started" << endl;
    }
};

class Wheel {
private:
    int size;

public:
    Wheel() {} //Default constructor 

    Wheel(int aSize) : size(aSize) {}

    void rotate() {
        cout << "Wheel of size " << size << " is rotating." << endl;
    }
};

class Headlight {
private:
    string company;

public:
    Headlight() {} 

    Headlight(const string& Brand) : company(Brand) {}

    void illuminate() {
        cout << "Headlight of brand " << company << " is working." << endl;
    }
};

class Steering {
private:
    string type;

public:
    Steering(const string& atype) : type(atype) {}

    void turn() {
        cout << "Steering of type " << type << " is turning" << endl;
    }
};

class Car {
private:
    Engine engine;
    Wheel* wheels;
    Headlight* headlights;
    Steering steering;

public:
    Car(const string& engineType, int wheelSize, const string& headlightBrand, const string& steeringType)
        : engine(engineType), steering(steeringType) {
        wheels = new Wheel[4];
        headlights = new Headlight[2];
        for (int i = 0; i < 4; ++i) {
            wheels[i] = Wheel(wheelSize);
        }
        for (int i = 0; i < 2; ++i) {
            headlights[i] = Headlight(headlightBrand);
        }
    }

    ~Car() {
        delete[] wheels;
        delete[] headlights;
    }

    void start() {
        engine.start();
    }

    void drive() {
        for (int i = 0; i < 4; ++i) {
            wheels[i].rotate();
        }
    }

    void turnOnLights() {
        for (int i = 0; i < 2; ++i) {
            headlights[i].illuminate();
        }
    }

    void turnSteering() {
        steering.turn();
    }
};

int main() {
    Car myCar("V6", 18, "hyundai", "power");
    myCar.start();
    myCar.drive();
    myCar.turnOnLights();
    myCar.turnSteering();
    return 0;
}
q6
#include <iostream>
#include <string>

using namespace std;

// Graphics Rendering Engine
class GraphicRenderEngine {
public:
    void render() {
        cout<<"Graphics engine is rendering graphics." << endl;
    }
};

class InputHandler {
public:
    void handleInput() {
        cout << "Input handler is processing user input." << endl;
    }
};

class PhysicsEngine {
public:
    void simulatePhysics() {
        cout << "Physics engine is simulating physics." << endl;
    }
};

class GameEngine {
//association being used
private:
    GraphicRenderEngine graphicsEngine;
    InputHandler inputHandler;
    PhysicsEngine physicsEngine;

public:
    void start() {
        cout << "the Graphics engine is starting." << endl;
        graphicsEngine.render();
        inputHandler.handleInput();
        physicsEngine.simulatePhysics();
        cout << "Game engine has started" << endl;
    }
};

int main() {
    GameEngine gameEngine;
    gameEngine.start();
    return 0;
}
q7
#include <iostream>
#include <string>

using namespace std;


class MenuItem {
private:
    string name;
    double price;

public:
	//default constructor
    MenuItem() : name(""), price(0.0) {}  
    
    MenuItem(const string& aName, double aPrice) : name(aName), price(aPrice) {}
    //getters
    string getName() const {
        return name;
    }

    double getPrice() const {
        return price;
    }
};

//menu and menu items have has-a relationship of composition
class Menu {
private:
	//static so all restaurant menus have same value and constant so it cannot be changed
    static const int MAX_ITEMS = 10;
    //array of menu items
    MenuItem items[MAX_ITEMS];
    int itemCount;

public:
	//default constructor
    Menu() : itemCount(0) {}
    
    //utility functions to change menu items
    void addMenuItem(const MenuItem& item) {
        if (itemCount < MAX_ITEMS) {
            items[itemCount++] = item;
        } else {
            cout<<"Menu is full. Cannot add more items."<<endl;
        }
    }

    void removeMenuItem(const string& itemName) {
        for (int i = 0; i < itemCount; ++i) {
            if (items[i].getName() == itemName) {
                for (int j = i; j < itemCount - 1; ++j) {
                    items[j] = items[j + 1];
                }
                itemCount--;
                break;
            }
        }
    }

    void displayMenu() const {
        cout << "Menu:\n";
        for (int i = 0; i < itemCount; ++i) {
            cout << items[i].getName() << " - $" << items[i].getPrice() << endl;
        }
    }
};


class Payment {
private:
    double amount;

public:
    Payment(double paymentAmount) : amount(paymentAmount) {}

    double getAmount() const {
        return amount;
    }
};

//order and payment class have a has-a relationship of association
class Order {
private:
    static const int MAX_ITEMS = 10;
    MenuItem items[MAX_ITEMS];
    int itemCount;
    Payment payment;

public:
    Order(const MenuItem* orderItems, int itemCount, const Payment& orderPayment) : itemCount(itemCount), payment(orderPayment) {
        for (int i = 0; i < itemCount; ++i) {
            items[i] = orderItems[i];
        }
    }

    void displayOrder() const {
        cout << "Ordered Items:\n";
        for (int i = 0; i < itemCount; ++i) {
            cout << items[i].getName() << " - $" << items[i].getPrice() << endl;
        }
        cout << "Total Amount: $" << payment.getAmount() << endl;
    }
};


class RestaurantOrder {
private:
    Menu menu;

public:
    void addMenuItemToMenu(const MenuItem& item) {
        menu.addMenuItem(item);
    }

    void removeMenuItemFromMenu(const string& itemName) {
        menu.removeMenuItem(itemName);
    }

    void displayMenu() const {
        menu.displayMenu();
    }

    void placeOrder(const MenuItem* items, int itemCount, const Payment& payment) {
        Order order(items, itemCount, payment);
        order.displayOrder();
    }
};

int main() {
    // Create a restaurant order class
    RestaurantOrder restaurant;

    //adding some menu items
    MenuItem item1("pasta", 11.36);
    MenuItem item2("lasagna", 12.50);
    restaurant.addMenuItemToMenu(item1);
    restaurant.addMenuItemToMenu(item2);

    //showing the menu
    cout << "Menu:\n";
    restaurant.displayMenu();

    //giving a order
    const MenuItem orderItems[] = {item1, item2};
    Payment payment(23.98);
    restaurant.placeOrder(orderItems, 2, payment);

    return 0;
}
