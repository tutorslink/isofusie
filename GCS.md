# Campus Survival App (Funny Edition) - Extended Project Plan

## 1. Goal & Learning Outcomes Mapping
* **CLO3 (Data Abstraction):** Using lists to store a history of player choices and scores during the session, and using file I/O to persist complex strings.
* **CLO2 (Fundamentals):** 
  * **Variables & Strings:** Storing names, feedback messages, and formatted output.
  * **Loops:** `WHILE` loops for the main menu and `WHILE` loops for strict input validation.
  * **Conditionals:** `IF/ELIF/ELSE` branching for every scenario.
  * **Functions:** Modularizing every scenario, calculation, and file operation.
  * **Arrays/Lists:** Tracking the sequence of choices made in a round.
* **CLO5 (Teamwork):** The modular file structure (`main.py`, `survival_logic.py`, `data_handler.py`) allows team members to divide the work cleanly.

---

## 2. Detailed Pseudocode Implementation

### A. Core Game Logic: `survival_logic.py`
This file contains the helper functions and all 6 interactive scenarios.

```text
// survival_logic.py

/* 
Function: get_valid_input
Purpose: A helper function with a loop to ensure the user only types 1, 2, or 3.
*/
FUNCTION get_valid_input(prompt_message)
    is_valid = FALSE
    WHILE is_valid == FALSE DO
        PRINT prompt_message
        INPUT user_choice
        IF user_choice == "1" OR user_choice == "2" OR user_choice == "3" THEN
            is_valid = TRUE
            RETURN user_choice
        ELSE
            PRINT "Error: The university does not accept that answer. Try 1, 2, or 3."
        END IF
    END WHILE
END FUNCTION

// --- SCENARIO 1: EXAMS ---
FUNCTION exam_survival(current_score, choice_history_list)
    PRINT "\n--- SCENARIO 1: THE 2 AM CRAM SESSION ---"
    PRINT "Tomorrow is your final exam. You know nothing."
    PRINT "1. Cram all night fueled by 5 Red Bulls."
    PRINT "2. Sleep and hope for divine intervention."
    PRINT "3. Watch 3 hours of YouTube tutorials on 'How to guess effectively'."
    
    choice = get_valid_input("Choose your strategy (1/2/3): ")
    APPEND choice to choice_history_list
    
    IF choice == "1" THEN
        PRINT "Outcome: Caffeine Overdose! You passed, but your hands are shaking."
        RETURN current_score + 10
    ELSE IF choice == "2" THEN
        PRINT "Outcome: You chose sleep... Professor noticed you drooling on the test."
        RETURN current_score - 15
    ELSE IF choice == "3" THEN
        PRINT "Outcome: YouTube algorithms saved you! C- is still a degree."
        RETURN current_score + 5
    END IF
END FUNCTION

// --- SCENARIO 2: CAFETERIA ---
FUNCTION cafeteria_mode(current_score, choice_history_list)
    PRINT "\n--- SCENARIO 2: CAFETERIA BATTLE ROYALE ---"
    PRINT "You enter the dining hall at peak lunch hour. It's absolute chaos."
    PRINT "1. Eat the mysterious 'Meat Surprise'."
    PRINT "2. Buy a $10 iced coffee and call it lunch."
    PRINT "3. Fight a freshman for the last slice of pizza."
    
    choice = get_valid_input("Choose your lunch (1/2/3): ")
    APPEND choice to choice_history_list
    
    IF choice == "1" THEN
        PRINT "Outcome: Food poisoning acquired! You lose valuable study time."
        RETURN current_score - 10
    ELSE IF choice == "2" THEN
        PRINT "Outcome: Bank account crying, but energy restored."
        RETURN current_score + 5
    ELSE IF choice == "3" THEN
        PRINT "Outcome: Victory! You feast like a king. The freshman is crying."
        RETURN current_score + 15
    END IF
END FUNCTION

// --- SCENARIO 3: ATTENDANCE ---
FUNCTION attendance_checker(current_score, choice_history_list)
    PRINT "\n--- SCENARIO 3: THE 8 AM LECTURE ---"
    PRINT "It's an 8 AM lecture, it's raining, and your bed is very warm."
    PRINT "1. Sprint to class in the rain."
    PRINT "2. Join the Zoom link from bed (camera off)."
    PRINT "3. Ignore it entirely and go back to sleep."
    
    choice = get_valid_input("Choose your attendance method (1/2/3): ")
    APPEND choice to choice_history_list
    
    IF choice == "1" THEN
        PRINT "Outcome: You arrived soaking wet, but the professor respects your dedication."
        RETURN current_score + 10
    ELSE IF choice == "2" THEN
        PRINT "Outcome: You fell asleep listening to the lecture. Retained 10% of the info."
        RETURN current_score + 5
    ELSE IF choice == "3" THEN
        PRINT "Outcome: Surprise Pop Quiz today! Your grade took a massive hit."
        RETURN current_score - 20
    END IF
END FUNCTION

// --- SCENARIO 4: GROUP PROJECT ---
FUNCTION group_project_chaos(current_score, choice_history_list)
    PRINT "\n--- SCENARIO 4: THE DREADED GROUP PROJECT ---"
    PRINT "Your group members are ghosting you. The presentation is tomorrow."
    PRINT "1. Do the entire project yourself while crying."
    PRINT "2. Snitch to the professor."
    PRINT "3. Submit what you have (just a title slide) and accept your fate."
    
    choice = get_valid_input("Choose your action (1/2/3): ")
    APPEND choice to choice_history_list
    
    IF choice == "1" THEN
        PRINT "Outcome: A+! But you aged 5 years in one night."
        RETURN current_score + 20
    ELSE IF choice == "2" THEN
        PRINT "Outcome: Professor doesn't care. Now your group hates you AND you failed."
        RETURN current_score - 15
    ELSE IF choice == "3" THEN
        PRINT "Outcome: You got a solid D. It builds character."
        RETURN current_score - 5
    END IF
END FUNCTION

// --- SCENARIO 5: SPORTS & SOCIAL ---
FUNCTION sports_and_friends(current_score, choice_history_list)
    PRINT "\n--- SCENARIO 5: INTRAMURAL SPORTS ---"
    PRINT "Your friends desperately need a 6th player for intramural dodgeball."
    PRINT "1. Play aggresively and carry the team."
    PRINT "2. Go, but just sit on the bench and cheer."
    PRINT "3. Refuse and stay in your dorm to play video games."
    
    choice = get_valid_input("Choose your social move (1/2/3): ")
    APPEND choice to choice_history_list
    
    IF choice == "1" THEN
        PRINT "Outcome: You won the championship but twisted your ankle. Worth it."
        RETURN current_score + 15
    ELSE IF choice == "2" THEN
        PRINT "Outcome: You were a great mascot. Free pizza post-game!"
        RETURN current_score + 10
    ELSE IF choice == "3" THEN
        PRINT "Outcome: Sanity restored, but your friends lost 10-0 without you."
        RETURN current_score + 0
    END IF
END FUNCTION

// --- SCENARIO 6: FREE TIME ---
FUNCTION free_time_boredom(current_score, choice_history_list)
    PRINT "\n--- SCENARIO 6: THE AWKWARD 3-HOUR GAP ---"
    PRINT "You have 3 hours to kill between classes on campus."
    PRINT "1. Go to the library and actually get ahead on homework."
    PRINT "2. Doomscroll TikTok in the student union."
    PRINT "3. Find a random couch in the geology building and nap."
    
    choice = get_valid_input("Choose your free time activity (1/2/3): ")
    APPEND choice to choice_history_list
    
    IF choice == "1" THEN
        PRINT "Outcome: Academic weapon! You feel productive and superior."
        RETURN current_score + 15
    ELSE IF choice == "2" THEN
        PRINT "Outcome: Brain rot achieved. You forgot what year it is."
        RETURN current_score - 10
    ELSE IF choice == "3" THEN
        PRINT "Outcome: You woke up 5 hours later. You missed your next class."
        RETURN current_score - 15
    END IF
END FUNCTION

// --- SCORING HELPERS ---
FUNCTION calculate_score(points_earned, total_possible)
    score_percentage = (points_earned / total_possible) * 100
    RETURN ROUND(score_percentage, 2)
END FUNCTION

FUNCTION generate_result_message(percentage)
    IF percentage >= 85 THEN
        RETURN "Status: Campus Legend! You survived, thrived, and got Dean's List."
    ELSE IF percentage >= 60 THEN
        RETURN "Status: Survived but emotionally unstable. Average student."
    ELSE IF percentage >= 40 THEN
        RETURN "Status: Barely hanging on. The coffee machine is your only friend."
    ELSE
        RETURN "Status: Academic Probation... The cafeteria staff will miss you."
    END IF
END FUNCTION
```

