# Project
## Task 1
#### Sports players analyzer optimized
To keep a time complexity performance of just O(N+M), I opted to use a hash set(unordered_set), which is a specialized type of hash table that not only stores unique elements but also checks for their existence. I used a "struct" data type for "player" to be able to group the player's associated variables (first name, last name, sport). I then defined the "find_multi_sport_players" function that accepts the basketball players array and football players array and returns an array of mutual players. Here is where the hash set basketball_set is created and filled with the data from the basketball_players array. The data in this set is then compared to the data in the football_players array, so only one hash set is required. When a match is found, the name is saved to the mutual_players array. To avoid overheads and data copying, I passed vectors by reference (<Player>&, const auto&). Inserting the basketball_players array's elements into the hash set takes O(N) (with N being the size of the first array) and then comparing the values takes O(M) (with M being the size of the second array) since hash searches take O(1). This leads to a time complexity of O(N+M)

```C++

#include <iostream>
#include <vector>
#include <string>
#include <unordered_set>

// sructure to represent a player
struct Player {
    std::string first_name;
    std::string last_name;
    std::string team;
};

// function to take both arrays and compare values
std::vector<std::string> find_multi_sport_players(const std::vector<Player>& basketball, const std::vector<Player>& football) {
    std::unordered_set<std::string> basketball_set;
    std::vector<std::string> mutual_players;

    for (const auto& player : basketball) {
        std::string full_name = player.first_name + " " + player.last_name;
        basketball_set.insert(full_name);
    }

    for (const auto& player : football) {
        std::string full_name = player.first_name + " " + player.last_name;

        if (basketball_set.find(full_name) != basketball_set.end()) {
            mutual_players.push_back(full_name);
        }
    }

    return mutual_players;
}

int main() {
    std::vector<Player> basketball_players = {
        {"Jill", "Huang", "Gators"},
        {"Janko", "Barton", "Sharks"},
        {"Wanda", "Vakulskas", "Sharks"},
        {"Jill", "Moloney", "Gators"},
        {"Luuk", "Watkins", "Gators"}
    };

    std::vector<Player> football_players = {
        {"Hanzla", "Radosti", "32ers"},
        {"Tina", "Watkins", "Barleycorns"},
        {"Alex", "Patel", "32ers"},
        {"Jill", "Huang", "Barleycorns"},
        {"Wanda", "Vakulskas", "Barleycorns"}
    };

    // calling the function on the 2 arrays, saving the result to "result"
    std::vector<std::string> result = find_dual_sport_players(basketball_players, football_players);

    //print the result
    std::cout << "Players who play in both sports:\n";
    for (const auto& name : result) {
        std::cout << "- " << name << "\n";
    }

    return 0;
}

```

## Task 2
#### Find the missing number optimized
According to Gauss's summation, the total sum of all integers from 0 to n should be (n*(n+1))/2. Using this formula, I created a function that takes an array of integers, finds its size (finding the size of the array will give us the exact value to use for "n"), and then finds what its sum should be using the formula. The function then finds the actual sum of the numbers in the array using "std::accumulate" and subtracts it from what the sum should actually be, and the resulting difference is the missing number in the sequence. The calculation is a quick O(1) process and the array need only be iterated through once resulting in a time complexity of O(N).

```C++

#include <vector>
#include <numeric>

int find_missing_number(const std::vector<int>& nums) {
    int n = numbers.size();
    
    // Gauss's Summation (expected sum of numbers from 0 to n)
    int expected_sum = (n * (n + 1)) / 2;
    
    // The actual sum of numbers in the array
    int actual_sum = std::accumulate(nums.begin(), nums.end(), 0);
    
    // The difference is the missing number
    return expected_sum - actual_sum;
}

```

