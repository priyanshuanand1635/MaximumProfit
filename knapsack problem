#include <iostream>
#include <string>
using namespace std;

struct Item {
    string name;
    int value;
    int weight;
};

void knapsack01(Item items[], int n, int capacity) {
    // Create DP table
    int dp[100][100] = {0};
    bool selected[100][100] = {false};
    
    // Build DP table
    for (int i = 1; i <= n; i++) {
        for (int w = 1; w <= capacity; w++) {
            if (items[i-1].weight <= w) {
                int include = items[i-1].value + dp[i-1][w - items[i-1].weight];
                int exclude = dp[i-1][w];
                
                if (include > exclude) {
                    dp[i][w] = include;
                    selected[i][w] = true;
                } else {
                    dp[i][w] = exclude;
                }
            } else {
                dp[i][w] = dp[i-1][w];
            }
        }
    }

    // Backtrack to find selected items
    cout << "\n=== PACKING SOLUTION ===" << endl;
    cout << "Maximum value achievable: " << dp[n][capacity] << endl;
    cout << "Selected items:" << endl;
    
    int remainingCapacity = capacity;
    int totalWeight = 0;
    int totalValue = 0;
    
    for (int i = n; i > 0 && remainingCapacity > 0; i--) {
        if (selected[i][remainingCapacity]) {
            cout << "✓ " << items[i-1].name << " (Value: " << items[i-1].value 
                 << ", Weight: " << items[i-1].weight << ")" << endl;
            totalValue += items[i-1].value;
            totalWeight += items[i-1].weight;
            remainingCapacity -= items[i-1].weight;
        }
    }
    
    cout << "Total weight used: " << totalWeight << "/" << capacity << endl;
    cout << "Remaining space: " << remainingCapacity << endl;
}

int main() {
    const int MAX_ITEMS = 10;
    Item items[MAX_ITEMS];
    int n, capacity;
    
    cout << "=== VALUABLE ITEMS PACKING HELPER ===" << endl;
    cout << "Enter knapsack capacity: ";
    cin >> capacity;
    
    cout << "Enter number of items (max " << MAX_ITEMS << "): ";
    cin >> n;
    
    if (n > MAX_ITEMS) {
        cout << "Error: Too many items!" << endl;
        return 1;
    }
    
    cout << "\nEnter item details (name, value, weight):" << endl;
    for (int i = 0; i < n; i++) {
        cout << "Item " << i+1 << ": ";
        cin >> items[i].name >> items[i].value >> items[i].weight;
    }
    
    knapsack01(items, n, capacity);
    
    return 0;
}
