# Movie Script Analysis using Hadoop MapReduce

## Project Overview
The goal of this project is to use Hadoop MapReduce to process the dialogue data in order to assess a movie script. Its three primary goals are:
1. **Character-specific Most Frequently Used Words**
2. **Analysis of Dialogue Length**
3. **Character-Specific Words**

In order to efficiently process vast amounts of script data and produce insights on the most often used terms by characters, the length of their dialogues, and the uniqueness of the words they employ, the analysis is carried out utilizing Hadoop's MapReduce architecture.

## Approach and Implementation
### Mapper and Reducer Logic

#### Task 1: Most Frequent Words by Character
- **Mapper**: 
  - Divides the dialogue into words, reads each line from the input file, and then outputs the word and character name.
- **Reducer**: 
  - Counts the number of times each word appears for a particular character after grouping words by character.

#### Task 2: Dialogue Length Analysis
- **Mapper**: 
  - Counts the amount of words in a certain character's dialogue after reading each line..
- **Reducer**: 
  - Determines the overall length of each character's dialogue by adding together all of their words.

#### Task 3: Unique Words by Character
- **Mapper**: 
  - Emits distinct words for every character and tokenizes every conversation.
- **Reducer**: 
  - Combines distinct words for every character.
 
### Execution Steps
1. **Set up Hadoop and Docker containers**:
   - Run Hadoop in Docker containers (namenode, datanode, resourcemanager, etc.).
   - Ensure HDFS is properly configured and running.

2. **Compile the Java Project**:
   - Run `mvn clean package` to compile the project and generate the JAR file.
   
3. **Load the Input File into HDFS**:
   - Copy the script file (e.g., `movie_dialogues.txt`) into HDFS using the following command:
     ```bash
     hdfs dfs -put /movie_dialogues.txt /user/hadoop/movie_script/
     ```

4. **Run the MapReduce Job**:
   - Execute the Hadoop MapReduce job with the following command:
     ```bash
     hadoop jar /hands-on2-movie-script-analysis-1.0-SNAPSHOT.jar com.movie.script.analysis.MovieScriptAnalysis /user/hadoop/movie_script/movie_dialogues.txt /user/hadoop/output
     ```

5. **Retrieve Output from HDFS**:
   - Use the following command to get the output from HDFS:
     ```bash
     hdfs dfs -get /user/hadoop/output/task1 /local/directory
     ```

6. **View the Results**:
   - After executing the above commands, view the result files in the output directories (`task1`, `task2`, `task3`).


### Challenges Faced & Solutions
- **Challenge 1**: File transfers from the local computer to the Hadoop container are challenging.
  - **Solution**: After copying the necessary files from the local file system to the container using the `docker cp` command, we loaded them into HDFS.
  
- **Challenge 2**: Inconsistent outcomes while attempting to access the output.
  - **Solution**: During the `hdfs dfs -get` operation, we made sure the output folders were properly formed in HDFS and that the right file paths were used.
 
### Sample Input and Output

### Input Data

Below are the quotes from the *Harry Potter* series, organized by character:

```text
Hagrid: I can teach you how to bottle fame, brew glory, even put a stopper in death.
Sirius: The boy who lived, come to die.
Voldemort: Turn to page 394.
Draco: It is our choices, Harry, that show what we truly are, far more than our abilities.
Voldemort: You have your mother's eyes.
Hagrid: It does not do to dwell on dreams and forget to live.
Ron: We could all have been killed - or worse, expelled.
```

### OutPut Data

Draco_a	13
Draco_abilities	4
Draco_act	3
Draco_after	1
Draco_aims	1
Draco_all	15
Draco_always	3
Draco_am	3
Draco_and	31
...
 