## Task 3
#### Greatest profit stocks calculator optimized
To avoid using nested loops, I used a linear tracking loop that keeps track of minimum and maximum prices using "std::min" and "std::max." Historical lows are saved and overwrited in min_price, and potential_profit calculates and stores the theoretical profit margins ((today's)price - min_price). To store and update the maximum profit seen so far, max_profit and potential_profit are passed to std::max and the result is saved to max_profit. This program performs with O(N) time complexity since it only has to iterate through the data once.

```C++

#include <vector>
#include <algorithm>
#include <iostream>

int calc_greatest_profit(const std::vector<int>& prices) {
    if (prices.empty()) return 0;

    int min_price = prices[0];
    int max_profit = 0;

    for (int price : prices) {
        // Update the lowest purchase price found so far
        min_price = std::min(min_price, price);
        
        // What the potential profit would be at current price
        int potential_profit = price - min_price;
        
        // Update the greatest profit seen so far
        max_profit = std::max(max_profit, potential_profit);
    }

    return max_profit;
}

int main() {
    std::vector<int> predicted_prices = {10, 7, 5, 8, 11, 2, 6};
    std::cout << "Greatest Profit: $" << calc_greatest_profit(predicted_prices) << std::endl;
    return 0;
}

```

## Task 4
#### Greatest product finder optimized
The following code only iterates through the array a singular time keeping the time complexity at just O(N) and stores 4 variables, the 2 greatest values found and the 2 lowest values found. The "max" variables are initialized to the lowest possible value allowed (INT_MIN) and the "min" variables are initalized to the highest possible value allowed (INT_MAX). This ensures the variables are correctly updated when the program loops through the data. It then calculates the products of the 2 greatest values and of the 2 lowest values and compares them using std::max. The greatest of the two products is then returned. "Long long" datatypes are used to prevent possible overflow. Try-catch protective block included in "main()" for possible runtime error exceptions.

```C++

#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

long long find_greatest_product(const std::vector<int>& nums) {
    // In case array has fewer than 2 elements
    if (nums.size() < 2) {
        throw std::invalid_argument("Array must contain at least two numbers.");
    }

    // Initialize the variables
    int max1 = INT_MIN, max2 = INT_MIN;
    int min1 = INT_MAX, min2 = INT_MAX;

    for (int num : nums) {
        // Update the two largest values
        if (num > max1) {
            max2 = max1;
            max1 = num;
        } else if (num > max2) {
            max2 = num;
        }

        // Update the two smallest values
        if (num < min1) {
            min2 = min1;
            min1 = num;
        } else if (num < min2) {
            min2 = num;
        }
    }

    // Type casting the products to long long to prevent overflow
    long long product1 = static_cast<long long>(max1) * max2;
    long long product2 = static_cast<long long>(min1) * min2;

    return std::max(product1, product2);
}

int main() {
    std::vector<int> example = {5, -10, -6, 9, 4};
    
    try {
        std::cout << "Maximum product: " << find_greatest_product(example) << std::endl;
    } catch (const std::exception& e) {
        std::cerr << e.what() << std::endl;
    }
    
    return 0;
}

```

## Task 5
#### Body temperature readings sorter optimized
Since the readings are from 97.0 to 99.0 incrementing by .1, there are only a total of 21 possible readings. This fixed range makes it ideal for use in a counting sort, which requires integer indices. To handle this, each temperature reading can be converted to an integer index using the formula index = (temperature - 97.0) * 10. This formula is then later reversed to get back the original value, temperature = 97.0 + (index / 10). This counting sort algorithm counts the frequencies that each specific integer index is seen and stores it in a new array (count). Since the original array is passed by reference (&), it is modified directly without taking a copy. The original array is then rebuilt by looping through our counter array which holds the frequencies for each index. The counter array is in itself always "sorted" since its indices are in order from smallest to highest (0-21). When rebuilding the array, the indices are converted back using the reversed formula and since the counter array also contains frequencies duplicates are handled correctly. In the end, the algorithm performs with O(N+K) time frequency or just O(N) since K is constant in this case (21).

```C++
#include <iostream>
#include <vector>
#include <cmath>

void sort_temperatures(std::vector<double>& temps) {
    // 21 possible values from 97.0 to 99.0 incrementing by 0.1
    const int RANGE_SIZE = 21; 
    std::vector<int> count(RANGE_SIZE, 0);

    // Count the frequency of each temperature
    for (double t : temps) {
        int index = std::round((t - 97.0) * 10.0);
        count[index]++;
    }

    // Overwrite the original array in sorted order
    int target_index = 0;
    for (int i = 0; i < RANGE_SIZE; i++) {
        while (count[i] > 0) {
            // Reverse the formula to get back the decimal value
            temps[target_index] = 97.0 + (i / 10.0);
            target_index++;
            count[i]--;
        }
    }
}

int main() {
    std::vector<double> sample = {98.6, 98.0, 97.1, 99.0, 98.9, 97.8, 98.5, 98.2, 98.0, 97.1};

    sort_temperatures(sample);

    std::cout << "Sorted temperatures:   ";
    for (double t : sample) std::cout << t << " ";
    std::cout << "\n";

    return 0;
}

```

## Task 6
#### Longest consecutive sequence finder
To optimize the function, a hash set (std::unordered_set) can be used which allows for O(1) lookups. Once the elements are inserted into the set, a number x is found such that x - 1 is not in the set. This number could signify the possible start of a consecutive series. A number x + 1 is then searched for and if that number exists we now have found a consecutive series and a counter sequence_length is incremented. This process continues until no such x + 1 is found, and is repeated for each value that does not have its respective x - 1 in the set. At the end, the longest consecutive sequence is stored using std::max (longest_consecutive_sequence = std::max(longest_consecutive_sequence, sequence_length)). Inserting N elements into the set takes O(N), and the outer loop runs N times. The inner while loop only runs for numbers that are starting points of a sequence. At most, each number is looked up once in the outer loop and possibly once again as part of a sequnce in the inner loop. This lead to a time complexity of just O(N).

```C++

#include <iostream>
#include <vector>
#include <unordered_set>
#include <algorithm>

int find_longest_consecutive_sequence(const std::vector<int>& nums) {
    // Insert all elements into a hash set
    std::unordered_set<int> num_set(nums.begin(), nums.end());
    int longest_consecutive_sequence = 0;

    for (int num : nums) {
        // Begin sequence only if appropriate number is found
        if (num_set.find(num - 1) == num_set.end()) {
            int current_num = num;
            int sequence_length = 1;

            // Count up as long as consecutive numbers exist in the set
            while (num_set.find(current_num + 1) != num_set.end()) {
                current_num += 1;
                sequence_length += 1;
            }

            // Keep track of the longest sequence
            longest_consecutive_sequence = std::max(longest_consecutive_sequence, sequence_length);
        }
    }

    return longest_consecutive_sequence;
}

int main() {
    std::vector<int> example_1 = {10, 5, 12, 3, 55, 30, 4, 11, 2};
    std::vector<int> example_2 = {19, 13, 15, 12, 18, 14, 17, 11};

    std::cout << "Longest consecutive sequence in example 1: " << find_longest_consecutive_sequence(example_1) << std::endl;
    std::cout << "Longest consecutive sequence in example 2: " << find_longest_consecutive_sequence(example_2) << std::endl;

    return 0;
}

```
