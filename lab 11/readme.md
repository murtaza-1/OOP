q1
#include <iostream>

using namespace std;

//base class
class Convert {
protected:
    double val1; //initial value
    double val2; //converted value

public:
    //parameterized constructor with an initializer list
    Convert(double v1 = 0, double v2 = 0) : val1(v1), val2(v2) {}

    //pure virtual function for computing the conversion
    virtual void compute() = 0;

    void display() const {
        cout << "Converted value: " << val2 << endl;
    }
};

//derived class for converting liters to gallons
class L_to_G : public Convert {
public:
    //parameterized constructor with initializer list
    L_to_G(double liters) : Convert(liters) {}

    //implementation 1 of the compute function
    void compute() override {
        val2 = val1 * 0.264172; // 1 liter = 0.264172 gallons
    }
};

//derived class for converting Fahrenheit to Celsius
class F_to_C : public Convert {
public:
    //parameterized constructor with initializer list
    F_to_C(double fahrenheit) : Convert(fahrenheit) {}

    //implementation 2 of the compute function
    void compute() override {
        val2 = (val1 - 32) * 5 / 9; //formula from Fahrenheit to Celsius
    }
};

int main() {
    //dma for the conversion classes
    Convert* convert1 = new L_to_G(4);
    Convert* convert2 = new F_to_C(70);

    convert1->compute();
    convert2->compute();

    cout << "Conversion 1: Liters to Gallons" << endl;
    convert1->display();

    cout << "Conversion 2: Fahrenheit to Celsius" << endl;
    convert2->display();

    //destructor
    delete convert1;
    delete convert2;

    return 0;
}
q2
#include <iostream>

using namespace std;

//abstract base class
class Account {
protected:
    int accountNumber;
    double balance;

public:
    //Parameterized constructor with initializer list
    Account(int accNum, double bal) : accountNumber(accNum), balance(bal) {}

    //pure virtual functions
    virtual void deposit(double amount) = 0;
    virtual void withdraw(double amount) = 0;
    virtual void calculateInterest() const = 0;

    //concrete member functions
    int getAccountNumber() const {
        return accountNumber;
    }
    double getBalance() const {
        return balance;
    }
};

//concrete subclass
class SavingsAccount : public Account {
private:
    double interestRate;

public:
    //parameterized constructor with initializer list and base class constructor
    SavingsAccount(int accNum, double bal, double rate)
            : Account(accNum, bal), interestRate(rate) {}

    //overridden member functions
    void deposit(double amount) override {
        balance += amount;
    }

    void withdraw(double amount) override {
        if (balance >= amount)
            balance -= amount;
        else
            cout << "Insufficient funds!" <<endl;
    }

    void calculateInterest() const override {
        double interest = balance * interestRate / 100.0;
        cout << "Interest earned: " << interest << endl;
    }
};

//concrete subclass 2
class CurrentAccount : public Account {
private:
    double overdraftLimit;

public:
    //parameterized constructor with initializer list and base class constructor
    CurrentAccount(int accNum, double bal, double limit)
            : Account(accNum, bal), overdraftLimit(limit) {}

    void deposit(double amount) override {
        balance += amount;
    }

    void withdraw(double amount) override {
        if (balance + overdraftLimit >= amount)
            balance -= amount;
        else
            cout << "Transaction cannot be completed due to insufficient funds and exceeding overdraft limit!" << endl;
    }

    void calculateInterest() const override {
        cout << "No interest earned on current account." <<endl;
    }
};


int main() {
    //savings account
    SavingsAccount savings(12345, 1000, 5); // Account number, balance, interest rate
    cout << "Savings Account Details:" <<endl;
    cout << "Account Number: " << savings.getAccountNumber() <<endl;
    cout << "Initial Balance: " << savings.getBalance() << endl;
    savings.calculateInterest();
    savings.deposit(500);
    cout << "Balance after deposit: " << savings.getBalance() << endl;
    savings.withdraw(200);
    cout << "Balance after withdrawal: " << savings.getBalance() << endl;
    savings.calculateInterest();

    //current account
    CurrentAccount current(54321, 2000, 500); // Account number, balance, overdraft limit
    cout << "\nCurrent Account Details:" << endl;
    cout << "Account Number: " << current.getAccountNumber() << endl;
    cout << "Initial Balance: " << current.getBalance() << endl;
    current.calculateInterest();
    current.deposit(300);
    cout << "Balance after deposit: " << current.getBalance() << endl;
    current.withdraw(2500);
    cout << "Balance after withdrawal: " << current.getBalance() << endl;
    current.calculateInterest();

    return 0;
}
q3

