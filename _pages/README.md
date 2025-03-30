# Crypto Market Lead-Lag Analysis: Exploring Cross-Exchange and Intra-Exchange Cryptocurrency Correlations		
									
## Team:
Zehao Li (zehao3@illinois.edu, Team Leader):\
Zehao, a senior at the University of Illinois at Urbana-Champaign, is set to graduate in 2023 with a major in Computer Science & Statistics from the LAS Department. He has a passion for programming in Java, C++, and database development, with a focus on data analysis and backend development.

Tony Chang(yaowenc2@illinois.edu):\
Tony is a current junior at the University of Illinois at Urbana-Champaign pursuing a dual degree in Computer Science, Statistics. Tony is graduating May 2024, with experience in working at Meta and Amazon. Tony enjoys analyzing massive amounts of data, conducting machine learning and algorithmic models on data, and building data pipelines.

You Lyu (youlyu2@illinois.edu):\
Hi, I'm You Lyu, a senior Computer Science student at UIUC. I'm passionate about technology and its positive impact. I've taken diverse courses in programming, algorithms, and databases and worked on interesting projects, enhancing my skills and knowledge. I'm eager to further my education and growth in this dynamic field.					

## Project Description:

The project is our semester-long project for “IE421 - High-Frequency Trading” under Professor David Lariviere.\
Our project mainly focuses on analyzing the time lead and lag of the crypto market. We do both analyses across exchanges for the same crypto and across crypto for the same exchange.

We generally break the project down into five sections:
1. Mock Data:\
We created a lead-lag time series generator. Before getting data from API, we   simulate the data by randomly generating a series of data to test the functionality of our model.
2. Market Data parser:\
We collected multiple years of crypto data from ALPACA market data API and turned the data into a structure that is easy for our analyzing framework to use.
3. Analyzing frameworks:\
We ultimately decided on two frameworks, the Naples model and the Bachelier model, that can analyze the time lead and lag of market data. Using these two frameworks to generate two different results, we can find similarities between the two outcomes. This outcome ensures we find a more reliable relationship among those market data. 
4. Analyzer:\
We further filtered the data and implemented two models we wrote into the market data. We also gave specific comparisons of time lead lag among those in the analyzer.
5. Visualization:\
We developed an interface that enables users to collect and analyze the data they want. It can be specific to, for example, Bitcoin’s time lead-lag in Jan 2022 in the exchange of Coinbase. After putting these keywords into the interface, it will automatically analyze the data. 
				
## Technologies:
### Alpaca API
Alpaca API is a RESTful API provided by Alpaca, a commission-free trading platform for individual traders and developers. We will use the crypto market API to gather yearly crypto trades data from CBSE, FTXU, ERSX three exchanges in total.  We will say that the crypto market API is not perfect as it’s still in its beta phase.  However, it gives us enough information to conduct meaningful analysis on the data.


### NAPLES algorithm(https://arxiv.org/pdf/2002.00724.pdf)
<p><img src="images/image27.png" /></p>

This algorithm follows a simple idea: If X is leading Y, we let trading Y follow the movement of X and see whether it makes a profit or loss. 

The method can handle non-synchronized time series and has a computationally efficient linear cost O(n) with respect to the number of operations. More details can be found in the link of the paper.
Note: this algorithm is fully implemented from scratch(by Tony) based on the research paper. 

### BACHELIER algorithm
The Bachelier lead-lag model involves a two-dimensional Brownian motion with a correlation coefficient. It introduces a lead-lag effect by shifting the time-delayed version of the process by a lead or lag time. The model is defined by two constants, x0 and y0, and two positive constants, σ1 and σ2. The lead-lag parameter represents the amount of time that one process anticipates the other. The model can be interpreted as a Black-Scholes version by exponentiating the processes.

### Grainger Causality algorithm(abandoned)
Performing Grainger Causality test, which analyzes how useful a time series is in forecasting another time series data.
Abandoned due to worse performance and high time complexity when dealing with large amounts of asynchronous data.

