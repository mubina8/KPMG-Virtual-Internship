![Screenshot (331)](https://github.com/mubina8/KPMG-Virtual-Internship/assets/54999073/1a683a4d-9bb2-41a3-841b-dde20faaceeb)
# KPMG-Virtual-Internship
Major Part was RFM Analysis: RFM stands for Recency , Frequency and Monetory. Which identify the targeted and valuable customer in market based on this 3 values
Lets eloborate what is Recency: How recently did the customer make a purchase. Person who make the recent purchase are mostly those customer are valuable for the business.
Frequency : How often does the customer make purchases? Customers with a higher frequency of purchases are likely to be more loyal and active.
Monetory: How much a customer spends money? person who spends more money are considered to be more valuable.
Now we will see RFM Analysis Using Power BI: 
After Cleaning the Dataset create 4 measures in that particuler dataset like this:
last transaction date = MAXX(FILTER('customerDemo',customerDemo[customer_id]=customerDemo[customer_id]),'customerDemo'[transaction_date])
R value = DATEDIFF('customerDemo'[last transaction date],TODAY(),DAY) 
F value = DISTINCTCOUNT('customerDemo'[transaction_id])
M value = 
var TotalSales = SUM('customerDemo'[Profit])
var TotalQuantity = sum(customerDemo[transaction_id])
Return 
DIVIDE (TotalSales,TotalQuantity,0)

After that Create a new table called RFM table like this: RFM table = SUMMARIZE('customerDemo','customerDemo'[customer_id],"R Value",[R Value],"F Value",[F Value],"M Value",[M Value])
Then Create 4 columns R Score, F Score, M Score and RFM  with this: 
R Score = 
SWITCH (
  TRUE (),
   [R value] <= PERCENTILE.INC ( 'RFM table'[R Value], 0.20 ), "5",    
   [R value] <= PERCENTILE.INC ( 'RFM table'[R Value], 0.40 ), "4", 
   [R Value] <= PERCENTILE.INC ( 'RFM table'[R Value], 0.60 ), "3", 
   [R value] <= PERCENTILE.INC ( 'RFM table'[R Value], 0.80 ), "2",
   "1"
       )

F Score = 
SWITCH (
  TRUE (),
   [F value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.20 ), "1",    
   [F value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.40 ), "2", 
   [F Value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.60 ), "3", 
   [F value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.80 ), "4",
   "5"
       )
M Score = 
SWITCH (
  TRUE (),
   [F value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.20 ), "1",    
   [F value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.40 ), "2", 
   [F Value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.60 ), "3", 
   [F value] <= PERCENTILE.INC ( 'RFM table'[F Value], 0.80 ), "4",
   "5"
       )
RFM = 'RFM table'[R Score]& 'RFM table'[F Score]&'RFM table'[M Score]
Lastly upload the segment score table into Power BI and relate to RFM Table and segtment the customer in the visualization


                                  Happy Coding
