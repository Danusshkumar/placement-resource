# Quantitative Aptitude

## Basics of Calendar related problems

1. week - 7 days
2. 1 year - 52 weeks + 1 odd day
3. Leap year - 52 weeks + 2 odd days
4. Ordinary year - 28<sup>th</sup> feb
5. Leap year - 29<sup>th</sup> feb

### Codes for Days, Months and Years

#### Days

```
0 - Sunday
1 - Monday
2 - Tuesday
3 - Wednesday
4 - Thursday
5 - Friday
6 - Saturday
```

#### Months

```
  J  F  M  A  M  J  J  A  S  O  N  D
  0  3  3  6  1  4  6  2  5  0  3  5
```

#### Years

```
(1600 - 1699) - 6
(1700 - 1799) - 4
(1800 - 1899) - 2
(1900 - 1999) - 0
(2000 - 2099) - 6
```

### Problems

**1. What was the day of the week on 26th Jan 1947 ?**

**Solution:**

| Description | Value |
| --- | --- |
| Last two digit of the year | 47 |
| Divide those digits by 4 | 11 |
| Date | 26 |
| Code of month | 0 |
| Code of year | 0 |
| Total | 84 |

```
Total % 7 = 84 % 7
          = 0
```
Week day corresponding to the code 0 is **Sunday**.

---


**2. What was the day of the week on 5th Oct 2016 ?**

**Solution:**

| Description | Value |
| --- | --- |
| Last two digit of the year | 16 |
| Divide those digits by 4 | 04 |
| Date | 05 |
| Code of month | 0 |
| Code of year | 6 |
| Total | 31 |

```
Total % 7 = 31 % 7
          = 3
```
Week day corresponding to the code 3 is **Wednesday**.

---


**3. What dates of May 2002 did Monday falls ?**

**Solution:**

Let's take 1st May 2002

| Description | Value |
| --- | --- |
| Last two digit of the year | 2 |
| Divide those digits by 4 | 0 |
| Date | 1 |
| Code of month | 1 |
| Code of year | 6 |
| Total | 10 |

```
Total % 7 = 10 % 7
          = 3
```
If the 1st May is Wednesday, then 
```
1  2  3  4  5  6
W  T  F  S  S  M
```
6th May is Monday. Furthermore,<br>
**6, 13, 20, 27** are the dates that falls on Monday.

---

**4. Today is Monday. After 30 days, it will be ?**

**Solution:**

```
To find week codes,
    = 30%7
    = 2
```
Then, Monday + 2 will be **Wednesday**.