### Cross correlation algorithm(abandoned)
Shift the data and see which amount of shift can achieve the highest cross correlation. 
Abandoned due to worse performance and high time complexity when dealing with large amounts of asynchronous data.

## Components:
<p><img src="images/image34.png" /></p>

### Config Json
The JSON object describes a configuration for our cryptocurrency trading application. The top-level keys are Mode, Model, exchange, and crypto, which provide information about the application's operation.\
1. Mode:\
A string that specifies the mode of operation for the application. In this case, it is set to "exchange".
2. Model:\
A string that specifies the model being used by the application. In this case, it is set to "naples".
3. exchange:\
An object that contains additional information for the "exchange" mode. It has keys for the year, month, exchanges, crypto, symbol, and output path.
4. crypto:\
An object that contains additional information for the "crypto" mode. It has keys for the year, month, exchange, cryptos, and output path. This JSON object likely represents a configuration file that is used to specify the parameters for running the financial or cryptocurrency trading application.

### Interface.py
This interface.py acts as the pipeline, which can collaborate with all the functions from loading data to running model and show the visualization. By manipulating the interface.py, users can access all the functionalities of the project.

## Git Repo Layout (File / Folder Layout of your project)
Describe briefly how your source code and project repo files and folders are layed out, what is where, etc.
```
.
├── 421libraries
├── data_analyzer/
│   ├── bachelier_analyzer.py
│   └── naples_analyzer.py
├── data_collectors/
│   ├── data/
│   ├── AlpacaHistoricaData.py
│   ├── safe_request.py
│   ├── task.py
│   └── task_executor.py
├── data_generator/
│   └── data_generator.py
├── data_parser/
│   ├── parse_parquet.ipynb
│   └── parser.py
├── data_visualization/
│   ├── bachelier_visualization.py
│   ├── naples_visualization.py
│   ├── time_gap.ipynb
│   └── time_gap.py
├── lead_lag_frameworks/
│   ├── bachelier_model/
│   │   ├── bachelier_lead_lag_analysis.py
│   │   ├── contrast.py
│   │   └── lead_lag.py
│   ├── cross_correlation_lead_lag_analysis.py
│   ├── granger_casuality_lead_lag_analysis.py
│   └── naples_model.py
├── outputs
├── venv
├── .env
├── .gitignore
├── config.json
├── interface.py
├── main.py
└── README.md
```
## Previous years data loaded on Box:
The Uofi app box contains a collection of data files that store historical cryptocurrency price data for several years. It contains CBSE FTXU and ERSX as exchanges and numerous crypto currencies.
https://uofi.box.com/s/rl9qtk481uhpjiy0aix7hil69adfy11q
```
├── data_collectors/
│   ├── data/
```

## Instructions for using your project:				
### 1. Program install
#### a. Git Clone
Clone with HTTPS by accessing this link: https://gitlab.engr.illinois.edu/ie421_high_frequency_trading_fall_2022/ie421_hft_fall_2022_group_01/hft_project.git \
#### b. Register Alpaca API
1. Access the link https://alpaca.markets/
2. Sign up a app builder account in the alpaca
<p><img src="images/image31.jpg" /></p>

3. After we get to the dashboard, press API/Devs in the sidebar. 
<p><img src="images/image36.jpg" /></p>

4. Generate a new API key and secret key.
5. Copy and paste the key and secret key to this task_executor.py under the data_collectors folder
<p><img src="images/image44.png" /></p>

### 2. Configure the parameter required
<p><img src="images/image5.png" /></p>

#### a. The Mode is the mode selection attribute it has two options
  1. exchange\
The exchange mode will investigate the lead-lag of the same crypto in different exchanges
  2. crypto\
The crypto mode will investigate the lead-lag of the different crypto in the same exchange

### 3. Run the project
#### a. Open up a terminal
#### b. Execute the command: ```python3 interface.py```
#### c. Firstly, our program will check whether it contains the required data.
1. If we have the data, nothing will happen
2. Otherwise, it will ask whether you want to collect the data from alpaca API\
   + If the answer is Yes, the program will automatically collect the data and display the results after the data was collected
   + Otherwise, the program will exit.
									
## Project Results					

