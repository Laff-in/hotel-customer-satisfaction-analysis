# Data Quality Log

This log documents every data cleaning decision made between the raw scraped
reviews (`data/raw/raw-hotel-reviews.csv`) and the analysis-ready dataset
(`data/processed/cleaned-hotel-reviews.csv`).

| Issue Identified | Action Taken |
|---|---|
| Rows with missing values in both the Rating and Review columns | Removed, contained insufficient information for customer satisfaction analysis |
| Rows with missing ratings but containing review text | Retained, the review text still provided useful service-quality information |
| Rows containing ratings but missing review text | Retained, the rating alone is still a measurable satisfaction indicator |
| Missing values in the Review Category column | Assigned a category based on the primary service quality factor discussed in the review |
| Missing values in the Guest Perception column | Classified as Positive, Neutral, or Negative based on the review's overall sentiment and/or rating |
| Inconsistent capitalization in Name and Review Category columns | Standardized using Proper Case formatting |
| Inconsistent capitalization in the Guest Perception column | Standardized to Positive / Neutral / Negative |
| Extra leading/trailing spaces in text values | Removed using text-cleaning functions |
| Reviews written in a foreign language | Translated into English before categorization |
| Short, generic positive comments (e.g. "Awesome", "Nice Hotel") | Categorized as "General Feedback" where no specific factor was identifiable |
| Reviews discussing multiple service quality factors | Assigned to the single factor most emphasized in the review |
| Reviews containing both positive and negative statements | Perception based on overall sentiment; category based on the dominant factor discussed |
| Rows with "No Review" text but an available rating | Perception inferred from the rating (1–2 = Negative, 3 = Neutral, 4–5 = Positive); category remained "No Review" |

## Column renames

| Original column | Renamed to |
|---|---|
| Title | Hotel Name |
| Star | Rating |
| Text | Review |

## Columns dropped

- `Url`, `ReviewUrl` , not required for the customer satisfaction analysis.

## New columns created

- **Rate Category**: bucketed version of the numeric Rating (e.g. Excellent, Good, Fair, Poor)
- **Review Category**: the primary service-quality factor discussed (Service, Food, Room, etc.)
- **Guest Perception**: overall sentiment (Positive / Neutral / Negative)

## A note on the raw data

The raw and cleaned datasets contain guest names and review text that were
originally scraped from **public Google Maps reviews**. The content is
already public, but including real names in a public GitHub repository is a
judgment call — see the note in the main [README](../README.md#data--privacy-note)
before publishing.
