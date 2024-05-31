#include <iostream>
#include <string>
#include <unistd.h>
#include <vector>
#include <map>
#include <fstream>
#include <fstream>
#include <iomanip>
#include <ctime>
using namespace std;

const int maxrow = 10;
int CurrentPlayer = 1;
int GameCounter = 1;
string PlayerNames[6];
struct ReviewQuestion;
struct Player;
int main();
vector<ReviewQuestion> reviewList;
map<string ,Player> playerData;
int NumberOfPlayers, Seconds, Number, Choice, Option, Menu, Admin;
struct ReviewQuestion{
    int index;
    string name;
    string question;
    char cAnswer;
    char pAnswer;

};
struct Player{
    string name;
    int score = 0;
    int answered = 1;
};



void sort_player_score() {

    int n = playerData.size();
    for (int row = 0; row < n; ++row) {
        for (int col = 0; col < n - row - 1; ++col) {
            if (playerData[PlayerNames[col]].score < playerData[PlayerNames[col + 1]].score) {

                string temp = PlayerNames[col];
                PlayerNames[col] = PlayerNames[col + 1];
                PlayerNames[col + 1] = temp;
            }
        }
    }
}

string getTimestamp() {
    time_t now = time(0);
    tm *ltm = localtime(&now);
    stringstream ss;
    ss << ltm->tm_year + 1900 << "-" << ltm->tm_mon + 1 << "-" << ltm->tm_mday << " " << ltm->tm_hour << ":" << ltm->tm_min << ":" << ltm->tm_sec;
    return ss.str();
}
void saveRecord() {
    sort_player_score();
    int  remark = 1;
    ofstream file("C:\\leaderboard.txt", ios::app);
    if (file.is_open()) {
        file << "--------------------------------------------------------------------------------------------\n";
        file << getTimestamp() << endl;
        file << NumberOfPlayers << " PLAYERS" << endl;
        int counter = 0;
        for (int i = 1; i <= NumberOfPlayers; ++i) {
            counter++;
            file <<"Player: " << playerData[PlayerNames[i-1]].name << " | "
            <<"Answered Questions: " << playerData[PlayerNames[i-1]].answered << " | "
            <<"Score: " << playerData[PlayerNames[i-1]].score << endl;
            file << "******" << endl;
    }
        file << endl;
        file << endl;
        file << "\t\t\t\t\t\t  +----------------------------------------+" << endl;
        file << "\t\t\t\t  +----------------------------------------+" << endl;
        file << "\t\t\t\t\t\t\t  LEADERBOARD" << endl;
        file << "\t\t\t\t\t\t  +----------------------------------------+" << endl;
        file << "\t\t\t\t  +----------------------------------------+" << endl;
        file << "\n\n";
        file << "\t\t\t\t\t" << left << setw(15) << "Player"
             << left << setw(15) << "Score"
             << left << setw(15) << "Remarks" << endl;
        file << endl;

        for(string player : PlayerNames){
             if(player != ""){
                file << "\t\t\t\t\t"<< left << setw(15) <<playerData[player].name
                 << left << setw(15) << playerData[player].score
                 << left << setw(15) << remark << endl;
                remark++;
             }
        }
        file << "--------------------------------------------------------------------------------------------\n";
        file.close();
    } else {
        cout << "Unable to open file for saving records." << endl;
    }
}

