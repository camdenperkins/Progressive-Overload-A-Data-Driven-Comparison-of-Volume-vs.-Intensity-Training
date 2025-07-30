# Volume-Vs-Intensity-Gym-Training
This independent project was completed by Camden Perkins, contact information: camden@fperkins.com / 203-290-7611

# Background
I began consistently weight training during the fall semester of my Junior year at Elon Univeristy, around late August in 2023. My workout plan was volume focused, using three sets on average for each exercise aiming for eight to ten repetitions. I saw continued growth for around a year but began to plateau rapidly around February 2025. As a result, on April 11th, I decided to focus on intensity training, with a focus of two sets per exercies aiming for four to six repetitions.

I utilized the "Push Pull Legs" training split, which means chest/triceps/front and side delts, followed by back/biceps/rear-delts, and then ending with legs. I then completed this routine again, thus exercising muscle groups twice per week. Both types of training were performed until failure

# Purpose
Research Question: "Does high-intensity resistance training result in a statistically significant higher frequency of progressive overload compared to high-volume?"

# Definitions
Progressive Overload is involves gradually increasing the weight, frequency, or intensity of your workouts over time to challenge your body and promote strength gains

# Functionality
I used excel to track my progress, an example of a given workout is below: <br>
<img width="354" height="175" alt="image" src="https://github.com/user-attachments/assets/38104745-cb08-46f7-9fed-a682ead053da" />

Key: <br>
-Date: Date of workout <br>
-Split: Type of workout that dictated what muscles were exercised, such as push/pull/legs <br>
-Exercise: Activity performed, such as chest press, bicep curl, etc. <br>
-Rep: How many repetitions I completed each exercise for <br>

I then used python.

# Selecting Exercises To Study
I want to focus on the exercises I performed the most to ensure the most statistically accurate data. <br>
<img width="238" height="134" alt="image" src="https://github.com/user-attachments/assets/ab6493a6-4162-4a8b-9581-4ed9e52cb662" /> <br>
The table above displays the most represented so let's go with these.

# Date Preparation and Manipulation
I began by loading and merging all my excel files together in one variable called "gym_stats".

Following this, I cleaned "gym_stats" by removing the empty separator rows and NaN values. I then added a new column called "Intensity" which assigned an integer "0" to the volume-focused months and a "1" to the intenisty-focused months. 

# Determining Progressive Overload
I created a function to check every workout against the best performance recorded so far for that specific exercise. This identifes and declares any new personal records and thus achieving progressive overload. <br>
<img width="535" height="310" alt="image" src="https://github.com/user-attachments/assets/e15c4f42-9569-49b3-9faa-75c7252c1f52" /> <img width="535" height="310" alt="image" src="https://github.com/user-attachments/assets/983fc191-eaee-43be-a0e9-0abb131488ca" />










