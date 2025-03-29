# coding sample_python
pip install pandas textblob
python
import pandas as pd
from textblob import TextBlob

#Read a sample CSV file 
input_file = r'C:\Users\users\sentiment_analysis.csv'  
df = pd.read_csv(input_file)


# Define a function for sentiment analysis using TextBlob
def analyze_sentiment(text):
if isinstance(text, str):  
blob = TextBlob(text)
polarity = blob.sentiment.polarity
subjectivity = blob.sentiment.subjectivity
return polarity, subjectivity
return 0, 0  # Return default values

# Apply sentiment analysis
df[['polarity', 'subjectivity']] = df['review'].apply(lambda x: pd.Series(analyze_sentiment(x)))

# Identify similar sentiments (positive vs. negative)
positive_reviews = df[df['Polarity'] > 0]
negative_reviews = df[df['Polarity'] < 0]

print("\nProducts with Positive Sentiment:")
print(positive_reviews[['Product', 'Polarity']])

print("\nProducts with Negative Sentiment:")
print(negative_reviews[['Product', 'Polarity']])



# Save the results to a new CSV file in the same directory
output_file = r'C:\Users\sentiment_analysis_output.csv'
df.to_csv(output_file, index=False)

print(f"Sentiment analysis complete. Results saved to {output_file}")
