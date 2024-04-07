#include <iostream>
#include <algorithm>        // for transform
#include <string>
#include <cctype>           // for tolower
#include <cstdlib>
#include <ctime>
#include <vector>
#include <cctype>
#include <chrono>

using namespace std;
using namespace std::chrono;

int main() {
    const int numSentinels = 5; // Number of sentinels in the labyrinth
    bool sentinelRoles[numSentinels];  // Array to store roles (true for truthful, false for liar)
    int num_questions_right = 0;
    int num_questions_wrong = 0;
    int questions_asked = 0;
    int answers_recieved = 0;
    int answers_to_win = 3;
    
    vector<string> questionsList = {
        "What is Syeda's favorite color?", 
        "How many siblings does Asmita have?",
        "What is Natalia's favorite vacation spot?", 
        "What is Amarda's favorite show?",
        "What pet animal has Hamsini always wanted?", 
        "What is Nabila scared of?",
        "What is Gloria's favorite hobby?", 
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
    
    auto start = chrono::high_resolution_clock::now();

    // Main game loop
    while (true) {
        cout << "\nThere are paths with sentinels. Choose a sentinel to question (1-" << numSentinels << "): ";
        int sentinel_choice;
        //cin >> sentinel_choice;
        if (!(cin >> sentinel_choice)) {
            cout << "Invalid input. Please enter a number." << endl;
            cin.clear();            // Clear the error state
            cin.ignore(100, '\n');  // Discard invalid input
            continue;               // Restart the loop
        }


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
                    cout << "The sentinel responds: 2" << endl;
                } else if (randomIndex == 2) {
                    cout << "The sentinel responds: Poland" << endl;
                } else if (randomIndex == 3) {
                    cout << "The sentinel responds: Outer Banks" << endl;
                } else if (randomIndex == 4) {
                    cout << "The sentinel responds: Turtle" << endl;
                } else if (randomIndex == 5) {
                    cout << "The sentinel responds: Heights" << endl;
                } else if (randomIndex == 6) {
                    cout << "The sentinel responds: Reading" << endl;
                } else if (randomIndex == 7) {
                    cout << "The sentinel responds: The Florida Project" << endl;
                }
            } else { // If the sentinel is a liar
                // Liar responses
                if (randomIndex == 0) {
                    cout << "The sentinel responds: Purple" << endl;
                } else if (randomIndex == 1) {
                    cout << "The sentinel responds: 3" << endl;
                } else if (randomIndex == 2) {
                    cout << "The sentinel responds: Italy" << endl;
                } else if (randomIndex == 3) {
                    cout << "The sentinel responds: Surviving Summer" << endl;
                } else if (randomIndex == 4) {
                    cout << "The sentinel responds: Dog" << endl;
                } else if (randomIndex == 5) {
                    cout << "The sentinel responds: Spiders" << endl;
                } else if (randomIndex == 6) {
                    cout << "The sentinel responds: Playing Badminton" << endl;
                } else if (randomIndex == 7) {
                    cout << "The sentinel responds: Pulp Fiction" << endl;
                }
            }

            while (true) {
                cout << "Do you think the sentinel is telling the truth? (Yes/No): ";
                string answer;
                cin >> answer;
                transform(answer.begin(), answer.end(), answer.begin(), ::tolower);

                if (answer == "yes" || answer == "no") {
                    // Check if the player's detection of the sentinel's truthfulness is correct
                    if ((sentinelRoles[sentinel_choice - 1] && answer == "yes") || (!sentinelRoles[sentinel_choice - 1] && answer == "no")) {
                        cout << "You detected the truth/lies correctly!" << endl;
                        num_questions_right += 1;
                        answers_to_win -= 1;
                        cout << "Only " << answers_to_win << " more to go!" << endl;
                    } else {
                        cout << "Wrong detection! Try again." << endl;
                        num_questions_wrong += 1;
                        cout << "You still have " << answers_to_win << " more to go!" << endl;
                    }
                    questions_asked += 1;
                    answers_recieved += 1;
                    break; // Exit the loop if a valid answer is provided
                } else {
                    cout << "Invalid answer, type in 'yes' or 'no.'" << endl;
                }
            }
        } else {
            cout << "Invalid sentinel choice. Choose a sentinel from 1 to " << numSentinels << "." << endl;
        }

        if (answers_to_win == 0)  {
            
            auto end = chrono::high_resolution_clock::now();
            auto duration = chrono::duration_cast<chrono::seconds>(end - start);
            int minutes = duration.count() / 60;
            int seconds = duration.count() % 60;
            
            cout << "Congratulations you won!" << endl;
            cout << "Number of right answers: " << num_questions_right << endl;
            cout << "Number of wrong answers: " << num_questions_wrong << endl;
            cout << "Number of questions asked: " << questions_asked << endl;
            cout << "Number of answers received: " << answers_recieved << endl;
            cout << "Time taken: " << minutes << " minutes and " << seconds << " seconds" << endl;
            break;
        }
    }

    return 0;
}
