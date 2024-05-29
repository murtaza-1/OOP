q1
#include <iostream>
#include <string>
#include <cstddef> // for NULLptr

using namespace std;

//class of pet
class Pet {
private:
    string name;
    string species;
    string healthStatus;
    int hungerLevel;
    int happinessLevel;
    string specialSkills[5];
    int numSpecialSkills;

public:
	// parametrized constructor with initializer list
    Pet(string n, string sp, string hs = "Healthy", int hl = 5, int hapl = 5) :
            name(n), species(sp), healthStatus(hs), hungerLevel(hl), happinessLevel(hapl), numSpecialSkills(0) {}
    
    //function to display pet details
    void displayPetDetails() {
        cout<<"Pet Name: "<<name<<endl;
        cout<<"Species: "<<species<<endl;
        cout<<"Health Status: "<<healthStatus<<endl;
        cout<<"Hunger Level: "<<hungerLevel<<endl;
        cout<<"Happiness Level: "<<happinessLevel<<endl;
        cout<<"Special Skills: ";
        for(int i=0;i< numSpecialSkills;i++) {
            cout<<specialSkills[i]<<", ";
        }
        cout<<endl;
    }
    
    //getter to access the name
    string getName() const { 
        return name;
    }
    
    //function to add special skills for the pet
    void addSpecialSkill(string skill) {
    	//only 5 skills per pet is possible max
        if (numSpecialSkills < 5) {
            specialSkills[numSpecialSkills++] = skill;
        }
    }

    void updateHappiness(string action) {
    	//updating happiness based on actions
    	//min max function used to implement limits for the values
        if(action=="feed") {
            happinessLevel=min(happinessLevel + 1, 10);
        } else if(action=="play") {
            happinessLevel=max(happinessLevel - 1, 0);
        }
        if(hungerLevel>=8) {
            happinessLevel=max(happinessLevel - 1, 0);
        }
    }

    void updateHealth() {
    	//updating hunger based on user action
        if (hungerLevel >= 8) {
            healthStatus = "Sick";
        } else if (hungerLevel <= 2) {
            healthStatus = "Healthy";
        }
    }
    
    void updateHunger(string action) {
    	//min max functions used to implement limits
        if (action == "feed") {
            hungerLevel = max(hungerLevel - 1, 0);
        } else if (action == "play") {
            hungerLevel = min(hungerLevel + 1, 10);
        }
        if (happinessLevel <= 2) {
            hungerLevel = min(hungerLevel + 1, 10);
        }
    }
};

class Adopter {
    private:
        string adopterName;
        string adopterMobileNum;
        //array of objecs of data-type pet
        Pet *adoptedPetRecords[3];
        int numAdoptedPets;

    public:
	    //parameterized constructor function with initalizer list
        Adopter(string name, string mobileNum) : adopterName(name), adopterMobileNum(mobileNum), numAdoptedPets(0) {}

        void adoptPet(Pet *pet/*passing pointer of array of data type object*/) {
        	//one adopter can oly adopt a max of 3 pets
            if (numAdoptedPets < 3) {
                adoptedPetRecords[numAdoptedPets++] = pet;
            }
        }
        
        //function to enable the adopter to return a pet if they want to 
        void returnPet(Pet *pet) {
            for(int i=0;i<numAdoptedPets;i++) {
                if (adoptedPetRecords[i] == pet) {
                    for (int j=i;j<numAdoptedPets-1;j++) {
                        adoptedPetRecords[j] = adoptedPetRecords[j + 1];
                    }
                    adoptedPetRecords[numAdoptedPets--] = NULL;
                    cout<< /*calling name getter function from its pointer of the object*/ pet->getName() << " has been returned." << endl;
                    return;
                }
            }
        }
    
    //function to display current adopted pets by a adopter
    void displayAdoptedPets() {
        cout<<"Adopted Pets by "<<adopterName<<":"<<endl;
        for(int i=0;i<numAdoptedPets;i++) {
            adoptedPetRecords[i]->displayPetDetails();
        }
    }
};

