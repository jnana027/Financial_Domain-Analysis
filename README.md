# Financial_Domain-Analysis

/*1.Total_Loan_application*/
  select distinct(count(id)) as Total_Loan_application from financial_loan

  /*MTD Total_Loan_application*/
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   count(id) as MTD_Loan_application from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   order by year,Month_Number

   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   case when MONTH(issue_date)=1 then 'Jan'
    when MONTH(issue_date)=2 then 'Feb'
	when MONTH(issue_date)=3 then 'Mar'
	when MONTH(issue_date)=4 then 'April'
	when MONTH(issue_date)=5 then 'May'
	when MONTH(issue_date)=6 then 'Jun'
	when MONTH(issue_date)=7 then 'July'
	when MONTH(issue_date)=8 then 'Aug'
	when MONTH(issue_date)=9 then 'Sep'
	when MONTH(issue_date)=10 then 'Oct'
	when MONTH(issue_date)=11 then 'Nov'
	else 'Dec' End as Month_Name,
   count(id) as MTD_Loan_application from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   order by year,Month_Number



   /*MOM Total_Loan_application
   formula=(MTD-PMTD)/PMTD*/
   with cte as(
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   count(id) as MTD_Loan_application from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   ),
   cte2 as(
   select *,
   lag(MTD_Loan_application) over (order by year,Month_Number) as PMTD_Total_Loan_application
   from cte
   )
   select * from cte2
   order by year,Month_Number



 with cte as(
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   count(id) as MTD_Loan_application from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   ),
   cte2 as(
   select *,
   cast(lag(MTD_Loan_application) over (order by year,Month_Number) as float) as PMTD_Total_Loan_application
   from cte
   )
   select *,(MTD_Loan_application-PMTD_Total_Loan_application) as Varience,
  round( ((MTD_Loan_application-PMTD_Total_Loan_application)/PMTD_Total_Loan_application)*100,2) as Percentage_MTD from cte2
   order by year,Month_Number


/*2. Total Funded Amount */
select * from financial_loan
select sum(loan_amount) as Total_Funded_Amount from financial_loan

/*MTD Total_Funded_amount*/
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   sum(loan_amount) as MTD_Total_Funded_amount from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   order by year,Month_Number


   
   /*MOM Total_Funded_amount
   formula=(MTD-PMTD)/PMTD*/
  with cte as(
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
    sum(loan_amount) as MTD_Total_Funded_amount from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   ),
   cte2 as(
   select *,
   lag(MTD_Total_Funded_amount) over (order by year,Month_Number) as PMTD_Total_Funded_amount
   from cte
   )
   select * from cte2
   order by year,Month_Number



 /*3. Total Amount Received */
select * from financial_loan
select sum(total_payment) as Total_Amount_Received from financial_loan

/*MTD Total_Funded_amount*/
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   sum(total_payment) as MTD_Total_Amount_Received from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   order by year,Month_Number


   
   /*MOM Total_Funded_amount
   formula=(MTD-PMTD)/PMTD*/
  with cte as(
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
    sum(total_payment) as MTD_Total_Amount_Received from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   ),
   cte2 as(
   select *,
   lag(MTD_Total_Amount_Received) over (order by year,Month_Number) as PMTD_Total_Amount_Received
   from cte
   )
   select * from cte2
   order by year,Month_Number


 /*4. Average Interest Rate */
select * from financial_loan
select round(avg(int_rate)*100,2) as Average_Interest_Rate from financial_loan

/*MTD Total_Funded_amount*/
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   round(avg(int_rate)*100,2) as MTD_Average_Interest_Rate from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   order by year,Month_Number


   
   /*MOM Total_Funded_amount
   formula=(MTD-PMTD)/PMTD*/
  with cte as(
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   round(avg(int_rate)*100,2) as MTD_Average_Interest_Rate from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   ),
   cte2 as(
   select *,
   lag(MTD_Average_Interest_Rate) over (order by year,Month_Number) as PMTD_Total_Amount_Received
   from cte
   )
   select * from cte2
   order by year,Month_Number



   
     /*5. Average DTI */
select * from financial_loan
select round(avg(dti)*100,2) as Average_Interest_Rate from financial_loan

/*MTD Average DTI*/
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   round(avg(dti)*100,2) as MTD_Average_DTI from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   order by year,Month_Number


   
   /*MOM Average DTI
   formula=(MTD-PMTD)/PMTD*/
  with cte as(
   select
   YEAR(issue_date) as Year,
   MONTH(issue_date) as Month_Number,
   round(avg(dti)*100,2) as MTD_Average_DTI from financial_loan 
   group by YEAR(issue_date),MONTH(issue_date)
   ),
   cte2 as(
   select *,
   lag(MTD_Average_DTI) over (order by year,Month_Number) as PMTD_Average_DTI
   from cte
   )
   select * from cte2
   order by year,Month_Number


/*6 Total Good Loan*/
select distinct(count(id)) as Total_good_loan_application from financial_loan where loan_status='fully Paid' or loan_status='current' 

