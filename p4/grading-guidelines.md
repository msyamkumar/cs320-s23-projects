# Project 4 Grading Guidelines

You can find details about the grading process [here](../p1/grading-guidelines.md). 

### Dashboard 
* Missing x, y labels, **-1** (deduct only once)
* Query string is not used, **-2**
* Query string is not descriptive enough, **-1**
    * e.g., still use “from=A” for changing the number of bins of the plot
* Changes to the plot with the query string is not meaningful enough, **-3**
    * e.g., simply changing the color of the entire plot from blue to red
    * Meaningful changes can be changing the x/y column, sorting the bar/hist plot, changing the number of bins, color-coding the scatterplot based on a third categorical column, etc. 
* The two plots with different routes are not distinct enough, **-4**
    * By distinct enough, it means that no significant portion of code is reused to generated the two plots
        * e.g., use scatter plots for both routes and only change the x, y columns
    * Distinct plots can be 
        * Two different types of plots (e.g., one scatter plot and one bar plot) or 
        * The same type of plot but with significant data transformations (e.g., aggregation, filtering, etc.)
* For each plot, hardcoding, **-6**
    * e.g., return random/empty plot