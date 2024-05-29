q1

using namespace std;

//global constant for the value of pi
const double PI = 3.14159265359;

class Shape {
	public:
    	//calculating area for a circle with formula pi*r*r
    	double Area(double radius) {
        	return PI * radius * radius;
    	}

    	//calculate area for rectangle with formula l*w
    	double Area(float length, float width) {
        	return length * width;
    	}

    	//calculating area for triangle with formula 0.5*b*h
    	double Area(float base, float height,int choice) {
        	return 0.5 * base * height;
    	}

    	//calculate perimeter for circle with formula of circumference
    	double Perimeter(double radius) {
        	return 2 * PI * radius;
    	}

    	//calculate perimeter for rectangle with formula of sum of all sides
    	double Perimeter(double length, double width) {
        	return 2 * (length + width);
    	}

    	//calculate perimeter for triangle with formula of sum of all sides
   		double Perimeter(double s1, double s2, double s3) {
        	return s1 + s2 + s3;
    	}
};

int main() {
	cout<<"murtazas\n23k-0076"<<endl;
	//instance of the class
    Shape shape;

    // areas
    cout<<"Area of circle with radius 5: " << shape.Area(5)<<endl;
    cout<<"Area of rectangle with length 4 and width 6: " << shape.Area(4, 6)<<endl;
    //3rd argument is added only to differentiate between overloaded functions
    cout<<"Area of triangle with base 3 and height 8: " << shape.Area(3, 8,1)<<endl;
    cout<<endl;
    // perimeters
    cout<<"Perimeter of circle with radius 5: "<<shape.Perimeter(5)<<endl;
    cout<<"Perimeter of rectangle with length 4 and width 6: "<<shape.Perimeter(4, 6)<<endl;
    cout<<"Perimeter of triangle with sides 3, 4, and 5: "<<shape.Perimeter(3, 4, 5)<<endl;

    return 0;
}
q2
#include <iostream>
#include <cmath> //for using sqrt function

using namespace std;

//global constant for the value of pi
const double PI = 3.14159265359;

//base class Shape
class Shape {
	public:
		//signature of virtual functions which will later be overidden
    	virtual double area() const = 0;
    	virtual double perimeter() const = 0;
    	virtual void displayProperties() const = 0;
    	//destructor
    	virtual ~Shape() {}
};

//derived class Circle shape class has been publically inherited
class Circle : public Shape {
	private:
    	double radius;

	public:
    	//parameterized constructor with initalizer list
		Circle(double r) : radius(r) {}
		
		//override keyword is used to override virtual fuctions. function is constant as it is a type of getter
		double area() const override {
        	return PI * radius * radius;
    	}
    	//overriden perimeter function
    	double perimeter() const override {
        	return 2 * PI * radius;
    	}
    	//display function for all properties
    	void displayProperties() const override {
        	cout<<"Properties of the Circle:"<<endl;
        	cout<<"- Area: "<<area()<<endl;
        	cout<<"- Perimeter: "<<perimeter()<<endl;
        	cout<<"- Diameter: "<<2 * radius<<endl;
    	}
};

//derived class Rectangle with public inheritance of shape
class Rectangle : public Shape {
	private:
    	double length;
		double width;
	
	public:
    	//parameterized constructor with initalizer list
		Rectangle(double alength, double awidth) : length(alength), width(awidth) {}
    
        //overriden function for area
		double area() const override {
        	return length * width;
    	}
    	//override perimeter function
    	double perimeter() const override {
        	return 2 * (length + width);
    	}	
    	void displayProperties() const override {
        	cout<<"Properties of the Rectangle:" <<endl;
        	cout<<"- Area: " << area() <<endl;
        	cout<<"- Perimeter: " << perimeter() <<endl;
        	//used pythagoras theorem to find value of diagnol of the rectangle
        	cout<<"- Diagonal: " << sqrt(length * length + width * width) <<endl;
    	}
};

//derived class Square with public inheritance of rectangle whichhas inheritance of Shape so a multi-level inheritance hierarchy
class Square : public Rectangle {
	public:
		//parametrized constructor with initializer list
    	Square(double side) : Rectangle(side, side) {}
    	
    	void displayProperties() const override {
        	cout<<"Properties of the Square:" <<endl;
        	cout<<"- Area: " << area() <<endl;
        	cout<<"- Perimeter: " << perimeter() <<endl;
    	}
};

//derived class Triangle
class Triangle : public Shape {
	private:
    	double side1;
		double side2;
		double side3;
	
	public:
		//parametrized constructor with initializer list
    	Triangle(double s1, double s2, double s3) : side1(s1), side2(s2), side3(s3) {}
		
		//overidden are function    
		double area() const override {
        	double s = perimeter() / 2;
        	//using herons formula to calculate area of triangle
        	return sqrt(s * (s - side1) * (s - side2) * (s - side3));
    	}
    	//overidden perimeter function
    	double perimeter() const override {
        	return side1 + side2 + side3;
    	}
    	//display function
    	void displayProperties() const override {
        	cout<<"Properties of the Triangle:" <<endl;
        	cout<<"- Area: " << area() <<endl;
        	cout<<"- Perimeter: " << perimeter() <<endl;
    	}
};

