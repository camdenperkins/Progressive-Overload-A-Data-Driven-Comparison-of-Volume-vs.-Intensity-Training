# Progressive Overload: A Data Driven Comparison of Volume vs Intensity Training
This independent project was completed by Camden Perkins, contact information: camden@fperkins.com / 203-290-7611

# Background
I began consistently weight training during the fall semester of my Junior year at Elon University, around late August in 2023. My workout plan was volume focused, using three sets on average for each exercise aiming for eight to ten repetitions. I saw continued growth for around a year but began to plateau rapidly around February 2025. As a result, on April 11th, I decided to focus on intensity training, with a focus of two sets per exercise aiming for four to six repetitions.

I utilized the "Push Pull Legs" training split, which means chest/triceps/front and side delts, followed by back/biceps/rear-delts, and then ending with legs. I then completed this routine again, thus exercising muscle groups twice per week. Both types of training were performed until failure.

I maintained a body weight of 225 pounds, fluctuating plus or minus five pounds. To support my training, I aimed to consume 180-225 grams of protein daily.

# Purpose
Research Question: "Does high-intensity resistance training result in a statistically significant higher frequency of progressive overload compared to high-volume?"

To answer this question, I’ll be conducting a two-part study.

**Section 1** focuses on analyzing the training metrics and progression I tracked during my senior year at Elon University, spanning August 20, 2024, to May 21, 2025. I plan to explore patterns across both the full year and the isolated, intensity-focused training block during the spring semester.

**Section 2** builds on that foundation by applying predictive modeling techniques—specifically linear and logistic regression—to forecast future progressive overload events. I’ll then compare these predictions against actual post-study data to evaluate the model’s accuracy and reliability.

# Definitions
<ins>Progressive Overload</ins> involves gradually increasing the weight, frequency, or intensity of your workouts over time to challenge your body and promote strength gains. <br>

<ins>Logistic Regression</ins> is a statistical method used to model the probability of a binary outcome (an event with two possible results, like yes/no or pass/fail) based on one or more predictor variables.

# Functionality
This analysis covers my workout data recorded during my senior year, beginning on August 20th, 2024. It is important to note that this dataset does not include my junior year, which was primarily dedicated to learning correct form and establishing a foundational strength base. Therefore, the progress analyzed here reflects my development as an intermediate lifter, rather than a novice. <br>

Furthermore, a shoulder injury from September 23, 2024, to approximately November 11, 2024, prevented me from training to failure. This context is crucial as it results in a comparison of five to six months of volume-focused training to only one month of high-intensity training.

I used excel to track my progress, an example of a given workout is below: <br>
<img width="354" height="175" alt="image" src="https://github.com/user-attachments/assets/38104745-cb08-46f7-9fed-a682ead053da" />

Key: <br>
-Date: Date of workout <br>
-Split: Type of workout that dictated what muscles were exercised, such as push/pull/legs <br>
-Exercise: Activity performed, such as chest press, bicep curl, etc. <br>
-Rep: How many repetitions I completed each exercise for <br>

# Implementation and Workflow

### Date Preparation and Manipulation
I  used python to programmatically clean, transform, and analyze this workout data to answer my research question.

I began by loading and merging all my Excel files into a single DataFrame called gym_stats, which includes workouts from Fall 2024, Winter 2024, Spring 2025 (volume), and Spring 2025 (intensity). I cleaned gym_stats by removing empty rows and NaN values, then concatenated everything together and reset the index. Finally, I standardized the exercise names by trimming spaces and converting them to lowercase.

<img width="601" height="197" alt="image" src="https://github.com/user-attachments/assets/61804401-03ce-4926-9a8c-72a5d6e41a4c" /> <br>


I added a new column called Intensity, assigning an integer “0” to volume-focused months (Aug 20, 2024 – Apr 10, 2025) and “1” to intensity-focused months (Apr 1, 2025 – May 21, 2025). This provided a simple way to label each workout by training style for later analysis.

<img width="629" height="171" alt="image" src="https://github.com/user-attachments/assets/6994b195-ebfc-4ed2-891e-1c0bed5b44a2" />

### Determining Progressive Overload
I created a function to check every workout against the best performance recorded so far for that specific exercise. This identifies and declares any new personal records and thus achieving progressive overload. <br>
<img width="414" height="308" alt="image" src="https://github.com/user-attachments/assets/63205ee6-509e-411a-94bc-fb35a6b32b49" />

1. Ensures the 'Weight' and 'Rep' columns contain only numerical data, if not they are removed.
2. Creates new column named 'Prog_Overload' and sets all values to 0. This establishes a baseline, assuming no personal record has been achieved until the function proves otherwise. 
3. Function loops through each unique exercise (e.g., 'Chest Press', 'Lat Pulldown'). For each one it creates a temporary history of only that exercise's sets. Also resets the 'max_weight' and 'reps_at_max_weight' trackers to zero, ensuring that the records do not interfere with another.
4. Function chronologically checks if the current_weight is heavier than the max_weight recorded so far for that exercise. If so, function marks this set as a personal record by changing its Prog_Overload value to 1 and updates the max_weight to this new record.
5. If the current_weight is not a new record, function checks if it matches the existing max_weight but was performed for more repetitions. If this condition is met, it also flags the set as a progressive overload event and updates the rep record at that weight.