void save_for_review(int index,string name,string question,char cAnswer,char pAnswer){
    ReviewQuestion reviewQuestion;
    reviewQuestion.index = index;
    reviewQuestion.name = name;
    reviewQuestion.question = question;
    reviewQuestion.cAnswer = cAnswer;
    reviewQuestion.pAnswer = pAnswer;
    reviewList.push_back(reviewQuestion);
}
string questions[] = {
	"What is the chemical symbol for water?\n\n\t\t\t\t\t\t    -A) HO B) H2O C) UA D) 2HO",
	"Who is known as the father of modern physics?\n\n\t\t       -A) Albert Einstein B) Isaac Newton C) Galileo Galilei D) Nikola Tesla",
	"What is the largest organ in the human body?\n\n\t\t\t\t	   -A) Liver B) Brain C) Skin D) Intestine",
	"What is the capital city of Japan?\n\n\t\t\t\t\t  -A) Beijing B) Seoul C) Tokyo D) Osaka",
	"Which of the following Philippine islands is the largest in terms of land area?\n\n\t\t\t\t    -A) Luzon B) Palawan C) Mindanao D) Visayas",
	"Which African country is famous for its ancient pyramids and the Nile River?\n\n\t\t\t\t    -A) Kenya B) Nigeria C) South Africa D) Egypt",
	"What is the capital city of the Philippines?\n\n\t\t\t\t    -A) Cebu City B) Manila C) Davao City D) Quezon City",
	"What is the process by which plants release water vapor into the atmosphere?\n\n\t\t\t    -A) Precipitation B) Condensation C) Transpiration D) Evaporation",
	"What is the main function of the human respiratory system?\n\n    -A) Circulation of blood B) Digestion of food C) To facilitate gas exchange D) Regulation of body temperature",
	"What is the powerhouse of the cell?\n\n\t\t\t\t    -A) Chloroplast B) Nucleus C) Ribosome D) Mitochondria",
	"What is the capital city of Thailand?\n\n\t\t\t\t    -A) Bangkok B) Phnom Penh C) Jakarta D) Phuket",
	"What is the force that pulls objects towards the center of the Earth?\n\n\t\t\t\t    -A) Magnetism B) Friction C) Gravity D) Electrostatic force",
	"What is the chemical formula for table salt?\n\n\t\t\t\t\t    -A) NaCl2 B) H2O2 C) NaOH D) NaCl",
	"Which among the following is the largest known number in the world?\n\n\t\t\t\t\t    -A) Infinity B) Googol C) Googolplex D) Gram",
	"The city of Sydney, famous for its Opera House and Harbour Bridge, is located in which Australian state?\n\n\t\t\t    -A) New South Wales B) Victoria C) Queensland D) Western Australia",
	"Find the missing terms in multiple of 3:3,6,9,15\n\n\t\t\t\t\t\t    -A) 10 B) 11 C) 12 D) 13",
	"What process do plants use to make their food?\n\n\t\t\t    -A) Fermentation B) Respiration C) Photosynthesis D) Combustion",
	"110 divided by 10 is:\n\n\t\t\t\t\t\t-A) 11 B) 10 C) 5 D) None of these",
	"60 Times of 8 Equals to?\n\n\t\t\t\t\t    -A) 480 B) 300 C) 250 D) 400",
	"The Amazon Rainforest, the largest tropical rainforest in the world, is primarily located in which South \nAmerican country?\n\n\t\t\t\t    -A) Brazil B) Colombia C) Peru D) Venezuela",
	"What is the process by which solid ice changes directly into water vapor without passing through the \n liquid phase?\n\n\t\t\t\t-A) Evaporation B) Melting C) Sublimation D) Condensation",
	"What is the solution to the equation (2x^2 - 5x + 2 = 0)?\n\n\t\t    -A) x = 1, x = 2 B) x = -1, x = -2 C) x = 1/2, x = 2/3 D) x = -1/2, x = -2/3",
	"Which river is considered the lifeline of India, supporting agriculture and transportation?\n\n\t\t\t\t    -A) Ganges B) Yangtze C) Nile D) Amazon",
	"Mount Rascuuko is the highest mountain in which country?\n\n\t\t\t\t -A) Australia B) Canada C) Brazil D) South Africa",
	"Lake Titicaca, the highest navigable lake in the world, is located on the border of which two South American \ncountries?\n\n\t\t  -A) Peru and Ecuador B) Bolivia and Argentina C) Peru and Bolivia D) Chile and Argentina",
	"Which country is known as the Land of the Rising Sun?\n\n\t\t\t\t    -A) China B) South Korea C) Japan D) Thailand",
	"What is the square root of 144?\n\t\t\t\t\t\t-A) 8 B) 12 C) 14 D) 16",
	"Which mountain range is located between Europe and Asia?\n\n\t\t\t\t-A) Rocky Mountains B) Andes C) Alps D) Ural Mountains",
	"What is the process by which plants convert light energy into chemical energy?\n\n\t\t\t    -A) Respiration B) Photosynthesis C) Germination D) Transpiration",
	"Which country is the largest landlocked country in the world?\n\n\t\t\t\t-A) Mongolia B) Kazakhstan C) Uzbekistan C) Turkmenistan"
};

char UpperCaseAnswer[] = {'B', 'A', 'C', 'C', 'A', 'D', 'B', 'C', 'C', 'D', 'A', 'C', 'D', 'B', 'A', 'C', 'A', 'A', 'D', 'C', 'A', 'A', 'A', 'C', 'B', 'B', 'B', 'D', 'B', 'B'};
char LowerCaseAnswer[] = {'b', 'a', 'c', 'c', 'a', 'd', 'b', 'c', 'c', 'd', 'a', 'c', 'd', 'b', 'a', 'c', 'a', 'a', 'd', 'c', 'a', 'a', 'a', 'c', 'b', 'b', 'b', 'd', 'b', 'b'};


int EasyScores[31] = {0};
int AverageScores[31] = {0};
int HardScores[31] = {0};
int TotalScores[31] = {0};
//int NumberOfPlayers, Seconds, Number, Choice, Option, Menu, Admin;
string AdminUsername, AdminPassword;
char Answer[30];
bool PickedQuestions[30] = {false};