We mainly analyze the time lead and lag of the crypto market. This analysis aims to find the leading index and provide a more detailed & truth-based comparison in the crypto market. We basically use two kinds of models to prove the results of each other. One is called Naples, and the other one is called Bachelier. The running time of the Naples model, it’s faster, but the Bachelier model processes the data slower than the other model. We could not only analyze the data of one crypto across any exchange but analyze the data of any crypto across one exchange, and we tested our model with data from both 2022 and 2021. As an example of our results, we will show the comparison and contrasts between the two models of 2022 March in this report. In addition, the source of market data is also not quite reliable when it comes to some small exchanges. Some exchanges are always or sometimes offline, so we are not able to collect data in those months, which leads to the inconsistency of our results. Nevertheless, analyzing the data month by month will help us offset this issue to a certain degree.
### Naples Model results
The result here is from 2022/3 BTC. We will run the model and perform yearlong analysis below in the other section.
<p><img src="images/image20.jpg" /></p>

<p><img src="images/image3.jpg" /></p>

<p><img src="images/image30.jpg" /></p>

We see that CBSE leads ERSX and FTXU, most of them by 20000ns. We see that ERSX slightly leads FTXU, since all the data points are negative, but the amount of lead is not significant. Some other visualizations to examine the pattern day by day and the spread of the data is denoted by the boxplot and scatter plot below.

<p><img src="images/image25.jpg" /></p>

<p><img src="images/image12.jpg" /></p>

<p><img src="images/image39.jpg" /></p>

<p><img src="images/image11.jpg" /></p>

<p><img src="images/image42.jpg" /></p>

<p><img src="images/image47.jpg" /></p>

Now we move on to the lead lag analysis of cryptos BTC,ETH, LTC. 

<p><img src="images/image13.jpg" /></p>

<p><img src="images/image33.jpg" /></p>

<p><img src="images/image24.jpg" /></p>

We see that there may be slight lead of BTC as most of the data. However the lead lag is significantly small, till a point that it’s nearly 0. Some other visualizations to examine the pattern day by data and the spread of the data is denoted by the boxplot and scatter plot below.

<p><img src="images/image9.jpg" /></p>

<p><img src="images/image7.jpg" /></p>

<p><img src="images/image19.jpg" /></p>

<p><img src="images/image40.jpg" /></p>

<p><img src="images/image18.jpg" /></p>

<p><img src="images/image8.jpg" /></p>

### Bachelier Model results
Based on this model, you can observe that CBSE has a lead over the other two models.

<p><img src="images/image6.png" /></p>

<p><img src="images/image43.png" /></p>

<p><img src="images/image35.png" /></p>

In addition, based on the same model, you can observe that BTC always has a lag over other cryptos.

<p><img src="images/image2.png" /></p>

<p><img src="images/image29.png" /></p>

### Combined Analysis

We will now run the data on all the data in 2022.

<p><img src="images/image1.jpg" /></p>

<p><img src="images/image28.jpg" /></p>

<p><img src="images/image15.jpg" /></p>

We see that CBSE again leads FTXU and ERSX. CBSE leads ERSX about 10000ns and FTXU about 20000ns.  Some other visualizations to examine the pattern day by data and the spread of the data is denoted by the boxplot and scatter plot below.

<p><img src="images/image45.jpg" /></p>

<p><img src="images/image38.jpg" /></p>

<p><img src="images/image37.jpg" /></p>

<p><img src="images/image22.jpg" /></p>

<p><img src="images/image4.jpg" /></p>

<p><img src="images/image16.jpg" /></p>

We see that there are some months that may result in more possibilities of outliers. Currently, we do not have a specific conclusion as to why that happens(specific event happening during those months, error in the alpaca api etc).
Now we do the cross crypto analysis. 

<p><img src="images/image46.jpg" /></p>

<p><img src="images/image14.jpg" /></p>

<p><img src="images/image21.jpg" /></p>

We see that the lead lag is across cryptos are nearly 0, with at most BTC leads ETH by a little. Thus, there aren’t significant lead lags across different cryptos compared to exchanges.  Some other visualizations to examine the pattern day by data and the spread of the data is denoted by the boxplot and scatter plot below.

