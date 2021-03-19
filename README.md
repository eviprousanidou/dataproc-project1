# Large Scale Data Processing: Project 1
## Evi Prousanidou


7. To execute the project's **.jar** file, you'll need to upload it somewhere accessible to the cluster. This can be accomplished by creating a [GCP storage bucket](https://console.cloud.google.com/storage). Name it `bcusername-csci3390-bucket`, e.g. `smith-csci3390-bucket`. Leave the rest of the settings on their default.  
8. Upload the **.jar** file located in **target/scala-2.12** in your project directory.  
9. Back in the **Dataproc** console, select the **Submit Job** button on the **Jobs** page.  
10. Submit a job with the following configuration:  
  a. Select the cluster you created for **Cluster**.  
  b. `Spark` job type.  
  c. `project_1.main` for the main class.  
  d. `gs://your-bucket-name/project_1_2.12-1.0.jar` for the **.jar** file.  
  e. A value of 1 for maximum restarts per hour.  
11. Upon successful execution, you should see `Usage: project_1 string difficulty #trials` as the job output. Cheers to successfully configuring your cloud environment.

## Bitcoin mining with Spark
The key to mining Bitcoin is to solve a puzzle involving the SHA-256 hash function, where SHA stands for "security hash algorithm" and 256 denotes the output of the hash function as having 256 bits (or, equivalently, a 64-digit hexadecimal number). Given a Bitcoin header string `S`, the puzzle is to find a positive integer `x` (called "nonce") such that the concatenation `xS` is hashed to a hexadecimal number with `k` leading zeros. The parameter `k` is known as the difficulty of the puzzle. The actual Bitcoin difficulty is currently 11. [Here](https://emn178.github.io/online-tools/sha256.html) is a working exhibit of an SHA-256 calculator.  

Let's look at an example of the mining process to clarify. Say we hash the string `this_is_a_bitcoin_block` with the SHA-256 function, which produces `5de97c4b0b4fd55c033fb1de4723de24b8fea9c6caa09af43008e0412ee2847a`. Now, we set the nonce to 20 and prepend it to the string, giving us `20this_is_a_bitcoin_block`. The new string hashes to `0c6de9a1e7a6b958dfe13c7383d9a5d3029a702691dfe689adec21b06676710b`, thus solving the puzzle for `k = 1`. Subsequently, a value of 457 for the nonce solves the puzzle for `k = 2` since `457this_is_a_bitcoin_block` hashes to `004306ef8f43e38fb17bce7cb96e568ed904e334dafb3cd69568a27ac564e08c`.  

Your mission (and yes, you have to accept it) is to run **project_1** with Spark to determine the nonce for varying difficulties of `k` with one of the following strings:
```
// If you're working in a pair
this_is_a_bitcoin_block_of_yourEagleId1_and_yourEagleId2

// If you're working alone
this_is_a_bitcoin_block_of_yourEagleId
```

The program accepts three parameters: the header string `S`, the difficulty `k`, and the number of trials `n`. For each trial, it will generate a random number between 1 and 2<sup>32</sup>-1 for the nonce `x` and hash `xS`. The program distributes the `n` trials evenly among the compute nodes and executes them in parallel. If a valid nonce is found for difficulty `k`, `xS` as well as its hash value will be outputted.  

Pass in the arguments by appending them to the `spark-submit` command you ran earlier. For example:
```
// Linux
spark-submit --class project_1.main --master local[*] target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_12345678 2 100

// Unix
spark-submit --class "project_1.main" --master "local[*]" target/scala-2.12/project_1_2.12-1.0.jar this_is_a_bitcoin_block_of_12345678 2 100
```
In GCP, simply include the arguments in the **Arguments** field of the job you're submitting.  

## Reporting your findings
You'll be submitting a report along with your code that provides commentary on the tasks below.  

1. **(4 points)** Run the program on your local machine to solve cases `k = 2,3,4,5,6`. For each `k`, provide `xS`, its hash value, the total time elapsed, and the number of trials.  
2. **(3 points)** Run the program on GCP to solve the case `k = 7`. Provide `xS`, its hash value, the total time elapsed, and the number of trials. Describe your cluster's configuration (number of machines, number/type of cores, etc.) and your process for estimating the number of trials needed in order to find the nonce.  
3. **(3 points)** Modify **one** line of code in **src/main/scala/project_1/main.scala** so that the program generates the potential nonce from 1 to `n` (the number of trials) instead of randomly. Discuss whether or not this is more efficient than the randomized approach.

## Submission via GitHub
Delete your project's current **README.md** file (the one you're reading right now) and include your report as a new **README.md** file in the project root directory. Have no fear—the README with the project description is always available for reading in the template repository you created your repository from. For more information on READMEs, feel free to visit [this page](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/about-readmes) in the GitHub Docs. You'll be writing in [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown). Be sure that your repository is up to date and you have pushed all changes you've made to the project's code. When you're ready to submit, simply provide the link to your repository in the Canvas assignment's submission.

## You must do the following to receive full credit
1. Create your report in the ``README.md`` and push it to your repo
2. In the report you must include your full name and your partner's full name, in addition to collaborators
3. Submit a link to your repo on the canvas assignment

## Late Submission Penalties
Beginning with the minute after the deadline, your submission will be docked a full letter grade (10%) for every 
day that it is late. For example, if the assignment is due at 11:59 PM EST on Friday and you submit at 3:00 AM EST on Sunday,
then you will be docked 20% and the max you could receive on that assignment is an 80%. 
Late penalties are calculated from the last commit in the git log.
**If you make a commit 48 hours after the deadline, you will receive a 0 -- Please do not do this, it messes up our grading.**
