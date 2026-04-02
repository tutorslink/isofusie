# Campus Survival App (Funny Edition) - Project Plan

## 1. Goal
Build a Python-based interactive application called “Campus Survival App (Funny Edition)” designed as a digital survival guide for university students. The application simulates real-life challenges (exams, attendance, cafeteria choices, group projects) to calculate a "survival score" based on user decisions.

## 2. Program Structure & Requirements
The project is modularized into three main Python files and one text file:
1. `main.py` – Main menu and user interface loop.
2. `survival_logic.py` – Core game mechanics and scenario functions.
3. `data_handler.py` – File I/O for saving and loading player scores.
4. `results.txt` – Text file to persist student survival history.

---

## 3. Pseudocode Implementation

### A. Core Logic: `survival_logic.py`
This module handles all the specific game scenarios and calculates the final scores and statuses.

```text
// survival_logic.py

FUNCTION exam_survival(current_score)
    PRINT "Scenario: It's 2 AM before the final exam."
    PRINT "1. Cram all night fueled by 5 Red Bulls."
    PRINT "2. Sleep and hope for divine intervention."
    PRINT "3. Watch 3 hours of YouTube tutorials on 'How to guess multiple choice'."
    
    INPUT choice
    
    IF choice == "1" THEN
        PRINT "Caffeine Overdose Level Unlocked! You passed, but your hands are still shaking."
        current_score = current_score + 10
    ELSE IF choice == "2" THEN
        PRINT "You chose sleep... Professor noticed you drooling on the test paper."
        current_score = current_score - 15
    ELSE IF choice == "3" THEN
        PRINT "YouTube algorithms saved you! C- is still a degree."
        current_score = current_score + 5
    ELSE
        PRINT "Invalid choice. Panic sets in, you lose 5 points."
        current_score = current_score - 5
    END IF
    
    RETURN current_score
END FUNCTION

FUNCTION cafeteria_mode(current_score)
    PRINT "Scenario: You enter the cafeteria at peak lunch hour."
    PRINT "1. Eat the mysterious 'Meat Surprise'."
    PRINT "2. Buy a $10 iced coffee and call it lunch."
    PRINT "3. Fight a freshman for the last slice of pizza."
    
    INPUT choice
    
    IF choice == "1" THEN
        PRINT "Food poisoning acquired! You lose study time."
        current_score = current_score - 10
    ELSE IF choice == "2" THEN
        PRINT "Bank account crying, but energy restored."
        current_score = current_score + 5
    ELSE IF choice == "3" THEN
        PRINT "Victory! You feast like a king."
        current_score = current_score + 15
    ELSE
        PRINT "You starved while deciding. Lose 5 points."
        current_score = current_score - 5
    END IF
    
    RETURN current_score
END FUNCTION

FUNCTION attendance_checker(current_score)
    PRINT "Scenario: It's an 8 AM lecture and it's raining."
    PRINT "1. Go to class."
    PRINT "2. Stay in bed."
    
    INPUT choice
    
    IF choice == "1" THEN
        PRINT "You arrived... but slept in the back row anyway."
        current_score = current_score + 5
    ELSE IF choice == "2" THEN
        PRINT "Surprise Quiz today! Your grade took a hit."
        current_score = current_score - 20
    ELSE
        PRINT "You got lost on campus. Lose 5 points."
        current_score = current_score - 5
    END IF
    
    RETURN current_score
END FUNCTION

FUNCTION calculate_score(points_earned, total_possible)
    // Converts raw points to a percentage
    score_percentage = (points_earned / total_possible) * 100
    RETURN score_percentage
END FUNCTION

FUNCTION generate_result_message(percentage)
    IF percentage >= 80 THEN
        RETURN "Status: Campus Legend! You survived and thrived."
    ELSE IF percentage >= 50 THEN
        RETURN "Status: Survived but emotionally unstable."
    ELSE
        RETURN "Status: Academic Probation... better luck next semester."
    END IF
END FUNCTION
```

### B. Data Storage: `data_handler.py`
This module manages saving and loading from `results.txt`.

```text
// data_handler.py

FUNCTION save_result(student_name, score_percentage, status_message)
    OPEN "results.txt" in APPEND mode AS file
    
    WRITE to file: "Student: " + student_name
    WRITE to file: "Score: " + score_percentage + "%"
    WRITE to file: "Status: " + status_message
    WRITE to file: "---------------------------------"
    
    CLOSE file
    PRINT "Your survival record has been saved to the archives."
END FUNCTION

FUNCTION load_results()
    TRY:
        OPEN "results.txt" in READ mode AS file
        content = READ all lines from file
        PRINT content
        CLOSE file
    CATCH FileNotFoundError:
        PRINT "No previous survival records found."
    END TRY
END FUNCTION
```

### C. User Interface: `main.py`
This is the entry point that controls the gameplay loop, integrating the logic and data handler.

```text
// main.py
IMPORT survival_logic
IMPORT data_handler

FUNCTION main()
    PRINT "Welcome to the Campus Survival App (Funny Edition)!"
    PRINT "Please enter your student name:"
    INPUT student_name
    
    WHILE True DO
        PRINT "\n--- MAIN MENU ---"
        PRINT "1. Start Survival Simulation"
        PRINT "2. View Previous Survival Records"
        PRINT "3. Exit"
        
        INPUT menu_choice
        
        IF menu_choice == "1" THEN
            // Initialize round variables
            current_score = 50 // Base starting score
            max_possible_score = 50 + 10 + 15 + 5 // Starting score + max from scenarios
            
            // Run through scenarios
            current_score = survival_logic.exam_survival(current_score)
            current_score = survival_logic.cafeteria_mode(current_score)
            current_score = survival_logic.attendance_checker(current_score)
            
            // Calculate final percentage and status
            final_percentage = survival_logic.calculate_score(current_score, max_possible_score)
            status = survival_logic.generate_result_message(final_percentage)
            
            // Display Results
            PRINT "\n--- FINAL SURVIVAL REPORT ---"
            PRINT "Student: " + student_name
            PRINT "Score: " + final_percentage + "%"
            PRINT status
            
            // Save data
            data_handler.save_result(student_name, final_percentage, status)
            
        ELSE IF menu_choice == "2" THEN
            PRINT "\n--- SURVIVAL ARCHIVES ---"
            data_handler.load_results()
            
        ELSE IF menu_choice == "3" THEN
            PRINT "Exiting Campus Survival App. Don't forget your assignments!"
            BREAK // Exit the loop
            
        ELSE
            PRINT "Invalid choice. Please select 1, 2, or 3."
        END IF
    END WHILE
END FUNCTION

// Start the program
CALL main()
```