### B. Data Storage: `data_handler.py`
Handles writing the tracking array and score to a persistent text file.

```text
// data_handler.py

FUNCTION save_result(student_name, score_percentage, status_message, choice_history_list)
    // Convert the list/array of choices to a readable string
    choices_string = JOIN(choice_history_list, ", ")
    
    OPEN "results.txt" in APPEND mode AS file
    
    WRITE to file: "Student: " + student_name
    WRITE to file: "Survival Rate: " + score_percentage + "%"
    WRITE to file: "Final Status: " + status_message
    WRITE to file: "Decisions Array: [" + choices_string + "]"
    WRITE to file: "---------------------------------"
    
    CLOSE file
    PRINT "=> System: Your survival record has been etched into university history."
END FUNCTION

FUNCTION load_results()
    TRY:
        OPEN "results.txt" in READ mode AS file
        file_contents = READ all lines from file
        
        IF file_contents is EMPTY THEN
            PRINT "The archives are empty. No students have survived yet."
        ELSE
            PRINT file_contents
        END IF
        
        CLOSE file
    CATCH FileNotFoundError:
        PRINT "Error: 'results.txt' not found. Be the first to play!"
    END TRY
END FUNCTION
```

### C. User Interface & Integration: `main.py`
The main loop that runs all 6 scenarios in sequence.

