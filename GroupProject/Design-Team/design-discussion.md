### Design 1 (bevans60)
* +Many methods that allow for more granularity
* -Architecture not entirely flushed out
* -Doesn't seem like there's a logical way for a Student to add/delete quizzes

### Design 2 (crobins8)
* +Simplistic design which makes it easy to extend as needed, and easy to understand
* +Utility classes for Date object
* -Unclear how QuizStatistic objects are stored
* -Ambiguous necessarily how a Student might take quizzes not created by that Student

### Design 3 (ewu41)
* +Very modular, which would allow for more flexibility should anything need to change later
* +Includes the "has a" and "is a" relationships, as well as specific number constraints on those relationships (e.g. 1 to many)
* -A bit complicated, and makes it difficult to read -- a little over-constrained
* -Some items are represented as objects, but they relate more to functionality (e.g. Remove, Add)

### Design 4 (rdymock3)
* +Actually used an enumeration for seniority level
* +QuizEvent object makes it very straightforward to take a Quiz, and also stores statistics for that Quiz
* -"Has a" relationships are not included

### Team Design

![alt text](Group%20Project%20D1%20-%20Updated.jpg)

For our design, we decided to branch off of Ryan's because we thought that it represented the described system and fulfilled the requirements in the most accurate and efficient manner. The Application is the main part of the design, and that essentially represents the controller that holds together the entire system. From there, a Student has the ability to login, add/remove a Quiz, practice a Quiz, and get various Quiz statistics. Some of us had something similar in our designs, but we felt that Ryan's design portrayed it the most efficiently, given the requirements. All of us had a Student class, and that was largely the same across the board. We also all had a Quiz class, which again was largely the same across the board. After that however, our designs started to diverge as we got into the more complicated business logic of the system.

Ryan created the idea of a QuizEvent, which is similar to Ben's idea of a QuizManager or Ethan's idea of a Practice, which aggregated a number of QuestionEvents, which hold whether or not the answer to a given Question was correct. This QuizEvent effectively allowed a Student to practice a Quiz, and it also kept statistics about that practice session. All of us had something somewhat similar in our respective designs, but we felt that Ryan's was the best design, as it did not overcomplicate things, it broke things out in a modular and flexible manner, and we thought it would be easy to maintain as well. Overall, this final design had pieces of all of our designs in it, but we felt that it would be best to branch off of Ryan's design since we thought it fulfilled the requirements more than the other three. 

>The quiz score statistics for a student S should list all quizzes, whether they were played by S or not, and including the quizzes created by S.

Comments:  I changed the name of one of the Application methods to getQuizScoresByStudent and changed it to return a Map instead of a list.  This would be the same structure as the quizHistory, but filtered to only include the Student’s Quiz Events.  Quizzes the Student has not yet played will be contained in the Map, their value being an empty array. 

>The quizzes not played by S can be displayed in any order (after the ones played).

Comments:  We could solve this by making the Map a TreeMap and then sorting the Map by number of QuizEvents.  This way, all the quizzes not played would be at the end.  


>For quizzes not played by S, only the names of the first three students to score 100% on the quiz should be displayed.

Comments:  Since each quiz object holds a Set of Student objects that obtained the three first 100% scores, this is already addressed.  


>The names displayed (and used to sort) in the statistics for the first three students to score 100% on the quiz can be either their usernames or their real names.

Comments:Since each quiz object holds a Set of Student objects that obtained the three first 100% scores, this is already addressed.  


>Every word in a quiz should be shown once and only once.

Comments:  This logic can handled in the getNextQuestion method in the QuizEvent class.  I changed the method generateQuestion in the Quiz class to allow for passing a Word to allow for this.   


>Incorrect definitions, conversely, may repeat.

Comments:  This assumption is already built in and is handled in the dynamic creation of new questions in the generateQuestion method.  


>General clarification: all relevant data (scores, statistics, quizzes, student logins) should persist between uses of the application.

Comments: Since this is an android device, we may want to persist the data in an SQLite database.  This can be accomplished using Room, which is an abstraction layer over an SQLite database.  This can be easily implemented using the classes we have defined. 


### Summary

Our group's UML Design experience is limited so being able to see each other individual designs and discuss them together was an important learning experience. Review/critique of our individual designs revealed that various requirements stated in the Requirements Document were not captured by the UML Diagram. Additionally, we found that over complicated designs can prove to be 1) difficult to read and 2) possibly over-constrained. As a group we gravitated towards designs that satisfied all the goals from the Requirements Document and were simple. We felt it was important not to weigh down designs with too much complexity. Over-constrained designs can potentially be hard to work with whereas simpler designs can be expanded upon if necessary. For these reasons, we decided as a group to build off Ryan's UML Diagram, which accomplished all the necessary goals without the unnecessary complexity.

From a teamwork perspective, it was especially important for this first deliverable that we were all present with our designs ready to share. Open, friendly dialogue was essential to have efficient and productive discussion. In the end, we learned from seeing each other's UML diagrams and hearing the thought process behind implementation. 
