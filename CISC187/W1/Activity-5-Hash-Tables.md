# Activity 5: Hash Tables

## Hash Table Code:

```C++
#include <vector>
#include <list>
#include <string>
#include <iostream>
#include <iomanip>

using namespace std;

class HashTable {
private:
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;

    int HashTable::hashFunction(const string& key) const {
    const int prime = 31;
    long long hash = 0;

    for (char c : key) {
        hash = (hash * prime + c) % capacity;
    }

    return (int)(hash % capacity);
}

void rehash() {
    int oldCapacity = capacity;
    vector<list<pair<string, int>>> oldTable = table;

    capacity *= 2;
    table.assign(capacity, list<pair<string, int>>());
    currentSize = 0;
    collisionCount = 0;

    for (int i = 0; i < oldCapacity; ++i) {
            for (auto& entry : oldTable[i]) {
                insert(entry.first, entry.second);
            }
        }
    }

public:
    HashTable(int size = 11) : currentSize(0), capacity(size), collisionCount(0) {
        table.resize(capacity);
    }

    void insert(const string& key, int value) {
        if (loadFactor() > 0.75) {
            rehash();
        }

        int index = hashFunction(key);
        
        for (auto& entry : table[index]) {
            if (entry.first == key) {
                entry.second = value;
                return;
            }
        }
    if (!table[index].empty()) {
            collisionCount++;
        }

        table[index].push_back({key, value});
        currentSize++;
    }

    bool remove(const string& key) {
        int index = hashFunction(key);
        auto& bucket = table[index];
        
        for (auto it = bucket.begin(); it != bucket.end(); ++it) {
            if (it->first == key) {
                if (bucket.size() > 1) {
                    collisionCount--;
                }
                bucket.erase(it);
                currentSize--;
                return true;
            }
        }
        return false;
    }

    int search(const string& key) const {
        int index = hashFunction(key);
        for (const auto& entry : table[index]) {
            if (entry.first == key) {
                return entry.second;
            }
        }
        return -1;
    }

    double loadFactor() const {
        return (double)currentSize / capacity;
    }

    int size() const {
        return currentSize;
    }
    bool isEmpty() const {
        return currentSize == 0;
    }
    void printTable() const {
        for (int i = 0; i < capacity; ++i) {
            cout << "Bucket " << i << ": ";
            for (const auto& entry : table[i]) {
                cout << "[" << entry.first << ": " << entry.second << "] -> ";
            }
            cout << "NULL" << endl;
        }
    }
};

int main() {
    HashTable ht(11);
    
    // 100 Common Words for testing
    vector<string> words = {
        "book", "drum", "stick", "practice", "linear", "algebra", "in", "that", "have", "it",
        "for", "not", "on", "with", "he", "as", "you", "do", "kiwi", "this",
        "but", "his", "by", "from", "they", "we", "say", "her", "she", "or",
        "woman", "computer", "my", "one", "all", "would", "dog", "their", "what", "so",
        "up", "out", "if", "about", "who", "get", "which", "go", "me", "food",
        "make", "can", "like", "time", "no", "just", "him", "know", "take", "person",
        "into", "year", "your", "good", "some", "could", "them", "see", "other", "than",
        "then", "cat", "look", "only", "come", "its", "over", "think", "man", "back",
        "banana", "use", "two", "how", "our", "work", "boss", "well", "way", "even",
        "new", "want", "because", "any", "these", "give", "day", "most", "us", "is"
    };

    // 1. Insert 100 words
    for (int i = 0; i < words.size(); ++i) {
        ht.insert(words[i], i + 1);
    }

    // 2. Print Stats
    cout << "--- Hash Table Stats ---" << endl;
    cout << "Capacity:         " << ht.getCapacity() << endl;
    cout << "Number of Items:  " << ht.size() << endl;
    cout << "Load Factor:      " << fixed << setprecision(2) << ht.loadFactor() << endl;
    cout << "Total Collisions: " << ht.getCollisions() << endl << endl;

    // 3. Search existing and non-existing keys
    cout << "--- Search Verification ---" << endl;
    string key1 = "because";
    string key2 = "cpp_rocks";
    cout << "Search '" << key1 << "': " << (ht.search(key1) != -1 ? "Found (Value: " + to_string(ht.search(key1)) + ")" : "Not Found") << endl;
    cout << "Search '" << key2 << "': " << (ht.search(key2) != -1 ? "Found" : "Not Found") << endl << endl;

    // 4. Remove keys and verify
    cout << "--- Removal Verification ---" << endl;
    cout << "Removing 'because'..." << endl;
    ht.remove("because");
    cout << "Search 'because' again: " << (ht.search("because") != -1 ? "Found" : "Not Found") << endl;
    cout << "New Size: " << ht.size() << endl;

    return 0;
}
```
## Written Response and Observation:

The polynomial rolling hash seems to work well on all three types of inputs, this must be due to the fact that it looks at both the character itself and where it is in the string. In the Sequential and Same Prefix tests, the strings are almost identical, just changing at the very end. The multiplier helps make sure that even a tiny change in the input makes a completely different hash value. This stops similar strings from clustering together, which is a problem with simpler methods like just adding up the character values. The result is that the average bucket length stays short and everything is spread out evenly. 

Even though I recorded a lot of collisions in total, the biggest bucket size is still tiny (usually less than 5). This means the collisions are spread out nicely across the whole table instead of piling up in one spot. When I experimented using the same prefix test, even with keys that start exactly the same for a long time, the function avoids slowing down much, keeping the average lookup time consistently fast. 