int main() {
	
	cout<<"CODE BY:\nMuhammad Abbas"<<endl;
	cout<<"23k-0068\n"<<endl;
    //Creating instances or objects of pets and initializing intial values using constructor functions
    Pet pet1("Buddy", "Dog", "Healthy", 5, 5);
    Pet pet2("Whiskers", "Cat", "Healthy", 5, 5);
    Pet pet3("Fluffy", "Rabbit", "Healthy", 5, 5);
    pet1.addSpecialSkill("dancing");
    pet1.addSpecialSkill("somersaults");
    pet1.addSpecialSkill("eating too much");
    pet1.addSpecialSkill("singing");
    
    pet2.addSpecialSkill("fighting");
    pet2.addSpecialSkill("sleeping");
    pet2.addSpecialSkill("eating");
    pet2.addSpecialSkill("whatever");
    
    pet3.addSpecialSkill("jumping");
    pet3.addSpecialSkill("carrots");
    pet3.addSpecialSkill("scratching ears");
    pet3.addSpecialSkill("cant think of a skill so random");
    
    //Creating instances of ouradopters
    Adopter adopter1("Alice", "1234567890");
    Adopter adopter2("Bob", "0987654321");

    //adopting pets by using pointers
    adopter1.adoptPet(&pet1);
    adopter2.adoptPet(&pet2);
    adopter2.adoptPet(&pet3);

    //Simulating some examples of interactions with the pets
    pet1.updateHappiness("feed");
    pet1.updateHealth();
    pet2.updateHunger("play");
    pet2.updateHealth();

    //Displaying adopted pets by each adopter
    adopter1.displayAdoptedPets();
    adopter2.displayAdoptedPets();

    return 0;
}
q2
#include <iostream>

using namespace std;

class Table {
    private:
	    //since it can only be 4 or 8 seats
        const int capacity;
        int occupiedSeats;
        bool clean;

    public:
        //Default constructor with initializer list
        Table() : capacity(4), occupiedSeats(0), clean(true) {}

        //Parameterized constructor initializer list is used as capacity is const so it cannot be changes using normal data assignment
        Table(int cap) : capacity((cap == 8 || cap == 4) ? cap : ((cap + 2) / 4 * 4)), clean(true), occupiedSeats(0) {}
        
        //all getters are intiialized as constant to make sure data isnt altered when being returned
        //Getter for capacity of the tabel
        int getCapacity() const {
            return capacity;
        }

        //Getter for occupied Seats of the table
        int getOccupiedSeats() const {
            return occupiedSeats;
        }

        //Getter for clean
        bool isClean() const {
            return clean;
        }

        //Function to use the table
        void useTable(int groupSize) {
        	// table can only be used if table is clean and group size if suitable for the table capacity(4 or 8)
            if(clean && groupSize<=capacity) {
                occupiedSeats=groupSize;
                cout<<"Table with capacity "<<capacity<<" is now occupied by a group of "<<groupSize<<endl;
            } else {
                cout<<"Table cannot be used by this group."<<endl;
            }
        }

        //Function for having lunch on the table
        void haveLunch() {
        	//table is no longer clean after lunch is had on the table
            clean=false;
            cout<<"Lunch is being had on the table."<<endl;
        }

        //Function for leaving the table
        void leaveTable() {
            occupiedSeats = 0;
            cout<<"occupants have left the table."<<endl;
        }

        // Function to clean the table
        void cleanTable() {
        	//if noone is sitting at the table so table can be cleaned
            if(occupiedSeats==0) {
                clean=true;
                cout<<"Table has been cleaned."<<endl;
            } else {
                cout<<"people are sitting at the table currently it cant be cleaned"<<endl;
            }
        }
};

//Globallly accessable function to occupy or use a table
void OccupyTable(Table tables[]/*array of tables*/, int groupSize) {
    for(int i=0;i<5;i++) {
    	//if current table that is being checked is not clean then move on to another table(next iteration of the loop) to seat the people
        if(!tables[i].isClean()) continue;
        //if num of people can be seated in the capacity of the table then use this table
        if (groupSize <= tables[i].getCapacity()) {
            tables[i].useTable(groupSize);
            return;
        }
    }
    cout << "No suitable table available."<<endl;
}

//Globally accessable function to empty a table
void EmptyTable(Table tables[], int tableNumber) {
	//emptying one of the 5 available tables
    if (tableNumber>=0 && tableNumber<5) {
    	//emptying a table and then cleaning it
        tables[tableNumber].leaveTable();
    } else {
        cout<<"Invalid table number."<<endl;
    }
}


