Extracting and Visualizing Stock Data

Description

This project involves extracting stock data for companies like Tesla and GameStop and visualizing it using Python. We utilize libraries such as yfinance to gather historical stock data and web scraping techniques to retrieve revenue data. The project then creates informative visualizations, including stock prices and revenue trends, with a focus on data up to June 2021.

Project Objectives

Extract Stock Data: Use the yfinance library to pull historical stock data for Tesla and GameStop.
Web Scraping: Extract revenue data from web sources using BeautifulSoup and store it in a structured format.
Data Visualization: Plot stock price trends and revenue data using interactive charts to provide insights into company performance.
Focus on Timeframe: The graphs are restricted to display data up to June 2021, giving a historical perspective on company performance until this date.
Features
Tesla Stock Data Visualization: Displays Tesla’s historical stock prices and revenue trends up to June 2021.
GameStop Stock Data Visualization: Visualizes GameStop’s stock prices and revenue, providing insights into its performance.
Interactive Plots: The use of plotly creates interactive and visually appealing charts with hoverable data points and range sliders.

Project Workflow

1. Extracting Stock Data Using yfinance
2. 
The yfinance library is used to pull stock data for Tesla and GameStop.

python
Copy
Edit
import yfinance as yf

# Tesla Stock Data
tesla = yf.Ticker("TSLA")
tesla_stock_data = tesla.history(period="max")

# GameStop Stock Data
gme = yf.Ticker("GME")
gme_stock_data = gme.history(period="max")

2. Web Scraping Revenue Data
We use requests and BeautifulSoup to scrape historical revenue data for Tesla and GameStop from the web. The data is stored in a pandas DataFrame for further processing.

python
Copy
Edit
import requests
from bs4 import BeautifulSoup
import pandas as pd

url = "https://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# Extract revenue data from the HTML
table = soup.find("table")
rows = table.find_all("tr")
dates = []
revenues = []

for row in rows[1:]:
    cols = row.find_all("td")
    date = cols[0].text.strip()
    revenue = cols[1].text.strip().replace("$", "").replace(",", "")
    dates.append(date)
    revenues.append(revenue)

# Create DataFrame
gme_revenue = pd.DataFrame({"Date": dates, "Revenue": revenues})
3. Visualizing the Data
Using the plotly library, the stock and revenue data are visualized in a two-row chart: stock price on the first row, and revenue data on the second row.

python
Copy
Edit
import plotly.graph_objects as go
from plotly.subplots import make_subplots

def make_graph(stock_data, revenue_data, stock):
    fig = make_subplots(rows=2, cols=1, shared_xaxes=True, subplot_titles=("Historical Share Price", "Historical Revenue"))
    
    stock_data_specific = stock_data[stock_data.index <= '2021-06-14']
    revenue_data_specific = revenue_data[revenue_data.Date <= '2021-04-30']
    
    # Plot stock data
    fig.add_trace(go.Scatter(x=stock_data_specific.index, y=stock_data_specific['Close'], name="Share Price"), row=1, col=1)
    
    # Plot revenue data
    fig.add_trace(go.Scatter(x=revenue_data_specific['Date'], y=revenue_data_specific['Revenue'], name="Revenue"), row=2, col=1)
    
    fig.update_xaxes(title_text="Date", row=1, col=1)
    fig.update_xaxes(title_text="Date", row=2, col=1)
    fig.update_yaxes(title_text="Price ($US)", row=1, col=1)
    fig.update_yaxes(title_text="Revenue ($US Millions)", row=2, col=1)
    fig.update_layout(title=stock, height=900, showlegend=False)
    
    fig.show()

# Generate Tesla and GameStop stock graphs
make_graph(tesla_stock_data, tesla_revenue, 'Tesla')
make_graph(gme_stock_data, gme_revenue, 'GameStop')
Dependencies
This project requires the following Python libraries:

yfinance: For extracting stock data.
pandas: For handling and manipulating data.
plotly: For creating interactive plots.
requests: For downloading web content.
beautifulsoup4: For web scraping and parsing HTML data.
Install the dependencies using the following command:

bash
Copy
Edit
pip install yfinance pandas plotly requests beautifulsoup4
How to Run the Project
Clone this repository to your local machine:
bash
Copy
Edit
git clone https://github.com/yourusername/stock-visualization.git
Navigate to the project directory:
bash
Copy
Edit
cd stock-visualization
Install the required Python libraries:
bash
Copy
Edit
pip install -r requirements.txt
Run the Python script to extract and visualize stock data:
bash
Copy
Edit
python stock_data_visualization.py
Screenshots

![Screenshot of Tesla Stock Graph](assets/tesla_graph.png)

![Tesla](https://github.com/user-attachments/assets/a87ad0af-fb4e-4e30-8b5a-dfeda2b6552e)

![Screenshot of GameStop Stock Graph](assets/Gamestop.png)

![GameStop](https://github.com/user-attachments/assets/cbda0713-3a07-46c3-86fd-e3abe9b093a7)



About the Author

This project was developed as part of a data analysis initiative  to explore historical stock and revenue data for companies like Tesla and GameStop. It aims to provide a clear visualization of the trends and performance of these companies up to June 2021.
