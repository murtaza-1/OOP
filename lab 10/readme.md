q1
#include <iostream>
#include <string>

using namespace std;

// class prototyping
class Logo;

// class to represent the social media platform
class Platform
{
private:
    string name;

public:
    // parameterized constructor with initalizer list
    Platform(string platformName) : name(platformName) {}
    void display(const Logo &logo) const;
};

class Server
{
private:
    string ipAddress;

public:
    // parameterized constructor with initalizer list
    Server(string serverIpAddress) : ipAddress(serverIpAddress) {}
    void display(const Logo &logo) const;
};

// class definition of above prototyped class
class Logo
{
private:
    string image;

public:
    // parameterized constructor with initalizer list
    Logo(string logoImage) : image(logoImage) {}
    // friend functions prototyping
    friend void changeLogo(Logo &logo, const string &newImage);
    friend void Platform::display(const Logo &logo) const;
    friend void Server::display(const Logo &logo) const;
};

// friend function definitions
void changeLogo(Logo &logo, const string &newImage)
{
    logo.image = newImage;
}

void Platform::display(const Logo &logo) const
{
    cout << "Platform: " << name << endl;
    cout << "Logo: " << logo.image << endl;
}

void Server::display(const Logo &logo) const
{
    cout << "Server IP Address: " << ipAddress << endl;
    cout << "Logo: " << logo.image << endl;
}

int main()
{
    // original logo
    Logo originalLogo("Blue Bird");

    // Creating instances of Platform and Server
    Platform twitter("Twitter");
    Server server("127.9.8.1");

    // Display original logo
    cout << "Original Logo:" << endl;
    twitter.display(originalLogo);
    server.display(originalLogo);
    cout << endl;

    // Change logo to Doge Coin
    changeLogo(originalLogo, "Doge Coin");

    // Display modified logo
    cout << "Modified Logo:" << endl;
    twitter.display(originalLogo);
    server.display(originalLogo);

    return 0;
}
q2
#include <iostream>

using namespace std;

class Number {
private:
    int value;

public:
    //parameterized constructor with initializer list
    Number(int val) : value(val) {}

    //overloading prefix decrement operator
    Number operator--() {
        value *= 4;
        return *this;
    }

    //postfix overload so int parameter is added
    Number operator--(int) {
        Number temp(value);
        value /=4;
        return temp;
    }

    // Method to display the value of the number
    void display() const {
        cout << "Value: " << value << endl;
    }
};

int main() {
    Number num(8);

    cout << "Original Value:" << endl;
    num.display();

    // Prefix decrement
    --num;
    cout << "Value after Prefix Decrement:" << endl;
    num.display();

    // Postfix decrement
    num--;
    cout << "Value after Postfix Decrement:" << endl;
    num.display();

    return 0;
}
q3
#include <iostream>

using namespace std;

class Shape {
private:
    double length;
    double width;
    double area; 

public:
    //parametrized constructor
    Shape(double l, double w) : length(l), width(w) {
        area = length * width;
    }

    //overloading the operator to add the areas of two shape objects
    Shape operator+(const Shape& other) const {
        // Create a new shape object with combined dimensions
        Shape combined(length + other.length, width + other.width);
        // Set the area of the combined shape by adding areas of both objects
        combined.area = area + other.area;
        return combined;
    }

    void Display() const {
        cout << "Length: " << length << ", Width: " << width << endl;
    }

    // Function to display the area of the shape
    void DisplayArea() const {
        cout << "Area: " << area << endl;
    }
};

int main() {
    // Creating two shape objects
    Shape shape1(5, 3);
    Shape shape2(4, 2);

    // Displaying the dimensions of shape1 and shape2
    cout << "Shape 1:" << endl;
    shape1.Display();
    cout << "Shape 2:" << endl;
    shape2.Display();

    // Displaying the area of shape1 and shape2
    cout << "Area of Shape 1:" << endl;
    shape1.DisplayArea();
    cout << "Area of Shape 2:" << endl;
    shape2.DisplayArea();

    //Adding the areas of shape1 and shape2 
    Shape totalShape = shape1 + shape2;

    //Displaying the area of the resulting shape
    cout << "Total Area:" << endl;
    totalShape.DisplayArea();

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