void Timer() { // Timer for Questions
	Seconds = 5;
	for (int i= 0; i<30; i++) {
		cout << Seconds << " ";
        if (Seconds == 0) {
        	break;
        }
        sleep(1);
        Seconds--;
    }
}

bool Picked(int number){ // Picked Number
	return PickedQuestions[number - 1];
}

void MarkPicked(int number){ // Mark the Picked Number
	PickedQuestions[number - 1] = true;
}

void ResetPickedQuestions(){ // For Reset, If All the Number is already Picked or If they Cancel the Quiz
	for(int i = 0; i < 30; i++){
		PickedQuestions[1] = false;
	}
}

void DisplayTurn(string PlayerName){ // To know which Player will Pick
	cout << "\t\t\t\t\t\t     Player " << PlayerName<< "'s turn." << endl;
}

void savetofile(){
 ofstream outFile("E:\\playerInfoFile.txt");
    if (!outFile) {
        cerr << "Failed to open player info file for writing!" << endl;
        return;
    }

    // Write player information to the file
    outFile << "Game " << GameCounter << ":\n";
    outFile << NumberOfPlayers << " PLAYERS" << endl;
    int counter = 0;
    for (int i = 1; i <= NumberOfPlayers; ++i) {
    	counter++;
        outFile <<"Player"<< counter<<": " << PlayerNames[i] << endl;
    }
    outFile.close();
	}

// txt file
void PlayerInfo() { // For Number of Players and their Names
	system("CLS");
	while(true){
		cout << "\t\t\t\t\t\t+------------------------------+" << endl;
		cout << "\t\t\t\t\t+------------------------------+" << endl;
		cout << "\t\t\t\t\t		PLAYERS " << endl;
		cout << "\t\t\t\t\t\t+------------------------------+" << endl;
		cout << "\t\t\t\t\t+------------------------------+" << endl;
		cout << "\n\n";
		cout << "\t\t\t\t\t\t   How many players? ";
		cout << endl;
		cout << "\t\t\t\t\t\t\t- ";
		cin >> NumberOfPlayers;
		cout << "\n\n\n";

		if(NumberOfPlayers >= 2 && NumberOfPlayers <= 5){
			for(int i = 1; i <= NumberOfPlayers; i++){
				cout << "\t\t\t\t\t    Enter name for player " << i << ": ";
				cin >> PlayerNames[i];
				Player player;
				player.name = PlayerNames[i];
				playerData.insert({PlayerNames[i],player});
			}

			break;
		}
		else{
			system("CLS");
			cout << "\n\t\t\t\t\t\t    2-5 Players only..." << endl;
			cout << "\n\n";
			continue;
		}


	system("pause");
}
}
void Openfile() {
	ifstream inFile("E:\\playerInfoFile.txt", ios::app);
    if (!inFile) {
        cerr << "Failed to open player info file for reading!" << endl;
        return;
    }

    // Read player information from the file
    inFile >> NumberOfPlayers;
    for (int i = 1; i <= NumberOfPlayers; ++i) {
        inFile >> PlayerNames[i];
    }
    inFile.close();
}

void DisplayPlayerInfo(){ //Display the Player Information for Admin View
	system("CLS");

	cout << "\t\t\t\t\t\t+------------------------------+" << endl;
	cout << "\t\t\t\t\t+------------------------------+" << endl;
	cout << "\t\t\t\t\t		PLAYERS " << endl;
	cout << "\t\t\t\t\t\t+------------------------------+" << endl;
	cout << "\t\t\t\t\t+------------------------------+" << endl;
	cout << "\n\n";

	for(int i = 0; i < NumberOfPlayers; i++) {
		if(NumberOfPlayers != 0){
			cout << "\t\t\t\t\tPLAYER "<< i + 1 << "\t\t"<< PlayerNames[i + 1] << endl;
		}
	}
	system("pause");
}