```text
// main.py
IMPORT survival_logic
IMPORT data_handler

FUNCTION main()
    PRINT "================================================="
    PRINT "  WELCOME TO THE CAMPUS SURVIVAL APP (FUNNY ED.) "
    PRINT "================================================="
    
    PRINT "Please enter your Student Name or ID:"
    INPUT student_name
    
    game_is_running = TRUE
    
    // Continuous gameplay loop
    WHILE game_is_running == TRUE DO
        PRINT "\n========= MAIN MENU ========="
        PRINT "1. Start a New Survival Week"
        PRINT "2. View Previous Survivors (High Scores)"
        PRINT "3. Drop Out (Exit)"
        PRINT "============================="
        
        INPUT menu_choice
        
        IF menu_choice == "1" THEN
            // Initialize round data
            current_score = 50       // Start with 50 base sanity/survival points
            // Max score = 50(base) + 10 + 15 + 10 + 20 + 15 + 15 = 135
            max_possible_score = 135 
            choice_history = EMPTY LIST // Array to track user choices (CLO2 requirement)
            
            PRINT "\n[ THE SEMESTER BEGINS ]"
            
            // Execute all 6 Scenarios sequentially
            current_score = survival_logic.exam_survival(current_score, choice_history)
            current_score = survival_logic.cafeteria_mode(current_score, choice_history)
            current_score = survival_logic.attendance_checker(current_score, choice_history)
            current_score = survival_logic.group_project_chaos(current_score, choice_history)
            current_score = survival_logic.sports_and_friends(current_score, choice_history)
            current_score = survival_logic.free_time_boredom(current_score, choice_history)
            
            // Post-game calculations
            final_percentage = survival_logic.calculate_score(current_score, max_possible_score)
            status = survival_logic.generate_result_message(final_percentage)
            
            // Display Final Report
            PRINT "\n========= FINAL SURVIVAL REPORT ========="
            PRINT "Student: " + student_name
            PRINT "Survival Rate: " + final_percentage + "%"
            PRINT status
            PRINT "Your sequence of decisions: " + choice_history
            PRINT "========================================="
            
            // Save data to results.txt
            data_handler.save_result(student_name, final_percentage, status, choice_history)
            
        ELSE IF menu_choice == "2" THEN
            PRINT "\n========= SURVIVAL ARCHIVES ========="
            data_handler.load_results()
            PRINT "====================================="
            
        ELSE IF menu_choice == "3" THEN
            PRINT "Dropping out... Good luck in the real world!"
            game_is_running = FALSE // Breaks the loop to exit
            
        ELSE
            PRINT "Invalid choice. The registrar's office does not understand your request."
        END IF
    END WHILE
END FUNCTION

// Application Entry Point
CALL main()
```
