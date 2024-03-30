#include <iostream>
#include <algorithm>        // for transform
#include <string>
#include <cctype>           // for tolower
#include <cstdlib>
#include <ctime>
#include <vector>
#include <cctype>

using namespace std;

int main() {
    const int numSentinels = 5; // Number of sentinels in the labyrinth
    bool sentinelRoles[numSentinels];  // Array to store roles (true for truthful, false for liar)
    vector<string> questionsList = {
        "What is Syeda's favorite color?", 
        "How old is Asmita?",
        "How many siblings does Natalia have?", 
        "What is Amarda's favorite subject?",
        "What pet animal has Hamsini always wanted?", 
        "What is Nabila majoring in?",
        "How many credits did Gloria take this semester?", 
        "What is Manar's favorite movie?" 
    };

    cout << "Welcome to the Truth or Lie Labyrinth Game!" << endl;
    cout << "Find your way by asking the sentinels questions. Some always tell the truth, others always lie." << endl;
    cout << "You need to correctly identify truth or lie from 3 sentinels to win." << endl;

    // Seed the random number generator
    srand(time(nullptr));

    // Initialize sentinel roles randomly
    for (int i = 0; i < numSentinels; ++i) {
        // Randomly assign truth teller or liar role
        sentinelRoles[i] = rand() % 2 == 0;
    }

    // Main game loop
    while (true) {
        cout << "\nThere are paths with sentinels. Choose a sentinel to question (1-" << numSentinels << "): ";
        int sentinel_choice;
        cin >> sentinel_choice;

        if (sentinel_choice >= 1 && sentinel_choice <= numSentinels) {
            cin.ignore();       // Ignore newline character from previous input
            
            int randomIndex = rand() % questionsList.size();   // Generate a random index for selecting a question from the list
            
            // Display the question asked to the sentinel
            cout << "You ask the sentinel: " << questionsList[randomIndex] << endl;
            
            // Check the response based on the question asked and the sentinel's role
            if (sentinelRoles[sentinel_choice - 1] == true) { // If the sentinel is a truth teller
                // Truth-teller responses
                if (randomIndex == 0) {
                    cout << "The sentinel responds: Green" << endl;
                } else if (randomIndex == 1) {
                    cout << "The sentinel responds: 18" << endl;
                } else if (randomIndex == 2) {
                    cout << "The sentinel responds: 1" << endl;
                } else if (randomIndex == 3) {
                    cout << "The sentinel responds: Math" << endl;
                } else if (randomIndex == 4) {
                    cout << "The sentinel responds: Turtle" << endl;
                } else if (randomIndex == 5) {
                    cout << "The sentinel responds: IT" << endl;
                } else if (randomIndex == 6) {
                    cout << "The sentinel responds: 15" << endl;
                } else if (randomIndex == 7) {
                    cout << "The sentinel responds: The Florida Project" << endl;
                }
            } else { // If the sentinel is a liar
                // Liar responses
                if (randomIndex == 0) {
                    cout << "The sentinel responds: Purple" << endl;
                } else if (randomIndex == 1) {
                    cout << "The sentinel responds: 19" << endl;
                } else if (randomIndex == 2) {
                    cout << "The sentinel responds: 2" << endl;
                } else if (randomIndex == 3) {
                    cout << "The sentinel responds: Science" << endl;
                } else if (randomIndex == 4) {
                    cout << "The sentinel responds: Dog" << endl;
                } else if (randomIndex == 5) {
                    cout << "The sentinel responds: Science" << endl;
                } else if (randomIndex == 6) {
                    cout << "The sentinel responds: 13" << endl;
                } else if (randomIndex == 7) {
                    cout << "The sentinel responds: Pulp Fiction" << endl;
                }
            }

            cout << "Do you think the sentinel is telling the truth? (Yes/No): ";
            string answer;
            cin >> answer;
            transform(answer.begin(), answer.end(), answer.begin(), ::tolower);
            
            if (answer == "yes" || answer == "no") {
                // Check if the player's detection of the sentinel's truthfulness is correct
                if ((sentinelRoles[sentinel_choice - 1] && answer == "yes") || (!sentinelRoles[sentinel_choice - 1] && answer == "no")) {
                    cout << "You detected the truth/lies correctly!" << endl;
                } else {
                    cout << "Wrong detection! Try again." << endl;
                }
            } else {
                cout << "Invalid answer, type in 'yes' or 'no.'" << endl;
            }
        } else {
            cout << "Invalid sentinel choice. Choose a sentinel from 1 to " << numSentinels << "." << endl;
        }
    }

    return 0;
}
