# Quest-2
#include <iostream>
#include <cstdlib> // for rand() and srand()
#include <ctime>   // for time()

using namespace std;

int main() {
    
    cout << "Welcome to the Truth or Lie Labyrinth Game!" << endl;
    cout << "Find your way by asking the sentinels questions. Some always tell the truth, others always lie." << endl;
    cout << "You need to correclty identify truth or lie from 3 sentinels to win." << endl;
    
    const int numSentinels = 5; // Number of sentinels in the labyrinth
    bool sentinelRoles[numSentinels]; // Array to store roles (true for truthful, false for liar)

    // Seed the random number generator
    srand(time(nullptr));

    // Randomly assign roles to sentinels
    for (int i = 0; i < numSentinels; ++i) {
        // Generate a random number (0 or 1)
        // If it's 0, the sentinel is a liar; if it's 1, the sentinel is a truth teller
        sentinelRoles[i] = rand() % 2 == 0; 
    }

    // Display roles of sentinels
    cout << "Sentinel Roles:" << endl;
    for (int i = 0; i < numSentinels; ++i) {
        cout << "Sentinel " << i + 1 << ": " << (sentinelRoles[i] ? "truth teller" : "liar") << endl;
    }

    return 0;
}

