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


**6. Profit Margin**

                        Profit Margin = DIVIDE(sum([Profit]), SUM(financials[ Sales]),0)

. . .


**SVG sparklines**

To used SVG Image Sparkline in the card, Search on Google "https://kerrykolosko.com/" and click on templets, choose SVG templets.

![image](https://github.com/Pushpendra5326/Power-BI/assets/145826060/c3a9b24a-8a3f-429f-8375-27c9e48488f9)


Now goto open "Gradient Area Sparkline with last point" and copy "To use in a singular visual" Code, and create the measure as per requirements as below:

            Sales Sparkline / Profit Sparkline / Profit Margin Sparkline = 
                        // Static line color - use %23 instead of # for Firefox compatibility (Measure Derived from Eldersveld Modified by Kolosko)
                        VAR LineColour = "%23118DFF"
                        VAR PointColour = "white"
                        VAR Defs = "<defs>
                            <linearGradient id='grad' x1='0' y1='25' x2='0' y2='50' gradientUnits='userSpaceOnUse'>
                                <stop stop-color='#118DFF' offset='0' />
                                <stop stop-color='#118DFF' offset='0.3' />
                                <stop stop-color='white' offset='1' />
                            </linearGradient>
                        </defs>"
                        // "Date" field used in this example along the X axis
                        VAR XMinDate = MIN(financials[Date])
                        VAR XMaxDate = MAX(financials[Date])
                        
                        // Obtain overall min and overall max measure values when evaluated for each date
                        VAR YMinValue = MINX(Values(financials[Date]),CALCULATE([SUM Gross Sales]))
                        VAR YMaxValue = MAXX(Values(financials[Date]),CALCULATE([SUM Gross Sales]))
                        
                        // Build table of X & Y coordinates and fit to 50 x 150 viewbox
                        VAR SparklineTable = ADDCOLUMNS(
                            SUMMARIZE('financials',financials[Date]),
                                "X",INT(150 * DIVIDE(financials[Date] - XMinDate, XMaxDate - XMinDate)),
                                "Y",INT(50 * DIVIDE([SUM Gross Sales] - YMinValue,YMaxValue - YMinValue)))
                        
                        // Concatenate X & Y coordinates to build the sparkline
                        VAR Lines = CONCATENATEX(SparklineTable,[X] & "," & 50-[Y]," ", financials[Date])
                        
                        // Last data points on the line
                        VAR LastSparkYValue = MAXX( FILTER(SparklineTable, financials[Date] = XMaxDate), [Y])
                        VAR LastSparkXValue = MAXX( FILTER(SparklineTable, financials[Date] = XMaxDate), [X])
                        
                        // Add to SVG, and verify Data Category is set to Image URL for this measure
                        VAR SVGImageURL = 
                            "data:image/svg+xml;utf8," & 
                            --- gradient---
                            "<svg xmlns='http://www.w3.org/2000/svg' x='0px' y='0px' viewBox='-7 -7 164 64'>" & Defs & 
                             "<polyline fill='url(#grad)' fill-opacity='0.3' stroke='transparent' 
                              stroke-width='0' points=' 0 50 " & Lines & 
                              " 150 150 Z '/>" &
                            --- Lines---
                            "<polyline 
                                fill='transparent' stroke='" & LineColour & "' 
                                stroke-linecap='round' stroke-linejoin='round' 
                                stroke-width='3' points=' " & Lines & 
                              " '/>" &
                            --- Last Point---
                                "<circle cx='"& LastSparkXValue & "' cy='" & 50 - LastSparkYValue & "' r='4' stroke='" & LineColour & "' stroke-width='3' fill='"                         & PointColour & "' />" &
                                "</svg>"
                        RETURN SVGImageURL

Note: Use SalesRevenue for Sales Sparkline, Profits for Profit Sparkline and Profit Marnig for Profit margin Sparkline instead of *SUM Gross Sales*.

**Create Visuals**

Create all visuals to which meet the minimum standards of having font style **"Segoe UI / Segoe UI Light"**, Font size **"12"** and Code for colour **"#4D6678"** that the tab order in your report makes sense.


**Publish to Power BI Service**

To publish the report on Power BI service, Click on Publish and fill the credentials and publish.

![image](https://github.com/Pushpendra5326/Power-BI/assets/145826060/2d1ed2ad-36f7-4115-8d71-8375df039483)


***Thank you!!***






