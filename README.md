# Progressive Overload: A Data Driven Comparison of Volume vs Intensity Training
This independent project was completed by Camden Perkins, contact information: camden@fperkins.com / 203-290-7611

# Background
I began consistently weight training during the fall semester of my Junior year at Elon University, around late August in 2023. My workout plan was volume focused, using three sets on average for each exercise aiming for eight to ten repetitions. I saw continued growth for around a year but began to plateau rapidly around February 2025. As a result, on April 11th, I decided to focus on intensity training, with a focus of two sets per exercise aiming for four to six repetitions.

I utilized the "Push Pull Legs" training split, which means chest/triceps/front and side delts, followed by back/biceps/rear-delts, and then ending with legs. I then completed this routine again, thus exercising muscle groups twice per week. Both types of training were performed until failure.

I maintained a body weight of 225 pounds, fluctuating plus or minus five pounds. To support my training, I aimed to consume 180-225 grams of protein daily.

# Purpose
Research Question: "Does high-intensity resistance training result in a statistically significant higher frequency of progressive overload compared to high-volume?"

To answer this question, I will use Logistic Regression. This statistical model is the ideal choice because the outcome I want to predict—whether a workout resulted in a personal record—is a binary, yes/no event. Logistic Regression will allow me to determine if the training style (Intensity) has a significant effect on the probability of this outcome occurring.

# Definitions
<ins>Progressive Overload</ins> involves gradually increasing the weight, frequency, or intensity of your workouts over time to challenge your body and promote strength gains. <br>

<ins>Logistic Regression</ins> is a statistical method used to model the probability of a binary outcome (an event with two possible results, like yes/no or pass/fail) based on one or more predictor variables.

# Functionality
This analysis covers my workout data recorded during my senior year, beginning on August 20th, 2024. It is important to note that this dataset does not include my junior year, which was primarily dedicated to learning correct form and establishing a foundational strength base. Therefore, the progress analyzed here reflects my development as an intermediate lifter, rather than a novice. <br>

Furthermore, a shoulder injury from September 23, 2024, to approximately November 11, 2024, prevented me from training to failure. This context is crucial as it results in a comparison of five to six months of volume-focused training to only three months of high-intensity training.

I used excel to track my progress, an example of a given workout is below: <br>
<img width="354" height="175" alt="image" src="https://github.com/user-attachments/assets/38104745-cb08-46f7-9fed-a682ead053da" />

Key: <br>
-Date: Date of workout <br>
-Split: Type of workout that dictated what muscles were exercised, such as push/pull/legs <br>
-Exercise: Activity performed, such as chest press, bicep curl, etc. <br>
-Rep: How many repetitions I completed each exercise for <br>

I then used python to programmatically clean, transform, and analyze this workout data to answer my research question.

# Date Preparation and Manipulation
I began by loading and merging all my excel files together in one DataFrame and called it "gym_stats". This DataFrame includes my workouts from Fall 2024, Winter 2024, Spring 2025 (volume), Spring 2025 (Intensity), and Summer 2025. Following this, I cleaned "gym_stats" by removing the empty separator rows and NaN values. 

I then added a new column called "Intensity" which assigned an integer "0" to the volume-focused months (August 20, 2024 - April 10, 2025) and a "1" to the intensity-focused months (April 11, 2025 - Present). This provided a clear method for categorizing each workout by its training style which will be useful later on. 

Image on the left is the code I described, while the image on the right is my DataFrame of gym logs.

<img width="664" height="212" alt="image" src="https://github.com/user-attachments/assets/af4f8005-2d05-499f-afae-c299f2c7d04c" />


# Determining Progressive Overload
I created a function to check every workout against the best performance recorded so far for that specific exercise. This identifies and declares any new personal records and thus achieving progressive overload. This is the backbone of my study. <br>
<img width="414" height="308" alt="image" src="https://github.com/user-attachments/assets/63205ee6-509e-411a-94bc-fb35a6b32b49" />

1. Ensures the 'Weight' and 'Rep' columns contain only numerical data, if not they are removed.
2. Creates new column named 'Prog_Overload' and sets all values to 0. This establishes a baseline, assuming no personal record has been achieved until the function proves otherwise. 
3. Function loops through each unique exercise (e.g., 'Chest Press', 'Lat Pulldown'). For each one it creates a temporary history of only that exercise's sets. Also resets the 'max_weight' and 'reps_at_max_weight' trackers to zero, ensuring that the records do not interfere with another.
4. Function chronologically checks if the current_weight is heavier than the max_weight recorded so far for that exercise. If so, function marks this set as a personal record by changing its Prog_Overload value to 1 and updates the max_weight to this new record.
5. If the current_weight is not a new record, function checks if it matches the existing max_weight but was performed for more repetitions. If this condition is met, it also flags the set as a progressive overload event and updates the rep record at that weight.

