# MS_SQL_SERVER TASK-1
 
 --Task-1
[Q]. Write a query to list out for each author and doctor the number of episodes made, but restrict your output to show only the author/doctor combinations for which more than 5 episodes have been written.
Ans =>
SELECT
	a.AuthorName,
	d.DoctorName,
    COUNT(e.EpisodeId) AS Episodes 
FROM 
	tblAuthor a
	INNER JOIN tblEpisode e on a.AuthorId= e.AuthorId
	INNER JOIN tblDoctor d on d.DoctorId= e.DoctorId
GROUP BY 
	a.AuthorName,
	d.DoctorName
HAVING 
	COUNT(e.EpisodeId) > 5 
ORDER BY COUNT(e.Episodeid) desc


--------------------------------------------------------------------------------
--Task -2
SELECT
(CAST(((YEAR(EventDate)/100)+1) AS varchar) + 'th century') AS 'Century',
COUNT(CAST(((YEAR(EventDate)/100)+1) AS varchar) + 'th century') AS 'Number of events'
FROM
[tblEvent]
GROUP BY
(CAST(((YEAR(EventDate)/100)+1) AS varchar) + 'th century')
WITH CUBE


---------------------------------------------------------------------------------
--Task -3
[Q].Create a subquery to list out all of those events whose:
•	Country id is not in the list of the last 30 country ids in alphabetical order; and
•	Category id is not in the list of the last 15 category ids in alphabetical order.

Ans=>
 USE WorldEvents;
GO
SELECT EventName, 
       EventDetails
FROM tblEvent
WHERE CountryID NOT IN(SELECT TOP 30 CountryId
                       FROM tblCountry
                       ORDER BY CountryID DESC) AND 
      CategoryID NOT IN(SELECT TOP 15 CategoryID
                        FROM tblCategory
                        ORDER BY CategoryId DESC);


---------------------------------------------------------------------------------
--Task -4
[Q]. Use a recursive CTE based on this table to show all of the menus, with breadcrumbs:

Ans=>
USE Carnival
GO

WITH menus AS ( 

	
	SELECT 
		MenuId,
		MenuName,
		CAST('Top' AS varchar(100)) AS Breadcrumb
	FROM 
		tblMenu
	WHERE 
		ParentMenuId  IS NULL 
	
	
	UNION ALL 
 
	SELECT 
		submenus.MenuId,
		submenus.MenuName,
		CAST((m.Breadcrumb + ' > ' + m.MenuName)
			AS varchar(100)) AS Breadcrumb
	FROM 
		tblMenu AS submenus
		INNER JOIN menus AS m
			ON submenus.ParentMenuId=m.MenuId
	) 


SELECT * FROM menus OPTION (MAXRECURSION 2)

