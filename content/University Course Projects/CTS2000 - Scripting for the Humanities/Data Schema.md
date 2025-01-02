---
title: "Data Schema - The Covid Museum: Journey into Unprecedented Times"
draft: false
tags:
  - CTS2000
---
___
# Museum Exhibit Summary 
The COVID Museum will display a variety of artifacts from the 2019-2021 era of the COVID-19 pandemic at the local Guelph gallery from January until early February. This exhibit will take visitors on a journey through the early stages of the pandemic and highlight its cultural impact on society. 

The star artifact of the health exhibit is the COVID-19 Rapid Response Antigen tests. Rapid Antigen self-testing kits were an important tool in the pandemic designed to detect the presence of virus proteins. These tests were often given out for free in pharmacies, test centres, and grocery stores and were useful for mass testing in schools, workplaces, large events, and travel. These tests are important to help control outbreaks and limit transmission of the virus.
![[covidtest.png]]
___
# Covid-19 Rapid Test Metadata 
| Data Categories          | Data Type | Example Values                            | Justification                                                                                                                       |
| ------------------------ | --------- | ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Date of release          | Date      | November 2020                             | Highlights when the test was officially authorized for public use, showing timeline relevance.                                      |
| Location of availability | String    | Pharmacies                                | Describes where the test can be accessed, impacting how the public engages with them.                                               |
| Test name                | String    | Covid-19 Antigen Rapid Test Device        | Identifies the specific test type.                                                                                                  |
| Test accuracy            | Float     | 78.3%                                     | Provides insight into how reliable the test; an important factor in evaluating the impact.                                          |
| Detection time           | Integer   | 15 minutes                                | Indicates how quickly the test deliveries results, showing tis efficiency.                                                          |
| Result type              | Boolean   | Positive/Negative                         | Explains the possible outcomes and function of the test.                                                                            |
| Cost per test            | Float     | $0.00                                     | Shows the accessibility and economic impact, relevant to showing the government’s response to importance of testing.                |
| Associated Health risks  | String    | Ingestion of tests chemical preservatives | Details potential risk of accidental consumption or coming into contact with the test solution, displaying the safety of the tests. |
| Artifact Type            | String    | Health Care                               | Explains the category that artifacts will be displayed with.                                                                        |
| Intended Use             | String    | To detect Covid-19 virus protein          | Provides insight into the purpose of the artifact in history, culture, or politics                                                  |
| Origin of artifact       | String    | Canada                                    | Indicates where the artifact was produced or distributed out of.                                                                    |
| Owner of artifact        | String    | Emily Scott                               | Recognizes and gives credit to the person who donated the artifact to the museum.                                                   |
___
# Contextual and Ethical Considerations 
When expanding the COVID-19 exhibit into a larger collection, we would focus on educating the younger generation born during the pandemic or in early education. The key highlights and exhibits of the museum could include: (1) A look into health care and warding against catching the virus. (2) The social impact and how we interact with the public and online spaces. (3) Environmental change and how COVID reversed significant environmental issues. When curating a more extensive collection, we hope the government, frontline, healthcare workers, and older generations contribute to the database and exhibit.

Throughout history, the pattern of pandemics has helped us respond to new breakouts in public health and tests the civil liberties given to us by the government. Throughout the COVID-19 pandemic, many of our civil liberties were limited, including the mandate to self-test for COVID-19. Self-testing before going out in public was mandatory if you had cold and flu symptoms. Covid-19 also acted as a stress test on society and shaped a new culture of life 6 feet apart with limited in-person social interaction.

We have curated the exhibit based on a timeline of events starting in late 2019 to late 2022. Using “Date of release” metadata, we can provide insight into how each stage of the pandemic progressed and the new science and technologies released to combat COVID-19. In 10 years, data collected from COVID-19 will still be used to influence research, medical insights, and societal efforts. In 20 years, the data may be interpreted as a historical case study, mainly used as an educational tool and a comparative framework to highlight what did and did not work in case of future pandemics. In 100 years, the data may be interpreted and focus more on its role in shaping the generations in the 21st century and the social justice and equity issues of the time. Some data collected may fade into myth or simplification, only focusing on the key events.
___
# Reflection 
The way objects are encoded shapes how they are interpreted because encoding determines how information is processed, understood, and remembered. A detailed database of information about an object can keep the information accurate in its value and source. The more consciously an object is encoded, the more transparent and effective communication becomes, leaving little room for misinterpretation. The control of data curation processes reflects an object's underlying values, biases, and power. For example, there is a selection bias when curating the COVID museum by deciding which artifacts to digitize and prioritize. Selection bias reflects not only the museum and intuitional priorities but also cultural values. The way the story is told is up to the power of the curators and archivists of the exhibit and less on the people the exhibit topic impacted.
___
# Works Cited
Canada, Service. “Testing for COVID-19: When to Get Tested and Testing Results.” _Aem_, 23 Oct. 2015, [www.canada.ca/en/public-health/services/diseases/2019-novel-coronavirus-infection/symptoms/testing/diagnosing.html](http://www.canada.ca/en/public-health/services/diseases/2019-novel-coronavirus-infection/symptoms/testing/diagnosing.html).

Forbes, Amy W. “Covid-19 in Historical Context: Creating a Practical Past.” _Hec Forum_, Jan. 2021, pp. 1–12, https://doi.org/10.1007/s10730-021-09443-x.

Government of Canada, Health Canada. “Rapid Antigen Test Kits and Potential Exposure to Hazardous Substances - Recalls, Advisories and Safety Alerts – Canada.ca.” _Recalls-Rappels.canada.ca_, 24 Feb. 2022, recalls-rappels.canada.ca/en/alert-recall/rapid-antigen-test-kits-and-potential-exposure-hazardous-substances.

Government of Ontario - Ontario Newsroom. “Ontario Deploys Rapid Testing to Support COVID-19 Response.” _Ontario.ca_, 24 Nov. 2020, news.ontario.ca/en/release/59330/ontario-deploys-rapid-testing-to-support-covid-19-response. Accessed 23 Nov. 2024.