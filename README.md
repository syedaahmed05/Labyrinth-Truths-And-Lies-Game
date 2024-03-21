#include <iostream>
#include <algorithm> //for transform
#include <string>
#include <cctype> // for tolower()

using namespace std;

int main() {
    const int numSentinels = 5; // Number of sentinels in the labyrinth
    bool sentinelRoles[numSentinels]; // Array to store roles (true for truthful, false for liar)
    int number_of_questions_asked = 0; //counts how many questions user asked.
    int number_right = 0; //counts how many questions the user got right. (User needs 3 right answers to win).
    
    cout << "Welcome to the Truth or Lie Labyrinth Game!" << endl;
    cout << "Find your way by asking the sentinels questions. Some always tell the truth, others always lie." << endl;
    cout << "You need to correclty identify truth or lie from 3 sentinels to win." << endl;

    // Initialize sentinel roles (you can do this randomly as before)
    for (int i = 0; i < numSentinels; ++i) {
        // For demonstration purposes, let's assume alternate sentinels are truthful
        sentinelRoles[i] = (i % 2 == 0);
    }

    // Main game loop
    while (true) {
        cout << "There are paths with sentinels. Choose a sentinel to question (1-" << numSentinels << "): ";
        int sentinel_choice;
        cin >> sentinel_choice;

        if (sentinel_choice >= 1 && sentinel_choice <= numSentinels) {
            cin.ignore(); // Ignore newline character from previous input
            
            string question;
            cout << "You ask the sentinel: ";
            getline(cin, question);

            cout << "The sentinel responds: ";

            // Convert the question to lowercase for case-insensitive comparison
            transform(question.begin(), question.end(), question.begin(), ::tolower);

            // Respond based on the sentinel's role and the question asked
            if (sentinelRoles[sentinel_choice - 1]) { // Truth teller
                // Example response logic: Assume the sentinel always tells the truth
                cout << "Ford";
                
                
            } else { // Liar
                // Example response logic: Assume the sentinel always lies
                cout << "Toyota";
            }

            cout << "\nDo you think the sentinel is telling the truth? (Yes/No): ";
            string answer;
            cin >> answer;
            transform(answer.begin(), answer.end(), answer.begin(), ::tolower);

            // Check if the player's detection of the sentinel's truthfulness is correct
            if ((sentinelRoles[sentinel_choice - 1] && answer == "yes") || (!sentinelRoles[sentinel_choice - 1] && answer == "no")) {
                cout << "Wrong detection! Try again." << endl;
            } else {
                cout << "You detected the truth/lies correctly!" << endl;
            }
        } else {
            cout << "Invalid sentinel choice. Choose a sentinel from 1 to " << numSentinels << "." << endl;
        }
    }

    return 0;
}
