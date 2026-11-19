# Day 13 - Advanced SPL Commands

## Objective
Learn advanced Splunk Search Processing Language (SPL) commands and understand their use in SOC investigations.

## 1. Stats Command
The stats command performs statistical calculations on search results.

Common functions:
- count
- sum
- avg
- min
- max

SOC Use:
Summarize login events and identify activity patterns.

## 2. Timechart Command
The timechart command displays data over time in a chart.

SOC Use:
Identify unusual increases or decreases in security events.

## 3. Eval Command
The eval command creates or calculates new fields.

SOC Use:
Add labels or calculate values during investigations.

## 4. Where Command
The where command filters search results using conditions.

SOC Use:
Find events matching specific investigation criteria.

## 5. Sort Command
The sort command arranges search results in ascending or descending order.

SOC Use:
Identify accounts or events with the highest activity.

## 6. Top Command
The top command displays the most frequently occurring field values.

SOC Use:
Identify frequently appearing accounts or event values.

## 7. Rare Command
The rare command displays the least frequently occurring field values.

SOC Use:
Identify less common activity that may require investigation.

Note:
Rare activity is not automatically malicious.

## 8. Dedup Command
The dedup command removes duplicate results based on specified fields.

SOC Use:
Identify unique accounts or values.

## 9. Multiple Stats Calculations
The stats command can summarize multiple event categories.

SOC Use:
Compare successful and failed login activity.

## Learning Outcomes
- Learned advanced SPL commands.
- Understood statistical analysis in Splunk.
- Learned time-based event analysis.
- Practised filtering and sorting events.
- Understood frequent and rare field values.
- Learned how to remove duplicate results.
- Applied SPL to Windows Security Event Logs.