Function correctly prioritizes lifting heavier weight as the primary driver of overload, with increasing reps as a secondary factor.

### Applying Function
I want to focus on the exercises I performed the most to ensure statistically accurate data. The most common exercises in the full-year dataset include Incline DB Press and Chest Press, while the most significant in the spring semester were Close Grip Row and Rope Hammer Curl.

I filtered through both the full-year and spring datasets using the selected exercises, then applied the newly created function, shown in the example below. <br>
<img width="369" height="139" alt="image" src="https://github.com/user-attachments/assets/b672d0a7-5036-46ed-a312-40b2a9a204bb" /> <br>
As shown in the table, the workouts completed in May were correctly labeled and categorized as intensive. The opposite applies for the February five rows in the image. Along with this, the Chest Press set on May 5th was recorded as progressive overload event. This indicates that the exercise was completed with a new heaviest (maximum) weight or rep for that lift, confirming that the function works.

# Section One - Empirical Analysis

### Visualization #1
<img width="799" height="463" alt="image" src="https://github.com/user-attachments/assets/2bed709f-da09-4511-896a-bf1ee75e175f" /> <br>
### Analysis
The bar chart compares total progressive overload between volume-based and intensity-based training across Chest Press and Incline DB Press. Intensity-based training resulted in overload scores of 8 and 6, respectively, while volume-based training reached only 3 for both exercises. Despite the five–six month time difference, intensity-based training still produced a 167% increase for Chest Press and a 100% increase for Incline DB Press.

### Visualization #2
<img width="774" height="460" alt="image" src="https://github.com/user-attachments/assets/b6717204-b95a-438c-a44d-aa40af7204b6" /> <br>
### Analysis
The scatter plot reveals a clear inverse relationship between reps and weight across both exercises. Close Grip Row sets dropped from 10 repetitions at 130 lbs in February to 6–7 repetitions at 195 lbs by May—a 50% increase in weight paired with a 30–40% reduction in reps. Similarly, Rope Hammer Curl progressed from 130 lbs for 8 reps to 180 lbs for 6 reps, marking a 38% increase in load with a 25% drop in reps. These shifts highlight how lower rep ranges enabled heavier lifts, reinforcing the effectiveness of intensity-based programming in promoting progressive overload.

### Section One Concluding Thoughts
The findings above offer direct support for the research question: Does high-intensity resistance training result in a statistically significant higher frequency of progressive overload compared to high-volume? Both the bar chart and scatter plot demonstrate that intensity-based training consistently produced greater overload outcomes—whether measured by total overload scores or by heavier weights achieved at lower rep ranges.

These results provide a strong empirical foundation for deeper analysis. With clear patterns emerging from the intensity block, the next step is to explore whether progressive overload events can be forecasted using machine learning—specifically logistic regression.

# Section Two - Predictive Modeling
Workout logs from June to August 2025 are not included in this study. Instead, I’ll use the empirical data gathered in Section One to predict future overload events. To do this, I’m applying logistic regression and focusing specifically on the spring intensity block. As the earlier results clearly showed, overload events were most frequent during high-intensity training, making this block the most reliable foundation for accurate forecasting.

Once the model generates its predictions, I’ll compare the total number of forecasted progressive overload events against my actual gym progress to evaluate how accurate the model was.

### Date Preparation and Manipulation
To start, I created a new DataFrame "spring_intensity_df", which simply isolates workouts labeled as high-intensity from the spring semester. Therefore, this DataFrame only contains roughly one month of workout logs. I then applied the calculate_progressive_overload function I established before to spring_intensity_df, resulting in a new DataFrame named part_four_df. To ensure statistical reliability, I filtered the data to include only the top 20 most frequently performed exercises. This step helps the model focus on well-represented movements with enough data to learn meaningful patterns.

To strengthen the model’s predictive power, I added several derived features—new variables created from existing data to highlight patterns that aren’t immediately obvious. Rather than relying solely on raw inputs like weight and reps, these features capture trends, ratios, and short-term changes. The features include:

-LoadPerRep: Calculated by dividing weight by reps, this metric reflects set intensity and helps distinguish between heavy low-rep sets and lighter high-rep volume. <br>
-RollingWeight and RollingRep: 3-set moving averages grouped by exercise that limit short-term fluctuations and highlight gradual progression, allowing the model to detect upward or downward trends in performance. <br>
-WeightDelta and RepDelta: Measure the change in weight and reps from one set to the next within each exercise that can indicate breakthroughs, fatigue, or strategic shifts in training style. <br>









