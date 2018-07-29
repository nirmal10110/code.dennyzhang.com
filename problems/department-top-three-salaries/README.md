
# Leetcode: Department Top Three Salaries     :BLOG:Hard:

---

Department Top Three Salaries  

---

Similar Problems:  

-   [Review: SQL Problems](https://code.dennyzhang.com/review-sql), [Tag: #sql](https://code.dennyzhang.com/tag/sql)

---

The Employee table holds all employees. Every employee has an Id, and there is also a column for the department Id.  

    +----+-------+--------+--------------+
    | Id | Name  | Salary | DepartmentId |
    +----+-------+--------+--------------+
    | 1  | Joe   | 70000  | 1            |
    | 2  | Henry | 80000  | 2            |
    | 3  | Sam   | 60000  | 2            |
    | 4  | Max   | 90000  | 1            |
    | 5  | Janet | 69000  | 1            |
    | 6  | Randy | 85000  | 1            |
    +----+-------+--------+--------------+

The Department table holds all departments of the company.  

    +----+----------+
    | Id | Name     |
    +----+----------+
    | 1  | IT       |
    | 2  | Sales    |
    +----+----------+

Write a SQL query to find employees who earn the top three salaries in each of the department. For the above tables, your SQL query should return the following rows.  

    +------------+----------+--------+
    | Department | Employee | Salary |
    +------------+----------+--------+
    | IT         | Max      | 90000  |
    | IT         | Randy    | 85000  |
    | IT         | Joe      | 70000  |
    | Sales      | Henry    | 80000  |
    | Sales      | Sam      | 60000  |
    +------------+----------+--------+

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/department-top-three-salaries)  

Credits To: [leetcode.com](https://leetcode.com/problems/department-top-three-salaries/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/department-top-three-salaries
    select t4.Name as Department, t3.Name as Employee, t3.Salary
    from
        (select t1.Id, t1.Name, t1.Salary, t1.DepartmentId, count(1) as rank
        from Employee as t1 inner join Employee as t2
        on t1.DepartmentId = t2.DepartmentId
        where t1.Salary <= t2.Salary
        group by t1.Id, t1.Name, t1.Salary, t1.DepartmentId) as t3
        inner join Department as t4
        on t3.DepartmentId = t4.Id
    where rank<=3
    order by t4.Name, t3.Salary desc
