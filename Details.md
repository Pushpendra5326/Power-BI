**Workout Wednesday || Power BI Challenge 2023 Week 26**


**Challenge OverView**

Today’s challenge I’ll display a few key metrics from the inbuilt sample dataset using the new card visual. I’ll present a few options, but feel free to play around with the design and selected metrics.

. . .

**Steps**
1. Fetch Data in power BI as excel format
2. Create required measures
3. SVG sparklines
3. Create Visuals:

            a. New Card

            b. Text Boxes

            c. Slicers

            d. Logo Image
   
            e. Filter
   
            f. Clustered Column Chart
5. Publish to Power BI Service

. . .

**Fetch Data in power BI as excel format**

To get raw data in power BI, Goto Home >> Click on Excel WorkBook >> Browse file from location [financials] >> Click on file check box at Navigator window >> Click on load.

![Screenshot 2023-11-20 081554](https://github.com/Pushpendra5326/Power-BI/assets/145826060/01789ca9-9889-4793-8fd0-5e8844e45c08)

Now, Read the sample data carefully which contain 16 Columns and 700 Rows with different types of Data Types.

![Data types](https://github.com/Pushpendra5326/Power-BI/assets/145826060/023d5f6f-0e01-4317-9cc3-2044c7a96af2)

. . .

**Create required measures**

To create measure: Right click on any of column name at power bi desktop and select **New Measure** Then write a query & New measure will be created.

![image](https://github.com/Pushpendra5326/Power-BI/assets/145826060/0294b54b-4fe2-4aac-95c7-bd8e7e3e797d)
 
I have created total 6 measures using DAX query.

**1. Profits**

                        Profits = SUM(financials[Profit])

**2. Profit last Month**

                        Profit last month = 
                                                CALCULATE(
                                                             [Profits],
                                                             PARALLELPERIOD(
                                                            financials[Date],
                                                                                -1,
                                                                                MONTH)
                                                            )

**3. SalesRevenue**

                        SalesRevenue = SUM(financials[ Sales])

**4. Profit MoM Var**

                        Profit MoM Var = [Profits]-[Profit last month]

**5. Profit Mom % Var**

                        Profit MoM % Var = DIVIDE([Profit MoM Var], [Profit last month], 0)




