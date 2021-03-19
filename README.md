# Large Scale Data Processing: Project 1
## Evi Prousanidou


## Bitcoin mining with Spark
The key to mining Bitcoin is to solve a puzzle involving the SHA-256 hash function, where SHA stands for "security hash algorithm" and 256 denotes the output of the hash function as having 256 bits (or, equivalently, a 64-digit hexadecimal number). Given a Bitcoin header string `S`, the puzzle is to find a positive integer `x` (called "nonce") such that the concatenation `xS` is hashed to a hexadecimal number with `k` leading zeros. The parameter `k` is known as the difficulty of the puzzle. The actual Bitcoin difficulty is currently 11. [Here](https://emn178.github.io/online-tools/sha256.html) is a working exhibit of an SHA-256 calculator.  

Let's look at an example of the mining process to clarify. Say we hash the string `this_is_a_bitcoin_block` with the SHA-256 function, which produces `5de97c4b0b4fd55c033fb1de4723de24b8fea9c6caa09af43008e0412ee2847a`. Now, we set the nonce to 20 and prepend it to the string, giving us `20this_is_a_bitcoin_block`. The new string hashes to `0c6de9a1e7a6b958dfe13c7383d9a5d3029a702691dfe689adec21b06676710b`, thus solving the puzzle for `k = 1`. Subsequently, a value of 457 for the nonce solves the puzzle for `k = 2` since `457this_is_a_bitcoin_block` hashes to `004306ef8f43e38fb17bce7cb96e568ed904e334dafb3cd69568a27ac564e08c`.  

Your mission is to run **project_1** with Spark to determine the nonce for varying difficulties of `k` with one of the following st

## Reporting your findings
You'll be submitting a report along with your code that provides commentary on the tasks below.  

1. **(4 points)** Run the program on your local machine to solve cases `k = 2,3,4,5,6`. For each `k`, provide `xS`, its hash value, the total time elapsed, and the number of trials.     
   Used: this_is_a_bitcoin_block_of_68058055

    **For k = 2**
    (444218325this_is_a_bitcoin_block_of_68058055,001aa7d88932cee91fc824dddcdbfb1b447e3a485ee9490d8129d992b4fd51ec)
    Time elapsed:2s
    Number of trials: 100
    
    **For k = 3**
    ((1949709656this_is_a_bitcoin_block_of_68058055,000cf34a0cfcb846be3dfc0c7ae32218190a70373aaaf53825779c7af584f4d1)
    Time elapsed:2s
    Number of trials: 5000
    
    **For k = 4**
    (1939771623this_is_a_bitcoin_block_of_68058055,000028acfbb9426812c309a52ef6ea4856fdac5f92cd420c89f42e8619a701e2)
    Time elapsed:4s
    Number of trials: 50000
    
    **For k = 5**
    (1388693602this_is_a_bitcoin_block_of_68058055,00000e0f94304f1030bb3091c7453460860509643882485b9a75b9e47b815f60)
    Time elapsed:9s
    Number of trials: 500000
    
    **For k = 6**
    (559798106this_is_a_bitcoin_block_of_68058055,0000004e05aa46627851589832fb8c50b7833fcd5060e7ad2da025273179af98)
    Time elapsed:138s
    Number of trials: 10000000


3. **(3 points)** Run the program on GCP to solve the case `k = 7`. Provide `xS`, its hash value, the total time elapsed, and the number of trials. Describe your cluster's configuration (number of machines, number/type of cores, etc.) and your process for estimating the number of trials needed in order to find the nonce
   
    Cluster Configuration:
      1 master
      2 workers
      
    (1194565486this_is_a_bitcoin_block_of_68058055,000000078a99564794d99593c04c4df268c3bf7773a6f021d51374d2edcad026)
    Time elapsed:705s
    Number of trials: 500000000


5. **(3 points)** Modify **one** line of code in **src/main/scala/project_1/main.scala** so that the program generates the potential nonce from 1 to `n` (the number of trials) instead of randomly. Discuss whether or not this is more efficient than the randomized approach.

   line 58 should change:
   
      iter.map(x => rand.nextInt(Int.MaxValue - 1) + 1)
    
    be replaced by:
    
      iter.map(x => rand.nextInt(trials) + 1)
      
      
    By changing the program to generate the potential nonce from 1 to n instead of randomly, this would not be significantly affect the efficiency but it would make     it a little more efficient.
      
      
    


    