int main() {
	cout<<"Muhammad Abbas\n23k-0068\n\n"<<endl;
	cout<<"welcome to table management system\n\n"<<endl;
	
    //initializing an array of 5 tables with their capacities
    Table tables[5] = {Table(8), Table(8), Table(4), Table(4), Table(4)};

    //Occupying table 1 with a group of 4
    cout<<"table1"<<endl;
    OccupyTable(tables, 4);
    cout<<endl;
    cout<<"table2"<<endl;
    //Occupying table 2 with a group of 6
    OccupyTable(tables, 6);
    cout<<endl;

    //Performing some actions on table 1
    //using table
    cout<<"actions being performed on table 1"<<endl;
    tables[0].useTable(4);
    //occupants having lunch on the table
    tables[0].haveLunch();
    //occupants leaving the table
    tables[0].leaveTable();
    //cleaning the table
    tables[0].cleanTable();
    cout<<endl;
    //Empty table 2 so index 1 is used as that is the second table
    cout<<"table2"<<endl;
    EmptyTable(tables, 1);

    return 0;
}
q3
#include<iostream>
#include<string>
#include <cstdlib> // For nullptr
#include <cmath>   // For abs()

using namespace std;

class chessPiece{
	private:
	    string name;
	    string color;
	    char symbol;
	
	public:
		//defalt constructor with initalizer list initializing a white pawn
		chessPiece() : name("Pawn"), symbol('P'), color("white") {}
		
		chessPiece(string aname, char asymbol, string acolor) {
			name=aname;
			color=acolor;
			symbol=asymbol;
		}
		//setter methods
		void set_name(string aname) {
			name=aname;
		}
		void set_color(string acolor) {
			color=acolor;
		}
		void set_symbol(char asymbol) {
			symbol=asymbol;
		}
		//getter methods
		string get_name()const {
			return name;
		}
		string get_color()const {
			return color;
	    }
	    char get_symbol()const {
			return symbol;
	    }
		
};

class chessBoard{
	public:
		chessPiece* board[8][8];
		
	    chessBoard() {
        for(int i=0;i<8;i++) {
            for(int j= 0;j<8; j++) {
                board[i][j] = nullptr;
            }
        }
        
        //upper case symbols are for white team and lower case symbols are for black team
        //Initialize all the white pieces with DMA
        board[0][0] = new chessPiece("Rook", 'R', "white");
        board[0][1] = new chessPiece("Knight", 'N', "white");
        board[0][2] = new chessPiece("Bishop", 'B', "white");
        board[0][3] = new chessPiece("Queen", 'Q', "white");
        board[0][4] = new chessPiece("King", 'K', "white");
        board[0][5] = new chessPiece("Bishop", 'B', "white");
        board[0][6] = new chessPiece("Knight", 'N', "white");
        board[0][7] = new chessPiece("Rook", 'R', "white");
        //initializing a whole row of pawns
		for(int i=0; i<8;i++) {
            board[1][i] = new chessPiece("Pawn", 'P', "white");
        }

        //Initialize all the black pieces with DMA
        //row of pawns
		for (int i=0; i<8;i++) {
            board[6][i] = new chessPiece("Pawn", 'p', "black");
        }
        board[7][0] = new chessPiece("Rook", 'r', "black");
        board[7][1] = new chessPiece("Knight", 'n', "black");
        board[7][2] = new chessPiece("Bishop", 'b', "black");
        board[7][3] = new chessPiece("Queen", 'q', "black");
        board[7][4] = new chessPiece("King", 'k', "black");
        board[7][5] = new chessPiece("Bishop", 'b', "black");
        board[7][6] = new chessPiece("Knight", 'n', "black");
        board[7][7] = new chessPiece("Rook", 'r', "black");
    }

    //destructor
    ~chessBoard() {
        for(int i=0;i<8;i++) {
            for(int j=0;j<8;j++) {
                delete board[i][j];
            }
        }
    }

