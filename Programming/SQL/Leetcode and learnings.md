1. DATE_ADD : function to check for date difference
	- [197. Rising Temperature](https://leetcode.com/problems/rising-temperature/)
	- ```
		# Write your MySQL query statement below
		SELECT W1.id
		FROM WEATHER W1
		JOIN WEATHER W2
		ON W1.recordDate = DATE_ADD(W2.recordDate, INTERVAL 1 DAY)
		WHERE W1.temperature > W2.temperature;

2. Having clause -> use after group by;
	Where clause -> use before group by;