// Derived class EquilateralTriangle and it inherits triangle class for a multlevel inheritance hierearchy
class EquilateralTriangle : public Triangle {
	public:
		//parameterized constructor with initializer list. since all sides are equal same length will be passed
    	EquilateralTriangle(double side) : Triangle(side, side, side) {}
    
		void displayProperties() const override {
        	cout<<"Properties of the Equilateral Triangle:" <<endl;
        	cout<<"- Area: " << area() <<endl;
        	cout<<"- Perimeter: " << perimeter() <<endl;
    	}
};

int main() {
	cout<<"murtaza\n23k-0076\n\n"<<endl;
    cout << "Welcome to the Geometry Competition Calculator!" <<endl;
    string choice;
    do {
        cout<<"for equilateral triangle just choose triangle and add all sides to a equal value"<<endl;
        cout<<"Please select a shape:"<<endl;
        cout<<"1. Circle\n2. Rectangle\n3. Square\n4. Triangle"<<endl;
		int option;
        cout<<"Enter your choice: ";
        cin>>option;
        switch (option) {
            //for circle
			case 1: {
                double radius;
                cout<<"Enter the radius of the circle: ";
                cin>>radius;
                //DMA allocation of circle class and passing the argument
                Shape *circle = new Circle(radius);
                circle->displayProperties();
                //deallocation of memory
                delete circle;
                break;
            }
            //for rectangle
            case 2: {
                double length, width;
                cout<<"Enter the length of the rectangle: ";
                cin>>length;
                cout<<"Enter the width of the rectangle: ";
                cin>>width;
                //DMA allocaton of rectanble class
                Shape *rectangle = new Rectangle(length, width);
                rectangle->displayProperties();
                delete rectangle;
                break;
            }
            //for square
            case 3: {
                double side;
                cout<<"Enter the side length of the square: ";
                cin>>side;
                Shape *square = new Square(side);
                square->displayProperties();
                delete square;
                break;
            }
            //for equilateral triangle
            case 4: {
                double side1, side2, side3;
                cout<<"Enter the lengths of the three sides of the triangle: ";
                cin>> side1 >> side2 >> side3;
                Shape *triangle = new Triangle(side1, side2, side3);
                triangle->displayProperties();
                delete triangle;
                break;
            }
            default:
                cout << "Invalid choice!" <<endl;
        }
        cout<<"Do you want to calculate properties for another shape? (yes/no): ";
        cin>>choice;
    } while (choice == "yes");
    cout<<"Thank you for using the Geometry Competition Calculator!" <<endl;
    return 0;

    q3
    #include <iostream>
#include <string>

using namespace std;

//base class
class Employee {
	//protected so derived classes can access these data attributes
	protected:
    	int employeeID;
    	string employeeName;

	public:
    	//parameterized constructor with initalizer list
		Employee(int id, const string& name) : employeeID(id), employeeName(name) {}
		
		//default implementation. function is virtual so function overriding could occer
    	virtual double calculatePay() const {
        	return 0.0; // Default implementation
    	}
		
		//function is const as its a type of getter method
    	virtual void displayDetails() const {
        	cout<< "Employee ID: "<<employeeID << ", Name: "<<employeeName;
    	}
};

//derived class
class FullTimeEmployee : public Employee {
	private:
    	double monthlySalary;

	public:
		//parameterized constructor with initalizer list
    	FullTimeEmployee(int id, const string& name, double salary) : Employee(id, name), monthlySalary(salary) {}

		//overriding virtual function in base class
    	double calculatePay() const override {
        	return monthlySalary;
    	}
		//overriden virtual function
    	void displayDetails() const override {
    		//using scope resolution operator to access virtual function
        	Employee::displayDetails();
        	//adding more to the implementation of the previous function
        	cout<<", Type: Full-time, Monthly Salary: "<<monthlySalary << endl;
    	}
};

//derived class 2
class PartTimeEmployee : public Employee {
	private:
    	double hourlyWage;
    	double hoursWorked;
	
	public:
		//parametrized constructor with initializer list
    	PartTimeEmployee(int id, const string& name, double wage, double hours) : Employee(id, name), hourlyWage(wage), hoursWorked(hours) {}

    	double calculatePay() const override {
        	return hourlyWage * hoursWorked;
    	}

    	void displayDetails() const override {
        	Employee::displayDetails();
        	cout<<", Type: Part-time, Hourly Wage: "<< hourlyWage <<", Hours Worked: "<<hoursWorked<<endl;
    	}
};

int main() {
	cout<<"Murtaza\n23k-0076\n\n"<<endl;
    FullTimeEmployee fullTimeEmp(101, "Ahmed", 5000);
    PartTimeEmployee partTimeEmp(102, "Muhammad", 15, 40);

    cout<<"Displaying Details:"<<endl;
    fullTimeEmp.displayDetails();
    partTimeEmp.displayDetails();

    cout<<"\nCalculating Pay:"<<endl;
    cout<<"Full-time Employee Pay: $" <<fullTimeEmp.calculatePay()<<endl;
    cout<<"Part-time Employee Pay: $" <<partTimeEmp.calculatePay()<<endl;

    //using base class pointer to demonstrate early or static binding by storing derived class address in a base class pointer
    Employee* empPtr = &fullTimeEmp;
    //accessing a method using pointer
    cout<<"\nUsing base class pointer to calculate Full-time Employee Pay: $" << empPtr->calculatePay() << endl;

    return 0;
}
}