    //Display the chessboard (kept constant as its like a getter method)
    void display() const {
        cout << "  a b c d e f g h " << endl;
        for(int i=0;i<8;i++) {
        	//mentioning the row numbers
            cout<<8 - i<<" ";
            for(int j=0; j < 8; j++) {
                if (board[i][j] == nullptr) {
                    cout<<". ";
                } else {
                	//symbol of the required pawn will be printed on the board
                    cout<<board[i][j]->get_symbol()<<" ";
                }
            }
            cout<<8 - i<<endl;
        }
        cout << "  a b c d e f g h " << endl;
    }
    
   bool movePiece(string& source, string& destination) {
    //Converting source and destination strings to row and column numerical valules
    //initial co-ordinates
    int sourceRow = 8 - (source[1] - '0');
    int sourceCol = source[0] - 'a';
    //co-ordinates where piece is supposed to go
    int destRow = 8 - (destination[1] - '0');
    int destCol = destination[0] - 'a';

    //limits validation for rows ad columns
    if (sourceRow<0 || sourceRow>=8 || sourceCol<0 || sourceCol>=8 || destRow<0 || destRow>=8 || destCol<0 || destCol>=8) {
        cout<<"Invalid coordinates."<<endl;
        return false;
    }

    //Getting the pointer to the chesspiece at the source position
    chessPiece* piece = board[sourceRow][sourceCol];

    //Checks if there is already a piece at the source position using nullptr that we intialized before
    if (piece == nullptr) {
        cout<<"There is no piece at the searched source position."<<endl;
        return false;
    }

    //Checks if the destination position is occupied by a piece of the same color
    if (board[destRow][destCol] != nullptr/*if position is not empty*/ && board[destRow][destCol]->get_color() == piece->get_color()/*same color piece already present there*/) {
        cout<<"Cannot move piece to the destination position occupied by a piece of the same color."<<endl;
        return false;
    }

    //Checks if the move is valid based on the type of piece
    char symbol = piece->get_symbol();
    //knight movement
    if (symbol == 'N' || symbol == 'n') { 
        //Calculate the difference in row and column indices
        //abs() fuction returns absolute value of any integer like the sign is ignored
        int rowDiff = abs(destRow - sourceRow);
        int colDiff = abs(destCol - sourceCol);

        //checks if knight movement is possible L shape by checking for 2 possible scenarios when this happens
        if ((rowDiff == 1 && colDiff == 2) || (rowDiff == 2 && colDiff == 1)) {
            //move the knight to the destination position
            delete board[destRow][destCol]; //remove or capture the piece at the destination if any
            board[destRow][destCol] = piece; //make the move of the piece
            board[sourceRow][sourceCol] = nullptr; //Set the source position to empty
            cout<<"Moved knight from "<<source<<" to "<<destination<<endl;
            return true;
        } else {
            cout<<"Invalid move for knight piece."<<endl;
            return false;
        }
    //now implementing logic for pawns
    } else if (symbol == 'P' || symbol == 'p') { 
        //see if it's the first move of the pawn beacuse here it can move one or two steps
        //ternary operator used to find if pawn is in the initial position or not
		int initialRow = piece->get_color() == "white" ? 6 : 1;
		//-1 to move up and 1 to move down
        int step = piece->get_color() == "white" ? -1 : 1;
        //scenario where attempy to make a double movement is made
        if (sourceRow == initialRow && destCol == sourceCol && (destRow == sourceRow + step || destRow == sourceRow + 2 * step)) {
            //checks if there is no piece in the path for a two-step move
            if (destRow == sourceRow + 2 * step && board[sourceRow + step][sourceCol]) {
                cout << "Cannot move pawn. a piece is in the way" <<endl;
                return false;
            }

            //move pawn to the destination position
            delete board[destRow][destCol]; //Deleting the piece if any at the destination
            board[destRow][destCol] = piece; //move the piece to the destination
            board[sourceRow][sourceCol] = nullptr; //set the source position to empty
            cout<<"Moved pawn from "<<source<<"to "<<destination<<endl;
            return true;
        //scenario where single movement move is being made
        } else if (destCol == sourceCol && destRow == sourceRow + step) {
            // Check if the destination position is empty
            if (!board[destRow][destCol]) {
                //move the pawn to the destination position
                delete board[destRow][destCol]; 
                board[destRow][destCol] = piece;
                board[sourceRow][sourceCol] = nullptr; 
                cout<<"Moved pawn from " <<source<<" to "<<destination<<endl;
                return true;
            } else {
                cout << "Cannot move the pawn as the destination position is occupied."<<endl;
                return false;
            }
        } else {
            cout<<"Invalid move for the pawn."<<endl;
            return false;
        }
    } else {
        cout << "this movement not supported for this piece."<<endl;
        return false;
    }

    //perform the move by updating the new position with the piece and the old postion with a nullptr
    board[destRow][destCol] = piece;
    board[sourceRow][sourceCol] = nullptr;

    return true;
}

};