/* Total Good Loan percentage*/
select
round((count(case when loan_status='fully Paid' or loan_status='current' then id end)*100.0)/count(id),2) as Total_Good_Loan_percentage
from financial_loan

/*Good loan Funded Amount*/
select sum(loan_amount) as Good_loan_Funded_Amount  from financial_loan
where loan_status='fully Paid' or loan_status='current' 

/*Good loan Received Amount*/
select sum(total_payment) as Good_loan_Received_Amount  from financial_loan
where loan_status='fully Paid' or loan_status='current' 


/*6 Total Bad Loan*/
select distinct(count(id)) as Total_good_loan_application from financial_loan where loan_status='charged off' 

/* Total Bad Loan percentage*/
select
round((count(case when loan_status='charged off' then id end)*100.0)/count(id),2) as Total_Bad_Loan_percentage
from financial_loan

/*Bad loan Funded Amount*/
select sum(loan_amount) as Bad_loan_Funded_Amount  from financial_loan
where loan_status='charged off'

/*Bad loan Received Amount*/
select sum(total_payment) as Bad_loan_Received_Amount  from financial_loan
where loan_status='charged off'


/*7. Loan Status*/
select * from financial_loan

select loan_status,
count(id) as Total_loan_application,
sum(total_payment) as Total_Amount_received,
sum(loan_amount) as Total_Funded_Amount,
AVG(int_rate*100) as interest_rate,
AVG(dti*100) as Average_dti from financial_loan
group by loan_status


select YEAR(issue_date) as year,Month(issue_date) as Month,loan_status,
count(id) as Total_loan_application,
sum(total_payment) as Total_Amount_received,
sum(loan_amount) as Total_Funded_Amount,
AVG(int_rate*100) as interest_rate,
AVG(dti*100) as Average_dti from financial_loan
group by YEAR(issue_date),Month(issue_date),loan_status
order by year,Month

with cte as(
select YEAR(issue_date) as year,Month(issue_date) as Month,loan_status,
count(id) as Total_loan_application,
sum(total_payment) as Total_Amount_received,
sum(loan_amount) as Total_Funded_Amount,
AVG(int_rate*100) as interest_rate,
AVG(dti*100) as Average_dti from financial_loan
group by YEAR(issue_date),Month(issue_date),loan_status
)
select *,
lag(Total_Amount_received) over(partition by loan_status order by YEAR,Month) as P_Total_Amount_received,
lag(Total_Funded_Amount) over(partition by loan_status order by YEAR,Month) as P_Total_Funded_Amount
from cte
order by year,Month


/*Monthly Trend by issue_date*/
select
DATEPART(month,issue_date) as Month_Number,
DATENAME(month,issue_date) as Month_name,
count(id) as Total_loan_application,
sum(loan_amount) as Total_funded_amount,
sum(total_payment) as Total_amount_received from financial_loan
group by DATEPART(month,issue_date),DATENAME(month,issue_date)
order by Month_Number

/*regional analysis by state*/
select
address_state,
count(id) as Total_loan_application,
sum(loan_amount) as Total_funded_amount,
sum(total_payment) as Total_amount_received from financial_loan
group by address_state
order by address_state


/*Loan term analysis*/
select
term,
count(id) as Total_loan_application,
sum(loan_amount) as Total_funded_amount,
sum(total_payment) as Total_amount_received from financial_loan
group by term
order by term

/*Employee length analysis*/
select
emp_length,
count(id) as Total_loan_application,
sum(loan_amount) as Total_funded_amount,
sum(total_payment) as Total_amount_received from financial_loan
group by emp_length
order by emp_length

/*Employee purpose analysis*/
select
purpose,
count(id) as Total_loan_application,
sum(loan_amount) as Total_funded_amount,
sum(total_payment) as Total_amount_received from financial_loan
group by purpose
order by purpose

/*Home ownership analysis*/
select
home_ownership,
count(id) as Total_loan_application,
sum(loan_amount) as Total_funded_amount,
sum(total_payment) as Total_amount_received from financial_loan
group by home_ownership
order by home_ownership



select * from financial_loan

Total loan Application = DISTINCTCOUNT(financial_loan[id])

MTD loan Application = 
var a=CALCULATE([Total loan Application],month('Date Table'[Date])=month(MAX('Date Table'[Date])) && 
YEAR('Date Table'[Date])=year(MAX('Date Table'[Date])))
var b=IF(ISBLANK(a),0,a)
return b

PMTD Loan Application = 
 var a=CALCULATE([Total loan Application],DATESMTD(DATEADD('Date Table'[Date],-1,MONTH)))
 var b=IF(ISBLANK(a),0,a)
 return b

MoM Loan Application = 
var a=([MTD loan Application]-[PMTD Loan Application])
var b=[PMTD Loan Application]
var c=DIVIDE(a,b)
var d=if(ISBLANK(c),0,c)
return d

