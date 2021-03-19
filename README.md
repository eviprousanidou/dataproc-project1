# Large Scale Data Processing: Project 1
## Evi Prousanidou


## Bitcoin mining with Spark
The key to mining Bitcoin is to solve a puzzle involving the SHA-256 hash function, where SHA stands for "security hash algorithm" and 256 denotes the output of the hash function as having 256 bits (or, equivalently, a 64-digit hexadecimal number). Given a Bitcoin header string `S`, the puzzle is to find a positive integer `x` (called "nonce") such that the concatenation `xS` is hashed to a hexadecimal number with `k` leading zeros. The parameter `k` is known as the difficulty of the puzzle. The actual Bitcoin difficulty is currently 11. [Here](https://emn178.github.io/online-tools/sha256.html) is a working exhibit of an SHA-256 calculator.  

Let's look at an example of the mining process to clarify. Say we hash the string `this_is_a_bitcoin_block` with the SHA-256 function, which produces `5de97c4b0b4fd55c033fb1de4723de24b8fea9c6caa09af43008e0412ee2847a`. Now, we set the nonce to 20 and prepend it to the string, giving us `20this_is_a_bitcoin_block`. The new string hashes to `0c6de9a1e7a6b958dfe13c7383d9a5d3029a702691dfe689adec21b06676710b`, thus solving the puzzle for `k = 1`. Subsequently, a value of 457 for the nonce solves the puzzle for `k = 2` since `457this_is_a_bitcoin_block` hashes to `004306ef8f43e38fb17bce7cb96e568ed904e334dafb3cd69568a27ac564e08c`.  

Your mission is to run **project_1** with Spark to determine the nonce for varying difficulties of `k` with one of the following st

## Reporting your findings
You'll be submitting a report along with your code that provides commentary on the tasks below.  

1. **(4 points)** Run the program on your local machine to solve cases `k = 2,3,4,5,6`. For each `k`, provide `xS`, its hash value, the total time elapsed, and the number of trials.   
Use this_is_a_bitcoin_block_of_68058055
***For k = 2***
(40969771456792this_is_a_bitcoin_block_of_68058055,007b9f67c4d919904bd01d2e224d99a5ddb06dcfbbf0178f7ae1ffd61acba492)
Time elapsed:2s
Number of trials: 100


3. **(3 points)** Run the program on GCP to solve the case `k = 7`. Provide `xS`, its hash value, the total time elapsed, and the number of trials. Describe your cluster's configuration (number of machines, number/type of cores, etc.) and your process for estimating the number of trials needed in order to find the nonce.  
4. **(3 points)** Modify **one** line of code in **src/main/scala/project_1/main.scala** so that the program generates the potential nonce from 1 to `n` (the number of trials) instead of randomly. Discuss whether or not this is more efficient than the randomized approach.