void QuizGame(int CurrentPlayer) { // Quiz 30 numbers with 30 questions to be picked by the players
	GameCounter++;
	while(true){
		string CurrentPlayerName = PlayerNames[CurrentPlayer];
		system("CLS");
		cout << "\t\t\t\t\t\t  +----------------------------------------+" << endl;
		cout << "\t\t\t\t  +----------------------------------------+" << endl;
		cout << "\t\t\t\t\t\t	PICK A NUMBER " << endl;
		cout << "\t\t\t\t\t\t  +----------------------------------------+" << endl;
		cout << "\t\t\t\t  +----------------------------------------+" << endl;
		cout << "\n\n";

		cout << "\t\t    [-----------------------------------------------------------------------------------]" << endl;
		DisplayTurn(CurrentPlayerName);
		cout << "\t\t    [-----------------------------------------------------------------------------------]" << endl;
		cout << "\t\t    [	 1	 2	 3	 4	 5	 6	 7	 8	 9	10	]" << endl;
		cout << "\t\t    [	11	12	13	14	15	16	17	18	19	20	]" << endl;
		cout << "\t\t    [	21	22	23	24	25	26	27	28	29	30	]" << endl;
		cout << "\t\t    [-----------------------------------------------------------------------------------]" << endl;
		cout << "\t\t    [				Pick [31] to cancel the quiz				]" << endl;
		cout << "\t\t    [-----------------------------------------------------------------------------------]" << endl;
		cout << "\n\n";

		cout << "\t\t\t\t\t\t\tPick a number: ";
		cout <<"\n";
		cout << "\t\t\t\t\t\t\t  - ";
		cin >> Number;
        if(Number == 31){

            system("CLS");
            saveRecord();

            main();

        }
		if (Picked(Number)){
			cout << "\n\n";
			cout << "\t\t\t\tNumber is already picked. Please choose another number." << endl;
			system("pause");
			continue;
		}
		MarkPicked(Number);

		switch(Number) {

			case 1:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\t[" << Number << "]    " << questions[0] << endl;
                cout << "\n\t\t\t\t\tTIMER: ";
                Timer();

                system("CLS");
                cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[0];

				if (Answer[0] == UpperCaseAnswer[Number - 1] || Answer[0] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;


				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(0,CurrentPlayerName,questions[0],UpperCaseAnswer[Number - 1],Answer[0]);
				break;
			case 2:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t[" << Number << "]    " << questions[1] << endl;
                cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[1];

				if (Answer[1] == UpperCaseAnswer[Number - 1] || Answer[1] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else{
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(1,CurrentPlayerName,questions[1],UpperCaseAnswer[Number - 1],Answer[1]);
				break;
			case 3:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t   [" << Number << "]    " << questions[2] << endl;
                cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[2];

				if (Answer[2] == UpperCaseAnswer[Number - 1] || Answer[2] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(2,CurrentPlayerName,questions[2],UpperCaseAnswer[Number - 1],Answer[2]);
				break;
			case 4:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\t[" << Number << "]    " << questions[3] << endl;
                cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[3];

				if (Answer[3] == UpperCaseAnswer[Number - 1] || Answer[3] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
					playerData[CurrentPlayerName].score++;
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(3,CurrentPlayerName,questions[3],UpperCaseAnswer[Number - 1],Answer[3]);
				break;
			case 5:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t[" << Number << "]    " << questions[4] << endl;
                cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[4];

				if (Answer[4] == UpperCaseAnswer[Number - 1] || Answer[4] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(4,CurrentPlayerName,questions[4],UpperCaseAnswer[Number - 1],Answer[4]);
				break;
			case 6:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t[" << Number << "]	" << questions[5] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[5];

				if (Answer[5] == UpperCaseAnswer[Number - 1] || Answer[5] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(5,CurrentPlayerName,questions[5],UpperCaseAnswer[Number - 1],Answer[5]);
				break;
			case 7:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t[" << Number << "]	" << questions[6] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[6];

				if (Answer[6] == UpperCaseAnswer[Number - 1] || Answer[6] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(6,CurrentPlayerName,questions[6],UpperCaseAnswer[Number - 1],Answer[6]);
				break;
			case 8:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t[" << Number << "]	" <<  questions[7] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[7];

				if (Answer[7] == UpperCaseAnswer[Number - 1] || Answer[7] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(7,CurrentPlayerName,questions[7],UpperCaseAnswer[Number - 1],Answer[7]);
				break;
			case 9:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t[" << Number << "]	" << questions[8] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[8];

				if (Answer[8] == UpperCaseAnswer[Number - 1] || Answer[8] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(8,CurrentPlayerName,questions[8],UpperCaseAnswer[Number - 1],Answer[8]);
				break;
			case 10:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\t[" << Number << "]	" << questions[9] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[9];

				if (Answer[9] == UpperCaseAnswer[Number - 1] || Answer[9] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(9,CurrentPlayerName,questions[9],UpperCaseAnswer[Number - 1],Answer[9]);
				break;
			case 11:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t     [" << Number << "]    " << questions[10] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[10];

				if (Answer[10] == UpperCaseAnswer[Number - 1] || Answer[10] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(10,CurrentPlayerName,questions[10],UpperCaseAnswer[Number - 1],Answer[10]);
				break;
			case 12:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t[" << Number << "]	" << questions[11] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[11];

				if (Answer[11] == UpperCaseAnswer[Number - 1] || Answer[11] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(11,CurrentPlayerName,questions[11],UpperCaseAnswer[Number - 1],Answer[11]);
				break;
			case 13:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t[" << Number << "]	" << questions[12] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[12];

				if (Answer[12] == UpperCaseAnswer[Number - 1] || Answer[12] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(12,CurrentPlayerName,questions[12],UpperCaseAnswer[Number - 1],Answer[12]);
				break;
			case 14:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t[" << Number << "]	" << questions[13] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[13];

				if (Answer[13] == UpperCaseAnswer[Number - 1] || Answer[13] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					HardScores[CurrentPlayer - 1]+= 3;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(13,CurrentPlayerName,questions[13],UpperCaseAnswer[Number - 1],Answer[13]);
				break;
			case 15:
				system("CLS");
				cout << "\n\n";
				cout << "  [" << Number << "]	" << questions[14] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[14];

				if (Answer[14] == UpperCaseAnswer[Number - 1] || Answer[14] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(14,CurrentPlayerName,questions[14],UpperCaseAnswer[Number - 1],Answer[14]);
				break;
			case 16:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t[" << Number << "]	" << questions[15] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[15];

				if (Answer[15] == UpperCaseAnswer[Number - 1] || Answer[15] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(15,CurrentPlayerName,questions[15],UpperCaseAnswer[Number - 1],Answer[15]);
				break;
			case 17:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t[" << Number << "]	" << questions[16] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[16];

				if (Answer[16] == UpperCaseAnswer[Number - 1] || Answer[16] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					EasyScores[CurrentPlayer - 1]+= 1;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(16,CurrentPlayerName,questions[16],UpperCaseAnswer[Number - 1],Answer[16]);
				break;
			case 18:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\t     [" << Number << "]	" << questions[17] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[17];

				if (Answer[17] == UpperCaseAnswer[Number - 1] || Answer[17] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					HardScores[CurrentPlayer - 1]+= 3;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(17,CurrentPlayerName,questions[17],UpperCaseAnswer[Number - 1],Answer[17]);
				break;
			case 19:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\t [" << Number << "]	" << questions[18] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[18];

				if (Answer[18] == UpperCaseAnswer[Number - 1] || Answer[18] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					HardScores[CurrentPlayer - 1]+= 3;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(18,CurrentPlayerName,questions[18],UpperCaseAnswer[Number - 1],Answer[18]);
				break;
			case 20:
				system("CLS");
				cout << "\n\n";
				cout << "[" << Number << "]	" << questions[19] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[19];

				if (Answer[19] == UpperCaseAnswer[Number - 1] || Answer[19] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(19,CurrentPlayerName,questions[19],UpperCaseAnswer[Number - 1],Answer[19]);
				break;
			case 21:
				system("CLS");
				cout << "\n\n";
				cout << "\t[" << Number << "]	" << questions[20] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[20];

				if (Answer[20] == UpperCaseAnswer[Number - 1] || Answer[20] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(20,CurrentPlayerName,questions[20],UpperCaseAnswer[Number - 1],Answer[20]);
				break;
			case 22:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t[" << Number << "]	" << questions[21] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[21];

				if (Answer[21] == UpperCaseAnswer[Number - 1] || Answer[21] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					HardScores[CurrentPlayer - 1]+= 3;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(21,CurrentPlayerName,questions[21],UpperCaseAnswer[Number - 1],Answer[21]);
				break;
			case 23:
				system("CLS");
				cout << "\n\n";
				cout << "\t[" << Number << "]	" << questions[22] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[22];

				if (Answer[22] == UpperCaseAnswer[Number - 1] || Answer[22] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(22,CurrentPlayerName,questions[22],UpperCaseAnswer[Number - 1],Answer[22]);
				break;
			case 24:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t [" << Number << "]	" << questions[23] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[23];

				if (Answer[23] == UpperCaseAnswer[Number - 1] || Answer[23] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(23,CurrentPlayerName,questions[23],UpperCaseAnswer[Number - 1],Answer[23]);
				break;
			case 25:
				system("CLS");
				cout << "\n\n";
				cout << "[" << Number << "]	" << questions[24] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[24];

				if (Answer[24] == UpperCaseAnswer[Number - 1] || Answer[24] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(24,CurrentPlayerName,questions[24],UpperCaseAnswer[Number - 1],Answer[24]);
				break;
			case 26:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t[" << Number << "]	" << questions[25] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[25];

				if (Answer[25] == UpperCaseAnswer[Number - 1] || Answer[25] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(25,CurrentPlayerName,questions[25],UpperCaseAnswer[Number - 1],Answer[25]);
				break;
			case 27:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\t[" << Number << "]	" << questions[26] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[26];

				if (Answer[26] == UpperCaseAnswer[Number - 1] || Answer[26] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					HardScores[CurrentPlayer - 1]+= 3;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(26,CurrentPlayerName,questions[26],UpperCaseAnswer[Number - 1],Answer[26]);
				break;
			case 28:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t  [" << Number << "]	" << questions[27] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[27];

				if (Answer[27] == UpperCaseAnswer[Number - 1] || Answer[27] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(27,CurrentPlayerName,questions[27],UpperCaseAnswer[Number - 1],Answer[27]);
				break;
			case 29:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t [" << Number << "]	" << questions[28] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[28];

				if (Answer[28] == UpperCaseAnswer[Number - 1] || Answer[28] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(28,CurrentPlayerName,questions[28],UpperCaseAnswer[Number - 1],Answer[28]);
				break;
			case 30:
				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t[" << Number << "]	" << questions[29] << endl;
				cout << "\n\t\t\t\t\tTIMER: ";
				Timer();

				system("CLS");
				cout << "\n\n";
				cout << "\t\t\t\t\tEnter your answer (A, B, C, or D): ";
				cin >> Answer[29];

				if (Answer[29] == UpperCaseAnswer[Number - 1] || Answer[29] == LowerCaseAnswer[Number - 1]) {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tCorrect answer!\t\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					playerData[CurrentPlayerName].score++;
					system("pause");
					AverageScores[CurrentPlayer - 1]+= 2;
				} else {
					cout << "\n\n\n";
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					cout << "\t\t\t\t	|\tIncorrect answer!\t|" << endl;
					cout << "\t\t\t\t   +-----------------------------------------+" << endl;
					system("pause");
				}
				save_for_review(29,CurrentPlayerName,questions[29],UpperCaseAnswer[Number - 1],Answer[29]);
				break;
			case  31:
			    saveRecord();
				return;
				break;
			default:
				cout << "Invalid choice. Please try again..." << endl;
				sleep(1);
				break;
		}
		playerData[CurrentPlayerName].answered++;
		CurrentPlayer = (CurrentPlayer % NumberOfPlayers) + 1;
	}

}

void DisplayAnsweredQuetions(){ // Display Answered Questions, Player Answer, If Correct or Incorrect(Admin View and for the Player to Review their Answer)
	system("CLS");
	cout << "\n\n\n";
	cout << "\t\t\t\t\t+--------------------------------------------------+" << endl;
    cout << "\t\t\t\t+--------------------------------------------------+" << endl;
    cout << "\t\t\t\t\t	ANSWERED QUESTIONS AND RESULTS" << endl;
    cout << "\t\t\t\t\t+--------------------------------------------------+" << endl;
    cout << "\t\t\t\t+--------------------------------------------------+" << endl;
    cout << "\n\n";

    for(int i = 0; i < 30; i++){
    	if(PickedQuestions[i]){
	    	for(ReviewQuestion review: reviewList){
                if(review.index == i){
                    cout << "Question " << (i + 1) << ": " << endl;
                    cout << reviewList[i].question << endl;
                    cout << "\t\t\t\t\t"+reviewList[i].name+"'s Answer: " << reviewList[i].pAnswer << endl;
                    cout << "\t\t\t\t\tCorrect Answer: " << reviewList[i].cAnswer;
                    cout << endl;
                }
	    	}
	    }
	}
	system("pause");
}

//txt file kasama ng leaderboard
void DisplayScores(){ // Scores Based on Level of Difficulty
	system("CLS");
	cout << "\t\t\t\t\t\t+---------------------------+" << endl;
	cout << "\t\t\t\t\t+---------------------------+" << endl;
	cout << "\t\t\t\t\t\t\tSCORE " << endl;
	cout << "\t\t\t\t\t\t+---------------------------+" << endl;
	cout << "\t\t\t\t\t+---------------------------+" << endl;
	cout << "\n\n";

	for(int i = 0; i < NumberOfPlayers; i++) {
		TotalScores[i] = EasyScores[i] + AverageScores[i] + HardScores[i];
	    cout << "\tPlayer " << i + 1 << "- " << PlayerNames[i + 1] << ": ";
		cout << "\t" << "EASY: " << EasyScores[i] << "\t\t" << " AVERAGE: " << AverageScores[i] << "\t\t" << " HARD: " << HardScores[i] << "\t\t" << "TOTAL POINTS: " << TotalScores[i] << endl;
	}
	cout << endl;
	system("pause");
}

//txt file
void Leaderboard() { // Leaderboard, Show Score, and Winner
    int MaxScore = -1;
    int WinnerIndex = -1;

    system("CLS");
    cout << "\t\t\t\t\t\t  +----------------------------------------+" << endl;
    cout << "\t\t\t\t  +----------------------------------------+" << endl;
    cout << "\t\t\t\t\t\t\t  LEADERBOARD" << endl;
    cout << "\t\t\t\t\t\t  +----------------------------------------+" << endl;
    cout << "\t\t\t\t  +----------------------------------------+" << endl;
    cout << "\n\n";

    int playerScores[NumberOfPlayers];
    int playerIndices[NumberOfPlayers];
    for (int i = 0; i < NumberOfPlayers; i++) {
        int totalScore = EasyScores[i] + AverageScores[i] + HardScores[i];
        playerScores[i] = totalScore;
        playerIndices[i] = i;
    }
    for (int i = 0; i < NumberOfPlayers - 1; i++) {
        for (int j = i + 1; j < NumberOfPlayers; j++) {
            if (playerScores[i] < playerScores[j]) {
                swap(playerScores[i], playerScores[j]);
                swap(playerIndices[i], playerIndices[j]);
            }
        }
    }
    for (int i = 0; i < NumberOfPlayers; i++) {
        int playerIndex = playerIndices[i];
        cout << "\t\t\t\t\tPlayer " << i + 1 << " - " << PlayerNames[playerIndex + 1] << ":    " << playerScores[i] << endl;
    }
    if (NumberOfPlayers > 0) {
        MaxScore = playerScores[0];
        WinnerIndex = playerIndices[0];
    }
    cout << endl;
    system("pause");
    if (WinnerIndex != -1) {
        system("CLS");
        cout << "\t\t\t\t\t\t+---------------------------+" << endl;
        cout << "\t\t\t\t\t+---------------------------+" << endl;
        cout << "\t\t\t\t\t\t\tWINNER " << endl;
        cout << "\t\t\t\t\t\t+---------------------------+" << endl;
        cout << "\t\t\t\t\t+---------------------------+" << endl;
        cout << "\n\n";

        cout << "\t\t\t\t\t   Player " << WinnerIndex + 1 << " - " << PlayerNames[WinnerIndex + 1] << " with score of " << MaxScore << endl;

        cout << "\n\n";
        cout << "\t\t\t\t\t\t   CONGRATULATIONS!!!" << endl;
    } else {
        cout << "\t\t\t\t\t\t\t No winner yet." << endl;
    }
    system("pause");
}



int main() {
	Openfile();
	while(true){
		// Main Menu
		cout << "\t\t\t\t\t\t+------------------------------+" << endl;
		cout << "\t\t\t\t\t+------------------------------+" << endl;
		cout << "\t\t\t\t\t		WELCOME " << endl;
		cout << "\t\t\t\t\t\t+------------------------------+" << endl;
		cout << "\t\t\t\t\t+------------------------------+" << endl;
		cout << "\n\n\n";

		cout << "\t\t\t\t\t\t\t[1] PLAYER\t" << endl;
		cout << "\t\t\t\t\t\t\t[2] ADMIN\t" << endl;
		cout << "\t\t\t\t\t\t\t[3] EXIT\t" << endl;
		cout << endl;
		cout << "\t\t\t\t\t\t\t- ";
		cin >> Menu;

		if (Menu == 1) { // PLAYER MENU OR VIEW
            while (1) {
                system("CLS");
                cout << "\t\t\t\t\t+--------------------------------------------------+" << endl;
                cout << "\t\t\t\t+--------------------------------------------------+" << endl;
                cout << "\t\t\t\t\t	PICK A NUMBER AND, THEN ANSWER " << endl;
                cout << "\t\t\t\t\t+--------------------------------------------------+" << endl;
                cout << "\t\t\t\t+--------------------------------------------------+" << endl;
                cout << "\n\n\n";

                cout << "\t\t\t\t\t\t  [1] QUIZ GAME" << endl;
                cout << "\t\t\t\t\t\t  [2] REVIEW QUESTIONS" << endl;
                cout << "\t\t\t\t\t\t  [3] LEADERBOARD" << endl;
                cout << "\t\t\t\t\t\t  [4] BACK TO MAIN MENU" << endl;
                cout << endl;
                cout << "\t\t\t\t\t\t\t- ";
                cin >> Choice;

                switch (Choice) {
                    case 1: // QUIZ GAME
                        PlayerInfo();
                		savetofile();
                        system("CLS");
                        cout << "\t\t\t\t\t+--------------------------------------------------+" << endl;
                        cout << "\t\t\t\t+--------------------------------------------------+" << endl;
                        cout << "\t\t\t\t\t\t	GAME MECHANICS " << endl;
                        cout << "\t\t\t\t\t+--------------------------------------------------+" << endl;
                        cout << "\t\t\t\t+--------------------------------------------------+" << endl;
                        cout << "\n\n";
                        cout << "\t\t\t[1]	Player will pick a number that consist of random question" << "\n" << endl;
                        cout << "\t\t\t[2]	Every questions has 5 seconds timer." << "\n" << endl;
                        cout << "\t\t\t[3]	If a number is already answered, the next player can't pick it again." << "\n" << endl;
                        cout << "\t\t\t[4]	The player can review their answer after the game." << "\n" << endl;
                        system("pause");

                        system("CLS");
                        cout << "\n\n\n";

                        cout << "\t\t\t\t\t\t\t[1] START" << endl;
                        cout << "\t\t\t\t\t\t\t[2] CANCEL" << endl;
                        cout << "\n\n\n";

                        cout << "\t\t\t\t\tPress 1 to Start the quiz or 2 to Cancel: " << endl;
                        cout << "\t\t\t\t\t\t\t- ";
                        cin >> Option;

                        if (Option == 1) { // START
                            ResetPickedQuestions();
                            QuizGame(CurrentPlayer);

                        } else if (Option == 2) { // CANCEL
                            system("CLS");
                            cout << "QUIZ CANCELLED!" << endl;
                            break;
                        } else {
                            system("CLS");
                            cout << "INVALID INPUT!" << endl;
                            sleep(1);
                            break;
                            system("pause");
                        }

                        break;
                    case 2: // REVIEW QUESTIONS
                    	//txt file
                        DisplayAnsweredQuetions();
                        break;
                    case 3: // LEADERBOARD
                    	// txt file
                        DisplayScores();
                        Leaderboard();
                        break;
                    case 4:
                        break;

                    default:
                        system("CLS");
                        cout << "Invalid choice. Please try again..." << endl;
                        sleep(1);
                        break;
                }
                if (Choice == 4) {
                    system("CLS");
                    break;
                }
            }
        }
		else if(Menu == 2){ // ADMIN MENU OR VIEW
			system("CLS");
			cout << "\t\t\t\t\t\t+------------------------------+" << endl;
			cout << "\t\t\t\t\t+------------------------------+" << endl;
			cout << "\t\t\t\t\t		ADMIN " << endl;
			cout << "\t\t\t\t\t\t+------------------------------+" << endl;
			cout << "\t\t\t\t\t+------------------------------+" << endl;
			cout << "\n\n\n";

			cout << "\t\t\t\t\t\tUSERNAME: ";
			cin >> AdminUsername;
			cout << endl;
			cout << "\t\t\t\t\t\tPASSWORD: ";
			cin >> AdminPassword;

			if(AdminUsername == "admin" && AdminPassword == "admin1234"){
				while(1){
					system("CLS");
					cout << "\n\n";
					cout << "\t\t\t\t\t\t[1] View Players" << endl;
					cout << "\t\t\t\t\t\t[2] Leaderboard" << endl;
					cout << "\t\t\t\t\t\t[3] Back to Main Menu" << endl;
					cout << endl;
					cout << "\t\t\t\t\t\t	- ";
					cin >> Admin;

					switch(Admin){
						case 1: // VIEW PLAYERS INFORMATION
							DisplayPlayerInfo(); //txt file
							break;
						case 2: // LEADERBOARD
							// txt file
							DisplayScores();
							Leaderboard();
							break;
						case 3: // BACK TO MENU
							break;
						default:
							system("CLS");
							cout << "\n\n\n\n\n";
							cout << "\t\t\t\t\t  Invalid choice. Please try again..." << endl;
							sleep(2);
							break;
					}
					if(Admin == 3){
						system("CLS");
						break;
					}
				}
			}
			else if(AdminUsername != "admin" && AdminPassword == "admin1234"){ // Admin UserName and Password Validation(Wrong UserName)
				system("CLS");
				cout << "\n\n\n\n\n";
				cout << "\t\t\t\t\t\t  INVALID USERNAME!" << endl;
				sleep(1);
				system("CLS");
			}
			else if(AdminUsername == "admin" && AdminPassword != "admin1234"){ // Admin UserName and Password Validation(Wrong Password)
				system("CLS");
				cout << "\n\n\n\n\n";
				cout << "\t\t\t\t\t\t  INVALID PASSWORD!" << endl;
				sleep(1);
				system("CLS");
			}
			else{ // Admin UserName and Password Validation(Wrong UserName and Password)
				system("CLS");
				cout << "\n\n\n\n\n";
				cout << "\t\t\t\t\t  INVALID USERNAME AND PASSWORD!" << endl;
				sleep(1);
				system("CLS");

			}
		}
		else if(Menu == 3){ // Exit Code
			return 0;
		}
		else{
			system("CLS");
			cout << "\n\n\n\n\n";
			cout << "\t\t\t\t\t  Invalid choice. Please try again..." << endl;
			sleep(2);
			system("CLS");
			continue;
		}
	}
	return 0;
}