int main() {
	cout<<"Murtaza\n23k-0076\n\n"<<endl;
	chessBoard board;
	board.display();
    
	//scenario where a valid move was made	
	string source = "b8";
    string destination = "a6";
    cout<<"Is move from b8 to a6 valid? "<<(board.movePiece(source, destination) ? "Yes" : "No")<<endl;
    
    //ascenario where a invalid move was made
    source = "b8";
    destination = "d7";
    cout<<"\n\nIs move from b8 to d7 valid? "<<(board.movePiece(source, destination) ? "Yes" : "No")<<endl;


    // Display the updated status of the board
    cout<<"\n\nboard with the knight moved shown"<<endl;
    board.display();
 
    //scenario where knight from opposite team is moves 	
    source = "g1";  
    destination = "h3";  
    cout<<"Is move from g1 to h3 valid? "<<(board.movePiece(source, destination) ? "Yes" : "No") <<endl;
    board.display();
}

q4
#include<iostream>
#include<string>
#include<cmath>

using namespace std;

class roller_coaster{
	private:
	    string name;
	    //max height the roller coaster can reach
	    float height;
	    //length of the roller coaster track
	    float length;
	    float speed;
	    int capacity;
	    int current_riders;
	    bool ride_in_progress;
	    
	public:
		//default constructor
		roller_coaster() : name("roller coaster"), height(500), length(2000), speed(0), capacity(20), current_riders(0), ride_in_progress(false) {}
		
		//parameterized constructor
		roller_coaster(string aname, float aheight, float alength, float aspeed, int acapacity, int occupiers) {
			name=aname;
			height=aheight;
			length=alength;
			speed=aspeed;
			//checks for the capacity values being made
			if(acapacity>3) {
				if(acapacity%2==0 || acapacity%3==0){
					capacity=acapacity;
				} else{
					 capacity = ((acapacity + 1) / 2) * 2;//formula to round to the nearest multiple of 2
				}
			}else {
				cout<<"minimum limit of people not reached"<<endl;
			}
			current_riders=occupiers;
		}
		
		//setter functions
		void set_name(string aname) {
			name=aname;
		}
		void set_height(float aheight) {
			height=aheight;
		}
		void set_length(float alength) {
			length=alength;
		}
		void set_speed(float aspeed) {
			speed=aspeed;
		}
		void set_capacity(int acapacity) {
			if(acapacity>3) {
				if(acapacity%2==0 || acapacity%3==0){
					capacity=acapacity;
				} else{
					 capacity = ((acapacity + 1) / 2) * 2;;
				}
			}else {
				cout<<"minimum limit of people not yet exceeded"<<endl;
			}
		}
		void set_currentriders(int occupiers) {
			current_riders=occupiers;
		}
		void set_flag(bool aflag) {
			ride_in_progress=aflag;
		}
		
		//getter functions
		string get_name() {
			return name;
		}
		float get_height() {
			return height;
		}
		float get_length() {
			return length;
		}
		float get_speed() {
			return speed;
		}
		int get_capacity() {
			return capacity;
		}
		int get_currentriders() {
			return current_riders;
		}
		bool get_flag() {
			return ride_in_progress;
		}
		
		//function to load riders on the roller coaster
		int loadRiders(int numRiders) {
            if (!ride_in_progress && numRiders<=(capacity-current_riders)) {
                current_riders=current_riders+numRiders;
                return 0; //all riders were successfully seated
            } else {
            	//calculating leftover people after railway is full
                int remainingRiders = numRiders - (capacity - current_riders);
                //since ride is at full capacity               
				current_riders=capacity;
                return remainingRiders; // Return the remaining riders not seated
            }
        }
        
