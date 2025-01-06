## DATA ANALYSIS ON CALL CENTER DATA
# Introduction
This is a dummy dataset from PhoneNow a telecom company. The business is looking to transform their messy data to meaningful insight that could help improve service delivery and enhance customer experience. 
The overall aim of this analysis is to have an accurate overview of the trend in customer and agent behaviour.

# Objective
The aim of this analysis is visualise the data to reflect all relevant key performance indicators and metrics in the dataset.

Possible KPIs include:

Overall customer satisfaction, Overall calls answered/abandoned, Calls by time, Average speed of answer, Agent’s performance quadrant -> average handle time (talk duration) vs calls answered.

# Technical Details
The dataset is a dummy gotten from forage job stimulation. It had 10 columns which are call id, agent, date, time, topic, answered, resolved, speed of answer, Average Talk duration, satisfaction rating. 
The data type was a mix of date-time, text, integers
![](https://github.com/MarySabestine/Data-Visualisation-with-BI-Tools/blob/main/CC%20Dataset.png)

  # Data model relationship
  ![](https://github.com/MarySabestine/Data-Visualisation-with-BI-Tools/blob/main/model%20view.png)

  # DAX Measures and Calculations
  Agent performance measure
  
    Average Call Duration
    AverageCallDuration = AVERAGE('Call Center Data'[NewAvgTalkDuration])

    Average Speed of Answer
    AvgSpeedOfAnswer = AVERAGE('Call Center Data'[Speed of answer in seconds])

    Resolved Calls
    ResolvedCalls = COUNTROWS(FILTER('Call Center Data', 'Call Center Data'[Resolved] = "Y"))

    Total calls
    TotalCalls = DISTINCTCOUNT('Call Center Data'[Call Id])

    Total Calls Abandoned
    TotalCallsAbandoned = COUNTROWS(FILTER('Call Center Data', 'Call Center Data'[Answered (Y/N)] = "N"))

    Total Calls Answered
    TotalCallsAnswered = COUNTROWS(FILTER('Call Center Data', 'Call Center Data'[Answered (Y/N)] = "Y"))

    Unresolved Calls
    UnResolvedCalls = COUNTROWS(FILTER('Call Center Data', 'Call Center Data'[Resolved] = "N"))

    Top Agent
    TopAgent = VAR TopAgentTable = 
    TOPN(
        1, 
        SUMMARIZE(
            'Call Center Data', 
            'Call Center Data'[Agent], 
            "ResolvedCount", [ResolvedCalls]
        ), 
        [ResolvedCount], 
        DESC
    )
    RETURN
    MAXX(TopAgentTable, 'Call Center Data'[Agent])

# Insight

    