<p><img src="images/image26.jpg" /></p>

<p><img src="images/image10.jpg" /></p>

<p><img src="images/image23.png" /></p>

<p><img src="images/image17.jpg" /></p>

<p><img src="images/image41.jpg" /></p>

<p><img src="images/image32.jpg" /></p>
				
## Zehao Li

1. What did you specifically do individually for this project?
* Implemented Bachelier model to the analyzation of market data.
* Implemented Visualization graph for the corresponding model.
* Analyzed the time lead-lag using the Bachelier model.
* Designed the general structure of the project.
* Collected data from Alpaca data API. 
* Performed code reviews.
2. What did you learn as a result of doing your project?
* I learned how market data is recorded and how I should deal with those valuable data. To be specific, I know how to implement models to analyze and help me predict and market. Besides, I understand more about the intrinsic value of High-Frequency trading, which takes every millisecond as an essential data point and can make a significant difference with different exchanges and indexes.
* Applying the models I developed to the market data likely required me to use a variety of data filtering and manipulation techniques. This process has helped me gain experience in data cleaning, feature engineering, and model implementation.
* Developing the Naples and Bachelier models required me to have a deep understanding of statistical modeling and time series analysis. This process has helped me gain a better understanding of how to choose the appropriate framework for a given data set and how to interpret the results.
3. If you had a time machine and could go back to the beginning, what would you have done differently?
* One thing I will do is have a tight schedule so that we won’t postpone this project for such a long time.
* Another thing that I would do is do a better job at finding a reliable data resource or trying to find an alternative data source other than this single one.
4. If you were to continue working on this project, what would you continue to do to improve it, how, and why?
* If we continue working on this project, I will choose to make my model run in a faster time. By achieving this, I need to add multithreading to the model. When a large dataset comes to the model, the current model might be a little overloaded so that it takes a long time to analyze the data.
* Besides, I will choose to find another dataset and improve the completeness of our dataset. Since many exchanges are offline in Alpaca data API, we cannot collect data in those months. Even that might not hurt the overall results, but it still affects the completeness of our project.
5. What advice do you offer to future students taking this course and working on their semester-long project. Providing detailed thoughtful advice to future students will be weighed heavily in evaluating your responses.
* Try to find a project that you are really curious about or like, or you might not be able to pick it up during the semester or finish it on-time.
* Besides, always try to enlarge your data collection. That will make your test results much more reliable.
		


## You Lyu
1. What did you specifically do individually for this project?\
I specifically designed the data collecting tools and process for this project at the first half of the semester and focused on integrating the data collecting tool and the data analyzer and visualizer that Zehao and Tony wrote together.
* First half of the semester:
  + Discover the usage and capability of the Alpaca Market Data API.
  + Dissemble the data collection job into several tasks.
  + Developed a queuing system for data collecting tasks.
  + Define the executor of the tasks queue.
* Second Half of the semester:
  + Read and understand the data analyzer and data visualizer code that we have.
  + Made the project ‘one-click’ program by integrating the data collecting tool with the data analyzer and visualizer.
  + Enabled the interface to autodetect missing data and automatically collect the missing data.