        int startRide() {
        	//if ride is not started yet
            if (!ride_in_progress) {
            	//checking if al the seats in the ride have been occupied or not
                if(current_riders==capacity) {
                    ride_in_progress=true;
                    return 0; //Ride has started successfully
                } else {
                    return capacity - current_riders; //Return number of empty seats yet left
                }
            } else {
                return -1; //this tell that ride is already in progress
            }
        }   
        
        void stopRide() {
        	//stopping the ride if it is in progress
            if (ride_in_progress) {
                ride_in_progress = false;
                cout<<"ride is stopping"<<endl;
            }
        }
        
        void unloadRiders() {
        	if(!ride_in_progress) {
			    current_riders = 0;
				cout<<"unloading people from the ride"<<endl;	
			}
        }
        
        //function to accelerate the ride(my roll number will be added)
        void accelerate(int aspeed) {
        	int digit;
        	//will keep extarcting last digits untill it not zero and then add that digit to the speed of the roller coaster
        	while(aspeed!=0) {
        		digit=aspeed%10;
        		if(digit!=0) {
        		    speed=speed+digit;
        		    cout<<"speed has been accelerated to "<<speed<<endl;
        		    break;
			    } else{
			    	aspeed=aspeed/10;
				}   
			}
		}
		
		//brake function as the same logic as the accelerate function
		void brake(int aspeed) {
        	int digit;
        	//will keep extarcting last digits untill it not zero and then add that digit to the speed of the roller coaster
        	while(aspeed!=0) {
        		digit=aspeed%10;
        		if(digit!=0) {
        		    speed=speed-digit;
        		    cout<<"speed has been slowed down to "<<speed<<endl;
        		    break;
			    } else{
			    	aspeed=aspeed/10;
				}   
			}
		}
		
};

int main() {
	cout<<"murtaza\n23k-0076\n\n"<<endl;
	
    //first instance of the class being initialized with the default constructor	
	roller_coaster rollerCoaster1; 
	//second instance of the class being initialized with the default constructor
    roller_coaster rollerCoaster2("playing with life", 600, 2500, 30, 50, 40); 

    //Displaying the roller coaster details
    cout<<"Roller Coaster 1 Details:"<<endl;
    cout<<"Name: " <<rollerCoaster1.get_name()<<endl;
    cout<<"Height: " <<rollerCoaster1.get_height()<<" meters"<<endl;
    cout<<"Length: " << rollerCoaster1.get_length() << " meters"<<endl;
    cout<<"Speed: " << rollerCoaster1.get_speed()<< " km/h"<<endl;
    cout<<"Capacity: " << rollerCoaster1.get_capacity()<<" riders"<<endl;
    cout<<"current riders: "<<rollerCoaster1.get_currentriders()<<endl;
    cout<<endl;

    cout<<"Roller Coaster 2 Details:"<<endl;
    cout<<"Name: " << rollerCoaster2.get_name()<<endl;
    cout<<"Height: " << rollerCoaster2.get_height()<< " meters" <<endl;
    cout<<"Length: " << rollerCoaster2.get_length()<< " meters" <<endl;
    cout<<"Speed: " << rollerCoaster2.get_speed()<< " km/h" <<endl;
    cout<<"Capacity: " << rollerCoaster2.get_capacity()<<" riders"<<endl;
    cout<<"current riders: "<<rollerCoaster2.get_currentriders()<<endl;
    cout<<endl;
    
    //giving my roll number as argument to the brake and accelerate functions
    cout<<"performing actions on roller coaster 2"<<endl;
    if(rollerCoaster2.loadRiders(10)==0) {
    	cout<<"all riders were seated successfuly"<<endl;
	} else {
		cout<<"remaining number of riders are: "<<rollerCoaster2.loadRiders(10)<<endl;
	}
    rollerCoaster2.loadRiders(10);
    rollerCoaster2.startRide();
    rollerCoaster2.accelerate(230068);
    rollerCoaster2.brake(230068);
    rollerCoaster2.stopRide();
    rollerCoaster2.unloadRiders();

    return 0;
	
}
q5
#include <iostream>

using namespace std;

