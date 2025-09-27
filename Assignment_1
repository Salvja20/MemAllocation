#include <iostream>
#include <vector>
#include <cstdlib>
#include <ctime>
#include <cmath>
#include <iomanip>

using namespace std;


const int TOTAL_PAGES = 100;
const int PAGE_SIZE_MB = 160;
const int PROCESS_UNIT_MB = 80;
const int START_ADDRESS = 2000;

struct Process {
    int processId;
    int startAddress;
    int sizeMB;
    int pagesAllocated;
    int unusedMemory;
};


int getRandom(int min, int max) {
    return rand() % (max - min + 1) + min;
}


void userMemoryAllocation() {
    vector<int> memory(TOTAL_PAGES, -1);
    vector<Process> processes;

    int currentAddress = START_ADDRESS;
    int processId = 1;
    int pagesLeft = TOTAL_PAGES;

    srand(time(0));

    while (true) {
        int randomPageUnits = getRandom(1, 30);
        int processSizeMB = randomPageUnits * PROCESS_UNIT_MB;

        int pagesRequired = ceil((double)processSizeMB / PAGE_SIZE_MB);

        if (pagesRequired > pagesLeft) {
            break; 
        }

       
        int pagesAllocated = 0;
        for (int i = 0; i < TOTAL_PAGES && pagesAllocated < pagesRequired; ++i) {
            if (memory[i] == -1) {
                memory[i] = processId;
                pagesAllocated++;
            }
        }

        int totalAllocatedMB = pagesRequired * PAGE_SIZE_MB;
        int unused = totalAllocatedMB - processSizeMB;

        Process p = {
            processId,
            currentAddress,
            processSizeMB,
            pagesRequired,
            unused
        };

        processes.push_back(p);

        
        currentAddress += totalAllocatedMB;
        pagesLeft -= pagesRequired;
        processId++;
    }

    
    cout << "\nSummary Report:\n";
    cout << left << setw(15) << "Process Id"
         << setw(30) << "Starting Memory Address"
         << setw(30) << "Size of the Process MB"
         << setw(25) << "Unused Space MB" << "\n";

    for (const auto& p : processes) {
        cout << left << setw(15) << p.processId
             << setw(30) << p.startAddress
             << setw(30) << p.sizeMB
             << setw(25) << p.unusedMemory << "\n";
    }

    cout << "\nTotal processes allocated: " << processes.size() << endl;
    cout << "Memory pages remaining: " << pagesLeft << endl;
}

int main() {
    userMemoryAllocation();
    return 0;
}