2. What did you learn as a result of doing your project?
* I have gained knowledge and expertise in using the Alpaca Market Data API to collect financial data and a queuing system to organize data collection tasks and an executor to manage the queue.
* I also gains Project management skills. I have learned how to manage a complex project, including breaking it down into smaller tasks and coordinating with other team members. I also gained experience in integrating different software tools and modules.
* By integrating the data collecting tool with the data analyzer and visualizer, I have developed a "one-click" program that can automatically detect and collect missing data. This required problem-solving skills and creativity to develop a solution that streamlined the data collection process.
* Most importantly, I worked with other team members, Zehao and Tony, and collaborated with them to integrate the data collecting tool and data analyzer/visualizer modules. I gained experience in communicating and coordinating with others to achieve a common goal.
3. If you had a time machine and could go back to the beginning, what would you have done differently?\
I plan to create a rigorous timeline to prevent any prolonged delays in the project. Additionally, If given the opportunity to undertake this project again, I would prioritize using a virtual machine for the sake of convenience and collaboration. A virtual machine would allow me to run multiple operating systems on a single physical machine, providing a sandbox environment for testing and developing the software. This would make it easier to set up a uniform development environment across team members, streamlining collaboration and ensuring consistency. Additionally, using a virtual machine would also eliminate the need to purchase and configure individual physical machines for each team member, saving both time and resources. Overall, I believe that using a virtual machine would be a significant improvement in terms of convenience and collaboration for this project.		
4. If you were to continue working on this project, what would you continue to do to improve it, how, and why?\
If given the opportunity to continue working on this project, my focus would be on developing a user-friendly front-end UI. Although our current implementation is a one-click project, there is still a learning curve associated with running it. By creating a front-end UI, we can significantly reduce the learning cost and make the project more accessible to non-computer science users. This would be particularly valuable for clients or stakeholders who may not be familiar with technical jargon or command line interfaces. A user-friendly front-end UI would also improve the overall user experience and provide a more professional and polished final product. Therefore, I believe that developing a front-end UI would be a significant value-add to our project.

5. What advice do you offer to future students taking this course and working on their semester long project (besides “start earlier”... everyone ALWAYS says that). Providing detailed thoughtful advice to future students will be weighed heavily in evaluating your responses.
* Put more effort into the initial proposal of the project: The initial proposal is a crucial step in the project as it sets the foundation for the rest of the work. Take the time to carefully consider the problem you want to solve, the methods you plan to use, and the potential challenges you may face. A well-defined project proposal will help you stay on track throughout the semester and ensure that you achieve your project goals.
* Communicate with the professor more: The professor is a valuable resource and can provide guidance and support throughout the project. Regularly check in with the professor to receive feedback on your progress and ensure that you are on the right track. Additionally, try to get a clearer view of the industry and the problem you are trying to solve. The professor may be able to provide valuable insights and connections that can help you with your project.



## Tony Chang

1. What did you specifically do individually for this project?
* Created mock data generator to test our framework before applying to real data
* Implemented Granger and cross correlation model, which later tested to be not as efficient 
* Implemented Naples model to the analyzation of market data(very efficient and best model)
* Created the basic parser to gather crypto trade information using the Alpaca API
* Changed how the information is saved and the folder structure
* Collected data from Alpaca data API. 
* Created boxplot, distribution scatter plot, and histogram of the result
* Analyze and visualize all the final results
2. What did you learn as a result of doing your project?
* I learned how to handle massive amounts of data. A simple O(n) to O(n^2) already can create, since our data contains way too much information. Furthermore, we should be storing the data in the most effective manner to minimize storage space too.
* I also learned how to read research paper and implement effective solutions. With the need to handle asynchronous data while being the most effective, I went to read the research paper and ultimately implemented the NAPLES model from scratch. 
* Never rely on a beta version API.  
3. If you had a time machine and could go back to the beginning, what would you have done differently?

* I will try to find a better source of information since Alpaca crypto trading API is still in the beta version. It’s hard to use and oftentimes lacking information.
* I will try to read more research papers and find different algorithms that can all conduct asynchronous lead lag analysis.

4. If you were to continue working on this project, what would you continue to do to improve it, how, and why?
* I will want to try out different models and compare their time complexity(interesting to know the accuracy and the time complexity of the existing algorithms!)
* I will try to find another datasource that gathers a stable amount of information instead of the Alpaca crypto data API(more/better data = better results).
* I will try to build a dashboard or a real time visualization of the lead lag, or using the information of the lead lag and develop a trading strategy(interesting side project!). 
5. What advice do you offer to future students taking this course and working on their semester-long project. Providing detailed thoughtful advice to future students will be weighed heavily in evaluating your responses. 	
* Find a project that everyone is passionate about, it will make everyone’s lives easier
* Think and plan out every step before diving into the project. If any part is confusing, discuss it and try to solve it ASAP with team members or the professor. It is important to keep going knowing how to approach the next steps.
		