class restaurant{
	private:
		string name;
		string location;
		string menu_list[5];
		float prices[5];
		string coupon_codes[5];
		//static variable to record number of coupons already used
		static int redeemed_coupons;
		
	public:
		
		//parameterized constructor with initializer list
		restaurant(string aname, string loc, string* menu, float* price, string* coupons) {
            name=aname;
			location = loc;
			for(int i=0 ;i<5;i++) {
				menu_list[i] = menu[i];
				prices[i] = price[i];
                coupon_codes[i] = coupons[i];
			}
            
        }
        
        
        
		
		void display_menu() {
			cout<<"this is the menu of the restaurant "<<name<<endl;
			for(int i =0; i<5;i++) {
				cout<<"menu item "<<i<<" is "<<menu_list[i]<<" with the price $"<<prices[i]<<endl;
			}
			cout<<endl;
		}
		
		void generate_bill(int* quantity) {
			float sum = 0;
			cout<<"\n\nbill for "<<name<<endl;
			for(int i =0; i<5;i++) {
				if(quantity[i]!=0) {
					cout<<"item name: "<<menu_list[i]<<"\tquantity: "<<quantity[i]<<" \tprice: $"<<prices[i]*quantity[i]<<endl;
					sum =sum+ (prices[i] * quantity[i]);
				}
			}
			cout<<"the total amount is: $"<<sum<<endl;
		}
		
		//function to check if coupon codes are valid
		bool valid_coupon(string code) {
			for(int i=0;i<5;i++) {
				if(coupon_codes[i]==code) {
					return true;
				}
			}
			return false;
		}
		
		static int get_redeemed_coupons_count() {
			return redeemed_coupons;
		}
		
};



class BOGOCoupon{
	public:
		//specific alphanumeric code to identify coupon
		string code;
		//month number will be used to check validity
		int valid_from;
		int valid_until;
		//special code to show which restaurant is the coupon associated with
		string restaurant_name;
		
	public:
		//parameterized constructor with initializer list
		BOGOCoupon(string acode, int from, int until, string restaurant) : code(acode), valid_from(from), valid_until(until), restaurant_name(restaurant) {}
        
        bool is_valid(string restaurant, string code, int current_month) {
        	//checking if coupon is of the selected restaurant
			if(restaurant_name!=restaurant) {
        		cout<<"this coupon does not belong to this restaurant"<<endl;
        		return false;
			}
			
			//checking the expiry date of the coupon code
			if(current_month >= valid_from && current_month <= valid_from) {
				cout<<"coupon is valid"<<endl;
				return true;
			} else {
				cout<<"the coupon has expired"<<endl;
				return false;
			}
		}
		
};

class user:  public BOGOCoupon{
	private:
		string name;
		int age;
		string mobile_num;
		//pointer to array of strings holding the coupons held by the user and the coupons that have already been used by the user
	public:
		string* coupons;
		string* redeemed_coupons;
		
	public:
		//parameterixed constructor with initalizer list and constructor of inherited class as well
	    user(string n, int a, string mobile, string acode, int from, int until, string restaurant) :
            BOGOCoupon(acode, from, until, restaurant), name(n), age(a), mobile_num(mobile) {
            //using DMA for giving storage to these arrays
            coupons = new string[5];
            redeemed_coupons = new string[5];
        }
        
        //destructor
        ~user() {
            delete[] coupons;
            delete[] redeemed_coupons;
        }
        
        //function to add a coupon to the coupon list of the user
        void accumulate_coupon(string coupon) {
           //assuming coupons list is not full
            for (int i = 0; i < 5;i++) {
            	//will find next empty space and store the coupon code in that space
                if (coupons[i] == "") {
                    coupons[i] = coupon;
                    break;
                }
            }  
        }
		
		//using inherited method from base class BOGOCoupon for this function implementation
		bool Has_valid_coupon(string code, string restaurant, int current_month) {
			for(int i=0;i<5;i++) {
				if(redeemed_coupons[i]!=code) {
					if (is_valid(restaurant, code, current_month)) {
				            return true;
			        } 
			        return false;
		        } else {
		        	cout<<"coupon has already been redeemed"<<endl;
		        	return false;
				}
						
			}
		}
		
