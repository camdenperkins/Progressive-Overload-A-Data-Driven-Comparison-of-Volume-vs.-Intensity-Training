# Volume-Vs-Intensity-Gym-Training
This independent project was completed by Camden Perkins, contact information: camden@fperkins.com / 203-290-7611

# Background
I began consistently weight training during the fall semester of my Junior year at Elon Univeristy, around late August in 2023. My workout plan was and still is volume focused, using three sets on average for each exercise aiming for eight to ten repetitions. I began tracking my workouts at the start of my Senior year, on August 20th, 2024. I saw continued growth for around a year but began to plateau rapidly around February 2025. As a result, on April 11th, I decided to focus on intensity training, with a focus of two sets per exercies aiming for four to six repetitions.

I utilized the "Push Pull Legs" training split, which means chest/triceps/front and side delts, followed by back/biceps/rear-delts, and then ending with legs. I then completed this routine again, thus exercising muscle groups twice per week. Both types of training were performed until failure

# Purpose
Research Question: "Does high-intensity resistance training result in a statistically significant higher frequency of progressive overload compared to high-volume?"

I will use Logistic Regression during this process.

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

# Date Preparation and Manipulation
I began by loading and merging all my excel files together in one variable called "gym_stats".

Following this, I cleaned "gym_stats" by removing the empty separator rows and NaN values. I then added a new column called "Intensity" which assigned an integer "0" to the volume-focused months and a "1" to the intenisty-focused months. 

# Determining Progressive Overload
I created a function to check every workout against the best performance recorded so far for that specific exercise. This identifes and declares any new personal records and thus achieving progressive overload. This is the backbone of my study. <br>
<img width="414" height="308" alt="image" src="https://github.com/user-attachments/assets/63205ee6-509e-411a-94bc-fb35a6b32b49" />

1. Ensuring the 'Weight' and 'Rep' columns are usable numbers 
2. Initializes a 'Prog_Overload' column with zeros 
3. Loop prioritizes weight over repetitions and begins by establishing a maximum for each
4. Goes through exercises and checks if there is a new maximum weight.
5. If not, checks if there is a new maximum repetitions

# Selecting Exercises To Study
I want to focus on the exercises I performed the most to ensure the most statistically accurate data. <br>
<img width="238" height="134" alt="image" src="https://github.com/user-attachments/assets/ab6493a6-4162-4a8b-9581-4ed9e52cb662" /> <br>
The table above displays the most represented so let's go with these.

# Applying Function
I filtered for the specific exercises we declared above in the "gym_statistics" and then applied the function we created to each of the three. Here is example data fom Carter Extension: <br>
<img width="278" height="220" alt="image" src="https://github.com/user-attachments/assets/57c675eb-fb51-433b-9e7e-16cb5f3dad55" /> <br>
Looking at this table, we see that the workouts completed in December were correctly labeled as non-intensive and thus volume focused. The opposite applies for the bottom five rows in the image. Along with this, the second set of "Carter Extension" on December 5th was labeled as progressive overload. This is correct because the exercise was completed with the heavist (maximum) weight recorded thereby determining the function works correctly.

# Training the Dataset 
I created a new list that only include our target exercises: Carter Extension, Lat Pulldown, and Chest Press. Using this...

I established the independent variable as the intensity column as it is the factor I am testing. <br>
The dependent variable is the Progressive Overload column as it is the factor I want to predict. <br>

Lastly, I created a constant which is required by the library and trained/fit the data.

# Results
Key Numbers:

1. coef (Coefficient): 1.4377 <br>

The coefficient shows the direction and strength of the relationship. Because this number is positive, it means that when the Intensity variable changes from 0 (Volume) to 1 (Intensity), the likelihood of achieving progressive overload (Prog_Overload = 1) goes up. A coefficient of +1.44 indicates a strong positive relationship.

3. P>|z| (p-value): 0.000 <br>

P-value measures the probability that you would see a result this strong purely by random chance. The standard threshold for significance is 0.05. My p-value of 0.000 is far below this threshold. This gives strong evidence to reject the idea that both training styles are equal I can be very confident that the positive effect of intensity training is real.

3. [0.025 and 0.975] (Confidence Interval): 0.681 to 2.194

This is the 95% confidence range for my coefficient. There is 95% confidence that the "true" effect of the intensity training lies somewhere between +0.681 and +2.194. This further confirms that the positive effect is statistically significant.

# Vizualization
<img width="648" height="368" alt="image" src="https://github.com/user-attachments/assets/71c40d1c-b536-4444-a075-7520b7288b19" /> <br>
This graph compares the total number of personal records achieved by date. The blue line increased at 7.6 percent. In other words, every time I completed a workout with a focus on volume training, I had a 7.6 percent chance to obtain a personal best. On the other hand, the red line intensity-focused training grew at 25.8 percent demonstrating the key difference in productivity between the two kinds of workout plans.

# Conclusion
Through my findings with Logestic Regression, I can confidently say that intensity-focused training is significantly more effective at producing progressive overload than volume-focused training. The results are not ambiguous and are highly statistically significant, meaning it is extremely unlikely this finding is due to random chance. <br>

I thoroughly enjoyed completing this personal project and I am pleased to see such strong findings after just under two years of consistent training. If you made it this far, thank you for taking the time to read my work. 