#include <iostream>
#include <string>

using namespace std;

//abstract base class
class Vehicle {
protected:
    string make;
    string model;
    int speed;

public:
    Vehicle(const std::string& mk, const std::string& mdl, int spd)
            : make(mk), model(mdl), speed(spd) {}

    //pure virtual functions
    virtual void accelerate() = 0;
    virtual void brake() = 0;
    virtual void calculateFuelEfficiency() const = 0;

    //concrete member functions
    string getMake() const {
        return make;
    }

    string getModel() const {
        return model;
    }

    int getSpeed() const {
        return speed;
    }
};

//concrete subclass 1
class Car : public Vehicle {
private:
    double fuelCapacity;

public:
    Car(const string& mk, const string& mdl, int spd, double fuelCap)
            : Vehicle(mk, mdl, spd), fuelCapacity(fuelCap) {}

    //overridden member functions
    void accelerate() override {
        speed += 10;
    }

    void brake() override {
        speed -= 10;
        if (speed < 0) speed = 0;
    }

    void calculateFuelEfficiency() const override {
        cout << "Fuel efficiency of the car is calculated based on its fuel capacity." <<endl;
    }
};

//concrete subclass 2
class Truck : public Vehicle {
private:
    int cargoCapacity;

public:
    Truck(const std::string& mk, const std::string& mdl, int spd, int cargoCap)
            : Vehicle(mk, mdl, spd), cargoCapacity(cargoCap) {}

    //overridden member functions
    void accelerate() override {
        speed += 5;
    }

    void brake() override {
        speed -= 5;
        if (speed < 0) speed = 0;
    }

    void calculateFuelEfficiency() const override {
        cout << "Fuel efficiency of the truck is calculated based on its cargo capacity." << endl;
    }
};


int main() {
    Car car("Toyota", "Camry", 60, 50.5); // Make, model, speed, fuel capacity
    cout << "Car Details:" << endl;
    cout << "Make: " << car.getMake() << endl;
    cout << "Model: " << car.getModel() << endl;
    cout << "Speed: " << car.getSpeed() << " km/h" << endl;
    car.accelerate();
    cout << "Speed after acceleration: " << car.getSpeed() << " km/h" << endl;
    car.brake();
    cout << "Speed after braking: " << car.getSpeed() << " km/h" << endl;
    car.calculateFuelEfficiency();

    // Creating a truck object
    Truck truck("Ford", "F-150", 50, 1000); // Make, model, speed, cargo capacity
    cout << "\nTruck Details:" << endl;
    cout << "Make: " << truck.getMake() << endl;
    cout << "Model: " << truck.getModel() << endl;
    cout << "Speed: " << truck.getSpeed() << " km/h" << endl;
    truck.accelerate();
    cout << "Speed after acceleration: " << truck.getSpeed() << " km/h" << endl;
    truck.brake();
    cout << "Speed after braking: " << truck.getSpeed() << " km/h" << endl;
    truck.calculateFuelEfficiency();

    return 0;
}
q4
#include <iostream>

using namespace std;

// Forward declaration of Perimeter class
class Perimeter {
private:
    double length;
    double breadth;

public:
    // Constructor to initialize length and breadth
    Perimeter(double l, double b) : length(l), breadth(b) {}

    // Friend function declaration
    friend class PrintClass;

    // Function to calculate perimeter
    double calculatePerimeter() const {
        return 2 * (length + breadth);
    }
};
// PrintClass class
class PrintClass {
public:
    // Function to display perimeter (friend function of Perimeter class)
    void displayPerimeter(const Perimeter& obj) {
        cout << "Perimeter: " << obj.calculatePerimeter() << endl;
    }
};

// Perimeter class


int main() {
    // Create an object of Perimeter class
    Perimeter perimeterObj(5, 3);

    // Create an object of PrintClass to display perimeter
    PrintClass printObj;

    // Display perimeter using PrintClass object
    printObj.displayPerimeter(perimeterObj);

    return 0;
}