		//function to redeem coupon code with validity checks made with another function within the same class
		bool redeem_coupon(string code, string restaurant, int current_month) {
			
			if(!Has_valid_coupon(code, restaurant, current_month) ) {
                cout<<"Coupon is not valid check validity"<<endl;
                return false;
            } else {
            	//if coupon is vaid it is redeemed successfully
            	for(int i=0;i<5;i++) {
            		if(redeemed_coupons[i]=="") {
            			redeemed_coupons[i]=code;
            			cout<<"coupon redeemed successfully"<<endl;
            			return true;
					}
				}
			}
			cout<<"coupon not found"<<endl;
		}

};

//simulated various functionaities in the main function
int main() {
	cout<<"Murtaza\n23k-0076\n\n"<<endl;
	
	//intializing menu for first restaurant
	string food_haven_menu[5] = {"Sushi", "Pad Thai", "Mango Tango", "",""};
	//initalizing prices for the above dishes
    float food_haven_prices[5] = {10.99, 12.99, 8.99,0,0};
    string food_haven_coupons[5] = {"FH-BOGO-12345", "","","",""};
    //initializig object of type restaurant with all values
	restaurant food_haven("Food Haven", "City Center", food_haven_menu, food_haven_prices, food_haven_coupons);
    
    //menu for the second restaurant
    string pixel_bites_menu[5] = {"Binary Burger", "Quantum Quinoa", "Data Donuts", "",""};
    //prices for the above items
	float pixel_bites_prices[5] = {8.99, 10.99, 6.99,0,0};
    string pixel_bites_coupons[5] = {"PB-BOGO-67890", "","","",""};
    //instance of the class
	restaurant pixel_bites("Pixel Bites", "Cyber Street", pixel_bites_menu, pixel_bites_prices, pixel_bites_coupons);

    food_haven.display_menu();
    pixel_bites.display_menu();
    
    
    
    //initializing coupon objects
    BOGOCoupon coupon1("FH-BOGO-12345",3,6,"Food Haven");
    BOGOCoupon coupon2("PB-BOGO-6789",2,5,"Pixel Bites");
    BOGOCoupon coupon3("PB-BOGO-67890",2,5,"Pixel Bites");
    
    //a user object to use this system
    user User("Muhammad", 20, "03322236757","FH-BOGO-12345",3,6,"Food Haven");
    User.accumulate_coupon("FH-BOGO-12345");
    User.accumulate_coupon("PB-BOGO-67890");
    User.accumulate_coupon("PB-BOGO-6789");

    cout<<"a instance where coupon is valid"<<endl;
    if (User.Has_valid_coupon(coupon1.code, coupon1.restaurant_name, 3)) {
        if (User.redeem_coupon(coupon1.code, coupon1.restaurant_name, 3)) {
            cout << "Coupon redeemed successfully!" <<endl;
        }
    }
    
    cout<<"\na instance where the coupon code in entered incorrectly:"<<endl;
    if (User.Has_valid_coupon(coupon2.code, coupon2.restaurant_name, 3)) {
        if (User.redeem_coupon(coupon2.code, coupon2.restaurant_name, 3)) {
            cout << "Coupon redeemed successfully!" <<endl;
        }
    }
    
    cout<<"\na instance where the coupon entered has already been redeemed"<<endl;
    if (User.Has_valid_coupon(coupon1.code, coupon1.restaurant_name, 3)) {
        if (User.redeem_coupon(coupon1.code, coupon1.restaurant_name, 3)) {
            cout << "Coupon redeemed successfully!" <<endl;
        }
    }
    
    cout<<"\ndemonstrating printing the bill when a user chooses something to order"<<endl;
    
    cout<<"lets say we are generating a bill for the food haven restaurant"<<endl;
    
    int quantity[5];
	for(int i=0; i<5; i++) {
    	cout<<"enter quantity for menu item "<<i+1<<endl;
    	cin>>quantity[i];
	}
	food_haven.generate_bill(quantity);
	
	cout<<"\nnow lets say we are generating a bill for the pixel bites restaurant"<<endl;
    int quantity2[5];
	for(int i=0; i<5; i++) {
    	cout<<"enter quantity for menu item "<<i+1<<endl;
    	cin>>quantity2[i];
	}
	pixel_bites.generate_bill(quantity2);
    
	
}