Function correctly prioritizes lifting heavier weight as the primary driver of overload, with increasing reps as a secondary factor.

# Selecting Exercises To Study
I want to focus on the exercises I performed the most to ensure the most statistically accurate data. <br>
<img width="238" height="134" alt="image" src="https://github.com/user-attachments/assets/ab6493a6-4162-4a8b-9581-4ed9e52cb662" /> <br>
The table above displays the most represented so let's go with these.

# Applying Function
I filtered for the specific exercises declared above in the "gym_stats" and then applied the function I created to each of the three. Here is example data from Carter Extension: <br>
<img width="278" height="220" alt="image" src="https://github.com/user-attachments/assets/57c675eb-fb51-433b-9e7e-16cb5f3dad55" /> <br>
As shown in the table, the workouts completed in December were correctly labeled as non-intensive and thus volume focused. The opposite applies for the bottom five rows in the image. Along with this, the second set of "Carter Extension" on December 5th was labeled as progressive overload. This is correct because the exercise was completed with a new heaviest (maximum) weight for that lift, confirming the function correctly identifies this as a progressive overload event.

# Training the Dataset 
I created a new DataFrame that only includes our target exercises: Carter Extension, Lat Pulldown, and Chest Press. From this new DataFrame,

I established the independent variable (X) as the intensity column as it is the factor I am testing. <br>
The dependent variable (y) is the Progressive Overload column as it is the factor I want to predict. <br>

Lastly, I created a constant which is required by the library and trained/fit the data.

# Results
<ins>Total Personal Records Achieved:</ins> <br>

Intensity-Focused Block: 23 PRs <br>
Volume-Focused Block: 12 PRs

This simple count reveals that the intensity-focused protocol produced nearly double the number of progressive overload events in a significantly shorter time frame.

<ins>Key Statistical Findings: </ins><br>
The logistic regression model was used to determine if this difference was statistically significant. The key results are as follows:

1. coef (Coefficient): 1.4377 <br>

The coefficient shows the direction and strength of the relationship. Because this number is positive, it means that when the Intensity variable changes from 0 (Volume) to 1 (Intensity), the likelihood of achieving progressive overload (Prog_Overload = 1) goes up. A coefficient of +1.44 indicates a strong positive relationship.

2. P>|z| (p-value): 0.000 <br>

P-value measures the probability that you would see a result this strong purely by random chance. The standard threshold for significance is 0.05. My p-value of 0.000 is far below this threshold. This gives strong evidence to reject the idea that both training styles are equal I can be very confident that the positive effect of intensity training is real.

3. [0.025 and 0.975] (Confidence Interval): 0.681 to 2.194

This is the 95% confidence range for my coefficient. There is 95% confidence that the "true" effect of the intensity training lies somewhere between +0.681 and +2.194. This further confirms that the positive effect is statistically significant.

# Visualizations
<img width="494" height="281" alt="image" src="https://github.com/user-attachments/assets/742921f0-fb39-4b00-993e-290d959826e4" />

This graph tracks the cumulative number of personal records (PRs) achieved throughout the study period. The blue line represents the volume-focused training block, while the red line represents the intensity-focused block. The steeper slope of the red line provides a clear confirmation that PRs were achieved at a significantly faster rate during the intensity training period. By the end of their respective phases, the volume block had yielded 12 PRs, whereas the shorter intensity block produced 23 PRs.

<img width="494" height="312" alt="image" src="https://github.com/user-attachments/assets/8e61dc61-1a57-486a-84c0-96065f8bda80" />

This second graph visualizes the core finding from the logistic regression model. The y-axis shows the model's predicted probability that any given set will result in a personal record. The upward-sloping red line indicates a strong positive relationship: switching from a volume style to an intensity style significantly boosts the likelihood of achieving a PR. This confirms the calculated success rates, where only 7.6% of sets resulted in a PR during volume training, compared to a 25.8% success rate during intensity training. The scattered grey dots represent the actual outcomes (0% for no PR, 100% for a PR), showing how the model fits the real-world data.

# Conclusion
Through my findings with Logistic Regression, I can confidently say that intensity-focused training is significantly more effective at producing progressive overload than volume-focused training. The results are not ambiguous and are highly statistically significant, meaning it is extremely unlikely this finding is due to random chance. <br>

These conclusions are further strengthened when considering the time difference between the two training protocols. The intensity-focused block produced nearly double the number of personal records (23 PRs) in only three months, compared to the 12 PRs achieved during the longer five-to-six month volume-focused block. This highlights that not only was the intensity protocol more effective, but it was also substantially more efficient at driving progress in a shorter timeframe.

# Personal Note
I thoroughly enjoyed completing this personal project and I am pleased to see such strong findings after just under two years of consistent training. If you made it this far, thank you for taking the time to read my work. 














