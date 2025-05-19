# Tableau Calculated Fields from HR Dashboard Project

## 1. Hiring Metrics

# % Total Hired
[Total Hired] / TOTAL([Total Hired])

# % Highlight Max
WINDOW_MAX([% Total Hired]) = [% Total Hired]

# % Total Terminated
[Total Terminated] / TOTAL([Total Terminated])

## 2. Headcount Metrics

# Total Active
COUNT(
  IF ISNULL([Termdate]) 
  THEN [Employee ID] 
  END
)

# Total Hired
COUNT([Employee ID])

# Total Terminated
COUNT(
  IF NOT ISNULL([Termdate]) 
  THEN [Employee ID] 
  END
)

# Net Headcount Change
[Total Hired] - [Total Terminated]

# Retention Rate
[Total Active] / [Total Hired]

# Turnover Rate
[Total Terminated] / [Total Hired]

## 3. Employee Lifecycle Metrics

# Length of Hire (Tenure Calculation)
IF ISNULL([Termdate]) THEN 
  DATEDIFF('year', [Hiredate], TODAY()) 
ELSE 
  DATEDIFF('year', [Hiredate], [Termdate]) 
END

# Age Calculation
DATEDIFF('year', [Birthdate], TODAY())

## 4. Ranking and Highlight Logic

# Top Department Rankings
RANK([Total Hired]) <= 1

# Top Department Rankings
RANK([Total Hired]) <= 2

# Highlight Max
WINDOW_MAX([Total Hired]) = [Total Hired]

# % Total Hired (Repeated)
[Total Hired] / TOTAL([Total Hired])

# % Total Terminated (Repeated)
[Total Terminated] / TOTAL([Total Terminated])
